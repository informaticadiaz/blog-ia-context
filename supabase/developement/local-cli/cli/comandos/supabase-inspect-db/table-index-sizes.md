## supabase inspect db table-index-sizes

Este comando muestra el tamaño total de los índices para cada tabla. Se calcula utilizando la función de administración del sistema `pg_indexes_size()`.

```
                 TABLE               │ INDEX SIZE
  ───────────────────────────────────┼─────────────
    job_run_details                  │ 10104 kB
    users                            │ 128 kB
    job                              │ 32 kB
    instances                        │ 8192 bytes
    http_request_queue               │ 0 bytes
```

### Uso

```
supabase inspect db table-index-sizes
```

### Banderas

- **--db-url <string>** _Opcional_
    
    Inspecciona la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Inspecciona el proyecto vinculado.
    
- **--local** _Opcional_
    
    Inspecciona la base de datos local.