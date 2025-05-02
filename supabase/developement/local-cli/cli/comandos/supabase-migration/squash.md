# supabase migration squash

Comprime las migraciones de esquema locales en un solo archivo de migración.

La migración comprimida es equivalente a un volcado de solo esquema de la base de datos local después de aplicar los archivos de migración existentes. Esto es especialmente útil cuando quieres eliminar modificaciones repetidas del mismo esquema de tu historial de migración.

Sin embargo, una limitación es que las declaraciones de manipulación de datos, como insert, update o delete, se omiten de la migración comprimida. Tendrás que agregarlas manualmente en un nuevo archivo de migración. Esto incluye trabajos cron, buckets de almacenamiento y cualquier secreto cifrado en vault.

Por defecto, el último archivo `<timestamp>_<name>.sql` se actualizará para contener la migración comprimida. Puedes anular la versión objetivo usando la bandera `--version <timestamp>`.

Si tu directorio `supabase/migrations` está vacío, ejecutar `supabase squash` no hará nada.

## Uso

```
supabase migration squash [flags]
```

## Banderas

- **--db-url <string>** _Opcional_
    
    Comprime las migraciones de la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Comprime el historial de migración del proyecto vinculado.
    
- **--local** _Opcional_
    
    Comprime el historial de migración de la base de datos local.
    
- **-p, --password <string>** _Opcional_
    
    Contraseña para tu base de datos Postgres remota.
    
- **--version <string>** _Opcional_
    
    Comprime hasta la versión especificada.