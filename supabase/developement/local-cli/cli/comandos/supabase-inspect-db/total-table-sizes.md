## supabase inspect db total-table-sizes

Este comando muestra el tamaño total de cada tabla en la base de datos. Es la suma de los valores que `pg_table_size()` y `pg_indexes_size()` proporcionan para cada tabla. Las tablas del sistema dentro de `pg_catalog` e `information_schema` no están incluidas.

```
                NAME               │    SIZE
───────────────────────────────────┼─────────────
  job_run_details                  │ 395 MB
  slack_msgs                       │ 648 kB
  emails                           │ 640 kB
```

### Uso

```
supabase inspect db total-table-sizes
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