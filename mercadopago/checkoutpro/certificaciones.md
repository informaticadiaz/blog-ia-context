# Certificacion

Los miembros certificados del programa de socios del Mercado Pago, el `<dev>program`, pueden identificar sus integraciones para acceder a los beneficios del programa ya sean estas integraciones antiguas o nuevas. Por eso, no olvides incluir tus credenciales en todas las integraciones que realices.

Para identificarse en sus integraciones y trabajar con métricas, puede usar uno de los SDKs disponibles para enviar el integrator_id y/o platform_id al ejecutar el request de pago.

Además de los SDK, es posible identificar sus integraciones a través de la API de pagos. Por lo tanto, puedes enviar los parámetros x-integrator_id y/o x-platform-id al endpoint /v1/payments al ejecutar el request.

| Header            | Tipo de código | Identificadores                                                            |
| ----------------- | -------------- | -------------------------------------------------------------------------- |
| `x-integrator-id` | Integrador     | Para desarrolladores o agencias que realizaron la integración.             |
| `x-platform-id`   | Plataforma     | Para las plataformas o módulos que ofrecen Mercado Pago en sus soluciones. |

Agrega los códigos de identificación y reemplaza por el valor necesario: `INTEGRATOR_ID`.

  

```js

const requestOptions = {

'integratorId': 'INTEGRATOR_ID',

};

```

