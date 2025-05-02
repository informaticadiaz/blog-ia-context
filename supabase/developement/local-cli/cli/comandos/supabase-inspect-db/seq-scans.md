## supabase inspect db seq-scans

Este comando muestra el número de escaneos secuenciales registrados en todas las tablas, ordenados de forma descendente por cantidad de escaneos secuenciales. Las tablas que tienen un número muy alto de escaneos secuenciales pueden tener pocos índices, y puede valer la pena investigar las consultas que leen de estas tablas.

```
                  NAME               │ COUNT
  ───────────────────────────────────┼─────────
    emails                           │ 182435
    users                            │  25063
    job_run_details                  │     60
    schema_migrations                │      0
    migrations                       │      0
```

### Uso

```
supabase inspect db seq-scans
```

### Banderas

- **--db-url <string>** _Opcional_
    
    Inspecciona la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Inspecciona el proyecto vinculado.
    
- **--local** _Opcional_
    
    Inspecciona la base de datos local.