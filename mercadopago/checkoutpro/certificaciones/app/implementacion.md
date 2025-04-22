# Guía de Implementación: E-commerce con Next.js y Mercado Pago Checkout Pro

Esta guía te ayudará a crear un sitio e-commerce básico con un producto y carrito utilizando Next.js, e integrar Mercado Pago Checkout Pro para la certificación.

## Índice
1. [Requisitos previos](#requisitos-previos)
2. [Configuración del proyecto Next.js](#configuración-del-proyecto-nextjs)
3. [Creación del e-commerce básico](#creación-del-e-commerce-básico)
   - [Estructura de carpetas](#estructura-de-carpetas)
   - [Modelo de producto](#modelo-de-producto)
   - [Página de inicio](#página-de-inicio)
   - [Componente de producto](#componente-de-producto)
   - [Componente de carrito](#componente-de-carrito)
4. [Integración de Mercado Pago](#integración-de-mercado-pago)
   - [Backend: API Routes](#backend-api-routes)
   - [Frontend: SDK de Mercado Pago](#frontend-sdk-de-mercado-pago)
5. [Configuración de notificaciones](#configuración-de-notificaciones)
6. [Prueba de integración](#prueba-de-integración)

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- [Node.js](https://nodejs.org/) (versión 18 o superior)
- NPM o Yarn
- [Cuenta de desarrollador en Mercado Pago](https://www.mercadopago.com.ar/developers)
- Cuentas de prueba (vendedor y comprador) creadas en Mercado Pago
- Credenciales de prueba (Access Token y Public Key)

## Configuración del proyecto Next.js

1. **Crear un nuevo proyecto Next.js**:

```bash
npx create-next-app@latest mp-certification
cd mp-certification
```

Selecciona las siguientes opciones:
- TypeScript: Sí (recomendado, pero opcional)
- ESLint: Sí
- Tailwind CSS: Sí (para estilos)
- App Router: Sí
- Otras opciones según tu preferencia

2. **Instalar las dependencias necesarias**:

```bash
npm install axios @mercadopago/sdk-react @mercadopago/sdk-js
```

## Creación del e-commerce básico

### Estructura de carpetas

Organiza tu proyecto con la siguiente estructura:

```
mp-certification/
├── app/
│   ├── api/
│   │   ├── mercadopago/
│   │   │   ├── create-preference/
│   │   │   │   └── route.js
│   │   │   └── webhook/
│   │   │       └── route.js
│   ├── cart/
│   │   └── page.js
│   ├── components/
│   │   ├── Product.js
│   │   ├── Cart.js
│   │   └── Checkout.js
│   ├── context/
│   │   └── CartContext.js
│   ├── page.js
│   └── layout.js
├── public/
│   └── product-image.jpg
└── ...
```

### Modelo de producto

Crea un archivo `app/models/product.js` para definir el producto de ejemplo:

```javascript
export const product = {
  id: "1234", // 4 dígitos numéricos
  title: "Smartphone Pro Max", // Nombre del producto
  description: "Dispositivo de tienda móvil de comercio electrónico",
  image: "/product-image.jpg", // Colocar una imagen en la carpeta public
  price: 50000, // Precio en centavos, equivalente a >US$1
  quantity: 1
};
```

### Contexto del carrito

Crea un contexto para gestionar el estado del carrito (`app/context/CartContext.js`):

```javascript
'use client';

import { createContext, useState, useContext } from 'react';

const CartContext = createContext();

export function CartProvider({ children }) {
  const [cart, setCart] = useState([]);

  const addToCart = (product) => {
    setCart([...cart, product]);
  };

  const clearCart = () => {
    setCart([]);
  };

  const getTotalPrice = () => {
    return cart.reduce((total, item) => total + item.price, 0);
  };

  return (
    <CartContext.Provider value={{ cart, addToCart, clearCart, getTotalPrice }}>
      {children}
    </CartContext.Provider>
  );
}

export function useCart() {
  return useContext(CartContext);
}
```

Modifica el archivo `app/layout.js` para incluir el proveedor de contexto:

```javascript
import { CartProvider } from './context/CartContext';
import './globals.css';

export default function RootLayout({ children }) {
  return (
    <html lang="es">
      <body>
        <CartProvider>
          {children}
        </CartProvider>
      </body>
    </html>
  );
}
```

### Página de inicio

Crea la página principal (`app/page.js`):

```javascript
'use client';

import Product from './components/Product';
import { product } from './models/product';
import Link from 'next/link';
import { useCart } from './context/CartContext';

export default function Home() {
  const { cart } = useCart();

  return (
    <main className="container mx-auto p-4">
      <header className="flex justify-between items-center mb-8">
        <h1 className="text-2xl font-bold">Mi Tienda para Certificación MP</h1>
        <Link href="/cart" className="bg-blue-500 text-white p-2 rounded flex items-center">
          Carrito ({cart.length})
        </Link>
      </header>
      
      <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
        <Product product={product} />
      </div>
    </main>
  );
}
```

### Componente de producto

Crea el componente de producto (`app/components/Product.js`):

```javascript
'use client';

import Image from 'next/image';
import { useCart } from '../context/CartContext';

export default function Product({ product }) {
  const { addToCart } = useCart();
  
  const handleAddToCart = () => {
    addToCart(product);
    alert('Producto agregado al carrito');
  };

  return (
    <div className="border rounded-lg p-4 flex flex-col">
      <div className="relative h-40 mb-4">
        <Image 
          src={product.image} 
          alt={product.title}
          fill
          style={{ objectFit: 'cover' }}
          className="rounded"
        />
      </div>
      <h2 className="text-xl font-semibold">{product.title}</h2>
      <p className="text-gray-600 my-2">{product.description}</p>
      <p className="text-lg font-bold mt-auto">${product.price / 100}</p>
      <button 
        onClick={handleAddToCart}
        className="bg-green-500 text-white p-2 rounded mt-4"
      >
        Agregar al carrito
      </button>
    </div>
  );
}
```

### Componente de carrito

Crea la página del carrito (`app/cart/page.js`):

```javascript
'use client';

import { useCart } from '../context/CartContext';
import Link from 'next/link';
import { useState } from 'react';
import { initMercadoPago } from '@mercadopago/sdk-react';

export default function Cart() {
  const { cart, getTotalPrice } = useCart();
  const [preferenceId, setPreferenceId] = useState(null);
  const [loading, setLoading] = useState(false);

  const handleCheckout = async () => {
    if (cart.length === 0) return;
    
    setLoading(true);
    try {
      const response = await fetch('/api/mercadopago/create-preference', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          items: cart,
          payer_email: 'test_user_buyer@example.com', // Email del comprador de prueba 
        }),
      });
      
      const data = await response.json();
      setPreferenceId(data.preferenceId);
      
      // Redirigir a la página de checkout de Mercado Pago
      window.location.href = data.init_point;
    } catch (error) {
      console.error('Error al crear preferencia:', error);
      alert('Error al procesar el pago');
    } finally {
      setLoading(false);
    }
  };

  return (
    <main className="container mx-auto p-4">
      <header className="mb-8">
        <Link href="/" className="text-blue-500 hover:underline">
          ← Volver a la tienda
        </Link>
        <h1 className="text-2xl font-bold mt-2">Carrito de compras</h1>
      </header>
      
      {cart.length === 0 ? (
        <p className="text-center py-8">El carrito está vacío</p>
      ) : (
        <>
          <div className="border rounded-lg p-4 mb-4">
            {cart.map((item, index) => (
              <div key={index} className="flex justify-between items-center mb-2 pb-2 border-b">
                <div>
                  <h3 className="font-medium">{item.title}</h3>
                  <p className="text-sm text-gray-600">Cantidad: {item.quantity}</p>
                </div>
                <p className="font-bold">${item.price / 100}</p>
              </div>
            ))}
            <div className="flex justify-between items-center mt-4 pt-2 border-t">
              <h3 className="font-bold">Total:</h3>
              <p className="font-bold">${getTotalPrice() / 100}</p>
            </div>
          </div>
          
          <div className="flex justify-end">
            <button
              onClick={handleCheckout}
              disabled={loading}
              className="bg-blue-500 text-white px-4 py-2 rounded disabled:bg-gray-400"
            >
              {loading ? 'Procesando...' : 'Proceder al pago'}
            </button>
          </div>
        </>
      )}
    </main>
  );
}
```

## Integración de Mercado Pago

### Backend: API Routes

Crea la ruta para generar preferencias (`app/api/mercadopago/create-preference/route.js`):

```javascript
import { NextResponse } from 'next/server';
import { MercadoPagoConfig, Preference } from 'mercadopago';

// Inicializa el cliente de Mercado Pago
const client = new MercadoPagoConfig({ 
  accessToken: process.env.MP_ACCESS_TOKEN,
  options: { 
    integratorId: 'dev_24c65fb163bf11ea96500242ac130004' // ID del integrador
  }
});

export async function POST(request) {
  try {
    const body = await request.json();
    const { items, payer_email } = body;
    
    // Crea el objeto de preferencia
    const preference = new Preference(client);
    
    // URL base para las redirects (ajusta según tu entorno)
    const baseUrl = process.env.VERCEL_URL 
      ? `https://${process.env.VERCEL_URL}` 
      : 'http://localhost:3000';
    
    const preferenceData = {
      items: items.map(item => ({
        id: item.id,
        title: item.title,
        description: item.description,
        picture_url: `${baseUrl}${item.image}`,
        quantity: item.quantity,
        unit_price: item.price / 100, // Convertir de centavos
        currency_id: 'ARS' // Ajusta según tu moneda local
      })),
      
      // URLs de retorno
      back_urls: {
        success: `${baseUrl}/success`,
        failure: `${baseUrl}/failure`,
        pending: `${baseUrl}/pending`
      },
      
      // URL de notificaciones
      notification_url: `${baseUrl}/api/mercadopago/webhook`,
      
      // External reference (correo del usuario)
      external_reference: "tu_correo@ejemplo.com", // Reemplaza con tu correo
      
      // Configuración de pagos
      payment_methods: {
        excluded_payment_methods: [{ id: 'visa' }], // Excluir Visa
        installments: 6 // Máximo 6 cuotas
      },
      
      auto_return: 'approved',
    };
    
    const result = await preference.create({ body: preferenceData });
    
    return NextResponse.json({ 
      preferenceId: result.id,
      init_point: result.init_point
    });
    
  } catch (error) {
    console.error('Error al crear preferencia:', error);
    return NextResponse.json(
      { error: 'Error al crear preferencia' },
      { status: 500 }
    );
  }
}
```

Crea la ruta para recibir webhooks (`app/api/mercadopago/webhook/route.js`):

```javascript
import { NextResponse } from 'next/server';
import { MercadoPagoConfig, Payment } from 'mercadopago';

// Inicializa el cliente de Mercado Pago
const client = new MercadoPagoConfig({ 
  accessToken: process.env.MP_ACCESS_TOKEN 
});

export async function POST(request) {
  try {
    const body = await request.formData();
    
    // Obtener action e ID del webhook
    const action = body.get('action');
    const id = body.get('data.id');
    
    if (action === 'payment.created' || action === 'payment.updated') {
      // Obtener detalles del pago
      const payment = new Payment(client);
      const paymentData = await payment.get({ id });
      
      console.log('Payment ID:', id);
      console.log('Payment status:', paymentData.status);
      
      // Aquí puedes guardar el pago en tu base de datos
      // y actualizar el estado del pedido
    }
    
    return NextResponse.json({ success: true });
  } catch (error) {
    console.error('Error en webhook:', error);
    return NextResponse.json(
      { error: 'Error procesando webhook' },
      { status: 500 }
    );
  }
}

// Configuración para permitir solicitudes de Mercado Pago
export const config = {
  api: {
    bodyParser: false,
  },
};
```

### Variable de entorno

Crea un archivo `.env.local` en la raíz del proyecto:

```
MP_ACCESS_TOKEN=TEST-xxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### Frontend: SDK de Mercado Pago

Crea páginas para manejar los estados de retorno:

- `app/success/page.js`: Página de pago exitoso
- `app/failure/page.js`: Página de pago fallido
- `app/pending/page.js`: Página de pago pendiente

## Prueba de integración

Para probar tu integración:

1. Inicia el servidor de desarrollo:
```bash
npm run dev
```

2. Abre tu navegador en `http://localhost:3000`
3. Agrega el producto al carrito
4. Procede al pago
5. Usa las credenciales de tu usuario comprador de prueba
6. Completa la compra con los datos de tarjeta de prueba

### Datos de prueba

Para tarjetas de prueba, usa:

```
Número: 5031 7557 3453 0604
Fecha: 11/25
CVV: 123
Titular: APRO (para aprobación) 
```

## Solución de problemas comunes

- **Credenciales incorrectas**: Asegúrate de usar el Access Token de tu cuenta de vendedor de prueba.
- **CORS en webhooks**: Agrega encabezados adecuados en tu función de webhook.
- **Redirect URLs**: Verifica que las URLs de retorno estén correctamente configuradas.

## Próximos pasos

Una vez completada la integración básica:

1. Guarda el Payment ID generado durante la simulación
2. Envía el Payment ID para validar tu certificación
3. Mejora la experiencia de usuario con manejo de estados y errores
4. Implementa persistencia de datos para guardar órdenes y pagos

---

Esta guía te proporciona los fundamentos para crear un e-commerce básico con Next.js e integrar Mercado Pago Checkout Pro para la certificación. Personaliza según tus necesidades específicas y recuerda seguir todas las especificaciones de la certificación.