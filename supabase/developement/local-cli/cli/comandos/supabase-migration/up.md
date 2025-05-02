# supabase migration up

## Uso

```
supabase migration up [flags]
```

## Banderas

- **--db-url <string>** _Opcional_
    
    Aplica migraciones a la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--include-all** _Opcional_
    
    Incluye todas las migraciones no encontradas en la tabla de historial remoto.
    
- **--linked** _Opcional_
    
    Aplica migraciones pendientes al proyecto vinculado.
    
- **--local** _Opcional_
    
    Aplica migraciones pendientes a la base de datos local.