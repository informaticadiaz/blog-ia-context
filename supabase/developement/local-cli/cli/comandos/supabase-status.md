# supabase status

## Descripción

Muestra el estado del stack de desarrollo local de Supabase.

Requiere que el stack de desarrollo local haya sido iniciado mediante la ejecución de `supabase start` o `supabase db start`.

Puedes exportar los parámetros de conexión para [inicializar supabase-js](https://supabase.com/docs/reference/javascript/initializing) localmente especificando la bandera `-o env`. Los parámetros compatibles incluyen `JWT_SECRET`, `ANON_KEY` y `SERVICE_ROLE_KEY`.

## Uso

```
supabase status [flags]
```

## Opciones

|Opción|Descripción|
|---|---|
|`--override-name <strings>`|Anula nombres específicos de variables. (Opcional)|

## Ejemplos

### Uso básico

```
supabase status
```

**Respuesta:**

```
supabase local development setup is running.

         API URL: http://127.0.0.1:54321
     GraphQL URL: http://127.0.0.1:54321/graphql/v1
          DB URL: postgresql://postgres:postgres@127.0.0.1:54322/postgres
      Studio URL: http://127.0.0.1:54323
    Inbucket URL: http://127.0.0.1:54324
      JWT secret: super-secret-jwt-token-with-at-least-32-characters-long
        anon key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1kZW1vIiwicm9sZSI6ImFub24iLCJleHAiOjE5ODM4MTI5OTZ9.CRXP1A7WOeoJeXxjNni43kdQwgnWNReilDMblYTn_I0
service_role key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1kZW1vIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImV4cCI6MTk4MzgxMjk5Nn0.EGIM96RAZx35lJzdJsyH-qQwv8Hdp7fsn3W0YpN81IU
```

### Formatear estado como variables de entorno

Puedes exportar los parámetros de conexión como variables de entorno para facilitar la inicialización de supabase-js:

```
supabase status -o env
```

Esta opción es particularmente útil para configurar scripts de desarrollo o CI/CD que necesitan interactuar con tu instancia local de Supabase.

### Personalizar los nombres de las variables exportadas

Si necesitas personalizar los nombres de las variables exportadas, puedes usar la opción `--override-name`:

```
supabase status -o env --override-name JWT_SECRET=SUPABASE_JWT,ANON_KEY=SUPABASE_ANON_KEY
```

Esto es útil cuando trabajas con frameworks que esperan nombres específicos para estas variables, o cuando necesitas evitar conflictos con otras variables de entorno en tu sistema.