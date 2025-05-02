## supabase inspect db total-index-size

Este comando muestra el tamaño total de todos los índices en la base de datos. Se calcula tomando el número de páginas (reportado en `relpages`) y multiplicándolo por el tamaño de página (8192 bytes).

```
    SIZE
  ─────────
    12 MB
```

### Uso

```
supabase inspect db total-index-size
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