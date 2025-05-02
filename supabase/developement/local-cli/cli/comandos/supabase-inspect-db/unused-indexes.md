## supabase inspect db unused-indexes

Este comando muestra los índices que tienen menos de 50 escaneos registrados contra ellos, y tienen un tamaño mayor a 5 páginas, ordenados por tamaño en relación con el número de escaneos de índice. Este comando es generalmente útil para descubrir índices que no se utilizan. Los índices pueden afectar el rendimiento de escritura, así como el rendimiento de lectura si ocupan espacio en memoria, es una buena idea eliminar los índices que no son necesarios o no se están utilizando.

```
        TABLE        │                   INDEX                    │ INDEX SIZE │ INDEX SCANS
─────────────────────┼────────────────────────────────────────────┼────────────┼──────────────
 public.users        │ user_id_created_at_idx                     │ 97 MB      │           0
```

### Uso

```
supabase inspect db unused-indexes
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