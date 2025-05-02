# supabase start

## Descripción

Inicia el stack de desarrollo local de Supabase.

Requiere que el archivo `supabase/config.toml` haya sido creado en tu directorio de trabajo actual mediante la ejecución de `supabase init`.

Todos los contenedores de servicios se inician por defecto. Puedes excluir aquellos que no necesites usando la bandera `-x`. Para excluir múltiples contenedores, puedes pasar una cadena separada por comas, como `-x gotrue,imgproxy`, o especificar la bandera `-x` múltiples veces.

> Se recomienda tener al menos 7GB de RAM para iniciar todos los servicios.

Se agregan automáticamente verificaciones de salud para comprobar los contenedores iniciados. Usa la bandera `--ignore-health-check` para ignorar estos errores.

## Uso

```
supabase start [flags]
```

## Opciones

|Opción|Descripción|
|---|---|
|`-x, --exclude <strings>`|Nombres de los contenedores que no se iniciarán. [gotrue,realtime,storage-api,imgproxy,kong,mailpit,postgrest,postgres-meta,studio,edge-runtime,logflare,vector,supavisor] (Opcional)|
|`--ignore-health-check`|Ignorar servicios no saludables y salir con código 0 (Opcional)|

## Ejemplos

### Uso básico

```
supabase start
```

**Respuesta:**

```
Creating custom roles supabase/roles.sql...
Applying migration 20220810154536_employee.sql...
Seeding data supabase/seed.sql...
Started supabase local development setup.
```

### Iniciar contenedores sin studio e imgproxy

Puedes excluir los contenedores de studio e imgproxy si no los necesitas para tu desarrollo:

```
supabase start -x studio,imgproxy
```

### Ignorar verificaciones de salud de los servicios

Si quieres que el comando continúe incluso si algunos servicios no inician correctamente:

```
supabase start --ignore-health-check
```