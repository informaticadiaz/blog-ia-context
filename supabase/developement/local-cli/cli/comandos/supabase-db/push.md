# supabase db push

## Descripción

Envía todas las migraciones locales a una base de datos remota.

Requiere que tu proyecto local esté vinculado a una base de datos remota ejecutando `supabase link`. Para bases de datos autoalojadas, puedes pasar los parámetros de conexión usando la bandera `--db-url`.

La primera vez que se ejecuta este comando, se creará una tabla de historial de migraciones en `supabase_migrations.schema_migrations`. Después de aplicar exitosamente una migración, se insertará una nueva fila en la tabla de historial de migraciones con la marca de tiempo como su identificador único. Las siguientes ejecuciones omitirán las migraciones que ya se hayan aplicado.

Si necesitas modificar la tabla de historial de migraciones, como eliminar entradas existentes o insertar nuevas entradas sin ejecutar realmente la migración, usa el comando `migration repair`.

Utiliza la bandera `--dry-run` para ver la lista de cambios antes de aplicarlos.

## Uso

```
supabase db push [banderas]
```

## Banderas

|Bandera|Descripción|
|---|---|
|`--db-url <string>`|Envía a la base de datos especificada por la cadena de conexión (debe estar codificada en porcentaje).|
|`--dry-run`|Muestra las migraciones que se aplicarían, pero no las aplica realmente.|
|`--include-all`|Incluye todas las migraciones no encontradas en la tabla de historial remota.|
|`--include-roles`|Incluye roles personalizados desde supabase/roles.sql.|
|`--include-seed`|Incluye datos de inicialización desde tu configuración.|
|`--linked`|Envía al proyecto vinculado.|
|`--local`|Envía a la base de datos local.|
|`-p, --password <string>`|Contraseña para tu base de datos Postgres remota.|

## Ejemplo de uso básico

```
supabase db push
```

### Respuesta

```
Linked project is up to date.
```