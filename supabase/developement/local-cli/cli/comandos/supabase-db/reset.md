# supabase db reset

## Descripción

Restablece la base de datos local a un estado limpio.

Requiere que el entorno de desarrollo local esté iniciado ejecutando `supabase start`.

Recrea el contenedor local de Postgres y aplica todas las migraciones locales encontradas en el directorio `supabase/migrations`. Si hay datos de prueba definidos en `supabase/seed.sql`, se cargarán después de que se ejecuten las migraciones. Cualquier otro dato o cambio de esquema realizado durante el desarrollo local será descartado.

Cuando se ejecuta `db reset` con la bandera `--linked` o `--db-url`, se ejecuta un script SQL para identificar y eliminar todas las entidades creadas por el usuario en la base de datos remota. Dado que los roles de Postgres son entidades a nivel de clúster, cualquier rol personalizado creado a través del panel de control o `supabase/roles.sql` no será eliminado por el restablecimiento remoto.

## Uso

```
supabase db reset [banderas]
```

## Banderas

|Bandera|Descripción|
|---|---|
|`--db-url <string>`|Restablece la base de datos especificada por la cadena de conexión (debe estar codificada en porcentaje).|
|`--linked`|Restablece el proyecto vinculado con migraciones locales.|
|`--local`|Restablece la base de datos local con migraciones locales.|
|`--no-seed`|Omite la ejecución del script de inicialización después del restablecimiento.|
|`--version <string>`|Restablece hasta la versión especificada.|

## Ejemplo de uso básico

```
supabase db reset
```

### Respuesta

```
Resetting database...
Initializing schema...
Applying migration 20220810154537_create_employees_table.sql...
Seeding data supabase/seed.sql...
Finished supabase db reset on branch main.
```