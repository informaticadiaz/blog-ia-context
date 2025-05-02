# supabase db pull

## Descripción

Extrae cambios de esquema desde una base de datos remota. Se creará un nuevo archivo de migración en el directorio `supabase/migrations`.

Requiere que tu proyecto local esté vinculado a una base de datos remota ejecutando `supabase link`. Para bases de datos autoalojadas, puedes pasar los parámetros de conexión usando la bandera `--db-url`.

Opcionalmente, se puede insertar una nueva fila en la tabla del historial de migraciones para reflejar el estado actual de la base de datos remota.

Si no existen entradas en la tabla de historial de migraciones, se utilizará `pg_dump` para capturar todo el contenido de los esquemas remotos que hayas creado. De lo contrario, este comando solo comparará los cambios de esquema con la base de datos remota, similar a ejecutar `db diff --linked`.

## Uso

```
supabase db pull [nombre_de_migracion] [banderas]
```

## Banderas

|Bandera|Descripción|
|---|---|
|`--db-url <string>`|Extrae desde la base de datos especificada por la cadena de conexión (debe estar codificada en porcentaje).|
|`--linked`|Extrae desde el proyecto vinculado.|
|`--local`|Extrae desde la base de datos local.|
|`-p, --password <string>`|Contraseña para tu base de datos Postgres remota.|
|`-s, --schema <strings>`|Lista separada por comas de esquemas a incluir.|

## Ejemplo de uso básico

```
supabase db pull
```

### Respuesta

```
Connecting to remote database...
Schema written to supabase/migrations/20240414044403_remote_schema.sql
Update remote migration history table? [Y/n]
Repaired migration history: [20240414044403] => applied
Finished supabase db pull.
The auth and storage schemas are excluded. Run supabase db pull --schema auth,storage again to diff them.
```