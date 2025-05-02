# supabase link

## Descripción

Vincula tu proyecto de desarrollo local a un proyecto alojado en Supabase.

Las configuraciones de PostgREST se obtienen de la plataforma Supabase y se validan contra tu archivo de configuración local.

Opcionalmente, la configuración de la base de datos puede ser validada si proporcionas una contraseña. Tu contraseña de base de datos se guarda en el almacenamiento de credenciales nativo si está disponible.

> Si no deseas que se te solicite la contraseña de la base de datos, como en un entorno de CI, puedes especificarla explícitamente a través de la variable de entorno `SUPABASE_DB_PASSWORD`.

Algunos comandos como `db dump`, `db push` y `db pull` requieren que tu proyecto esté vinculado primero.

## Uso

```
supabase link [flags]
```

## Opciones

|Opción|Descripción|
|---|---|
|`-p, --password <string>`|Contraseña de tu base de datos Postgres remota. (Opcional)|
|`--project-ref <string>`|Referencia del proyecto de Supabase. (Opcional)|

## Ejemplos

### Uso básico

```
supabase link --project-ref ********************
```

**Respuesta:**

```
Ingresa tu contraseña de base de datos (o deja en blanco para omitir): ********
Supabase link completado.
```

### Vincular sin contraseña de base de datos

Puedes vincular tu proyecto sin proporcionar la contraseña de la base de datos si no necesitas acceso a la base de datos.

### Vincular usando un solucionador DNS-over-HTTPS

Puedes usar un solucionador DNS-over-HTTPS al vincular tu proyecto para una resolución DNS segura.