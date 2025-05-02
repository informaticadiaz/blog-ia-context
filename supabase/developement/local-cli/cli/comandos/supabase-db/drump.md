# supabase db dump

## Descripción

Vuelca (exporta) contenidos desde una base de datos remota.

Requiere que tu proyecto local esté vinculado a una base de datos remota ejecutando `supabase link`. Para bases de datos autoalojadas, puedes pasar los parámetros de conexión usando la bandera `--db-url`.

Ejecuta `pg_dump` en un contenedor con banderas adicionales para excluir esquemas gestionados por Supabase. Los esquemas ignorados incluyen auth, storage y aquellos creados por extensiones.

El volcado predeterminado no contiene datos ni roles personalizados. Para volcar explícitamente esos contenidos, especifica la bandera `--data-only` o `--role-only`.

## Uso

```
supabase db dump [banderas]
```

## Banderas

|Bandera|Descripción|
|---|---|
|`--data-only`|Vuelca solo los registros de datos.|
|`--db-url <string>`|Vuelca desde la base de datos especificada por la cadena de conexión (debe estar codificada en porcentaje).|
|`--dry-run`|Muestra el script pg_dump que se ejecutaría.|
|`-x, --exclude <strings>`|Lista de esquema.tablas para excluir del volcado de solo datos.|
|`-f, --file <string>`|Ruta del archivo para guardar los contenidos volcados.|
|`--keep-comments`|Mantiene las líneas comentadas de la salida de pg_dump.|
|`--linked`|Vuelca desde el proyecto vinculado.|
|`--local`|Vuelca desde la base de datos local.|
|`-p, --password <string>`|Contraseña para tu base de datos Postgres remota.|
|`--role-only`|Vuelca solo los roles del clúster.|
|`-s, --schema <strings>`|Lista separada por comas de esquemas a incluir.|
|`--use-copy`|Usa declaraciones COPY en lugar de INSERT.|

## Ejemplo de uso básico

```
supabase db dump -f supabase/schema.sql
```

### Respuesta

```
Dumping schemas from remote database...
Dumped schema to supabase/schema.sql.
```