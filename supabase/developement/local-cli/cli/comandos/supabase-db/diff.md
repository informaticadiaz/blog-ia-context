# supabase db diff

## Descripción

Compara los cambios de esquema realizados en la base de datos local o remota.

Requiere que el entorno de desarrollo local esté en ejecución cuando se compara con la base de datos local. Para comparar con una base de datos remota o autoalojada, especifica la bandera `--linked` o `--db-url` respectivamente.

Ejecuta [djrobstep/migra](https://github.com/djrobstep/migra) en un contenedor para comparar las diferencias de esquema entre la base de datos objetivo y una base de datos sombra. La base de datos sombra se crea aplicando migraciones del directorio local `supabase/migrations` en un contenedor separado. La salida se escribe en stdout por defecto. Para mayor comodidad, también puedes guardar la diferencia de esquema como un nuevo archivo de migración pasando la bandera `-f`.

Por defecto, se comparan todos los esquemas en la base de datos objetivo. Utiliza la bandera `--schema public,extensions` para restringir la comparación a un subconjunto de esquemas.

Aunque el comando diff es capaz de capturar la mayoría de los cambios de esquema, hay casos donde puede fallar. Actualmente, esto podría ocurrir si tu esquema contiene:

- Cambios en la publicación
- Cambios en los buckets de almacenamiento
- Vistas con atributos `security_invoker`

## Uso

```
supabase db diff [banderas]
```

## Banderas

|Bandera|Descripción|
|---|---|
|`--db-url <string>`|Compara con la base de datos especificada por la cadena de conexión (debe estar codificada en porcentaje).|
|`-f, --file <string>`|Guarda la diferencia de esquema en un nuevo archivo de migración.|
|`--linked`|Compara los archivos de migración locales con el proyecto vinculado.|
|`--local`|Compara los archivos de migración locales con la base de datos local.|
|`-s, --schema <strings>`|Lista separada por comas de esquemas a incluir.|
|`--use-migra`|Usa migra para generar la diferencia de esquema.|
|`--use-pg-schema`|Usa pg-schema-diff para generar la diferencia de esquema.|
|`--use-pgadmin`|Usa pgAdmin para generar la diferencia de esquema.|

## Ejemplo de uso básico

```
supabase db diff -f my_table
```

### Respuesta

```
Connecting to local database...
Creating shadow database...
Applying migration 20230425064254_remote_commit.sql...
Diffing schemas: auth,extensions,public,storage
Finished supabase db diff on branch main.

No schema changes found
```