# supabase migration list

Lista el historial de migraciones tanto en bases de datos locales como remotas.

Requiere que tu proyecto local esté vinculado a una base de datos remota ejecutando `supabase link`. Para bases de datos auto-alojadas, puedes pasar los parámetros de conexión usando la bandera `--db-url`.

> Nota que las cadenas de URL deben escaparse según [RFC 3986](https://www.rfc-editor.org/rfc/rfc3986).

Las migraciones locales se almacenan en el directorio `supabase/migrations` mientras que las migraciones remotas se rastrean en la tabla `supabase_migrations.schema_migrations`. Solo se comparan las marcas de tiempo para identificar cualquier diferencia.

En caso de discrepancias entre el historial de migración local y remoto, puedes resolverlas utilizando el comando `migration repair`.

## Uso

```
supabase migration list [flags]
```

## Banderas

- **--db-url <string>** _Opcional_
    
    Lista las migraciones de la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Lista las migraciones aplicadas al proyecto vinculado.
    
- **--local** _Opcional_
    
    Lista las migraciones aplicadas a la base de datos local.
    
- **-p, --password <string>** _Opcional_
    
    Contraseña para tu base de datos Postgres remota.
    

## Ejemplo de uso básico

```
supabase migration list
```

### Respuesta

```
LOCAL      │     REMOTE     │     TIME (UTC)
─────────────────┼────────────────┼──────────────────────
                 │ 20230103054303 │ 2023-01-03 05:43:03
                 │ 20230103093141 │ 2023-01-03 09:31:41
  20230222032233 │                │ 2023-02-22 03:22:33
```