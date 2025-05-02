# supabase gen types

Este comando permite generar tipos basados en tu esquema de base de datos Supabase, facilitando el desarrollo con tipado estático en varios lenguajes de programación.

## Uso

```
supabase gen types [flags]
```

## Flags

### --db-url <string>

_Opcional_

Genera tipos a partir de una URL de base de datos.

### --lang <[ typescript | go | swift ]>

_Opcional_

Lenguaje de salida para los tipos generados. Las opciones disponibles son:

- typescript
- go
- swift

### --linked

_Opcional_

Genera tipos desde el proyecto vinculado.

### --local

_Opcional_

Genera tipos desde la base de datos de desarrollo local.

### --postgrest-v9-compat

_Opcional_

Genera tipos compatibles con PostgREST v9 y versiones anteriores. Usar solo junto con --db-url.

### --project-id <string>

_Opcional_

Genera tipos a partir de un ID de proyecto.

### -s, --schema <strings>

_Opcional_

Lista separada por comas de esquemas a incluir.

### --swift-access-control <[ internal | public ]>

_Opcional_

Control de acceso para los tipos generados en Swift. Las opciones disponibles son:

- internal
- public