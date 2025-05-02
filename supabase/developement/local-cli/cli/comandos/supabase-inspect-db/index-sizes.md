## supabase inspect db index-sizes

Este comando muestra el tamaño de cada índice en la base de datos. Se calcula tomando el número de páginas (reportado en `relpages`) y multiplicándolo por el tamaño de página (8192 bytes).

```
              NAME              │    SIZE
  ──────────────────────────────┼─────────────
    user_events_index           │ 2082 MB
    job_run_details_pkey        │ 3856 kB
    schema_migrations_pkey      │ 16 kB
    refresh_tokens_token_unique │ 8192 bytes
    users_instance_id_idx       │ 0 bytes
    buckets_pkey                │ 0 bytes
```

### Uso

```
supabase inspect db index-sizes
```

### Banderas

- **--db-url <string>**  
    _Opcional_  
    Inspecciona la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked**  
    _Opcional_  
    Inspecciona el proyecto vinculado.
    
- **--local**  
    _Opcional_  
    Inspecciona la base de datos local.