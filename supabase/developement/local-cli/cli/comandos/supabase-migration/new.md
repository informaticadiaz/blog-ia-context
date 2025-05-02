# supabase migration new

Crea un nuevo archivo de migración localmente.

Un directorio `supabase/migrations` será creado si aún no existe en tu actual `workdir`. Todos los archivos de migración de esquema deben ser creados en este directorio siguiendo el patrón `<timestamp>_<name>.sql`.

Las salidas de otros comandos como `db diff` pueden ser redirigidas a `migration new <name>` a través de stdin.

## Uso

```
supabase migration new <migration name>
```

## Ejemplo de uso básico

```
supabase migration new schema_test
```

### Respuesta

```
Created new migration at supabase/migrations/20230306095710_schema_test.sql.
```