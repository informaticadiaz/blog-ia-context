## supabase inspect db table-sizes

Este comando muestra el tamaño de cada tabla en la base de datos. Se calcula utilizando la función de administración del sistema `pg_table_size()`, que incluye el tamaño de la bifurcación principal de datos, el mapa de espacio libre, el mapa de visibilidad y los datos TOAST. No incluye el tamaño de los índices de la tabla.

```
                  NAME               │    SIZE
  ───────────────────────────────────┼─────────────
    job_run_details                  │ 385 MB
    emails                           │ 584 kB
    job                              │ 40 kB
    sessions                         │ 0 bytes
    prod_resource_notifications_meta │ 0 bytes
```

### Uso

```
supabase inspect db table-sizes
```

### Banderas

- **--db-url <string>** _Opcional_
    
    Inspecciona la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Inspecciona el proyecto vinculado.
    
- **--local** _Opcional_
    
    Inspecciona la base de datos local.