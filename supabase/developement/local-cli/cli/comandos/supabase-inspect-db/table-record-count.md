## supabase inspect db table-record-counts

Este comando muestra un recuento estimado de filas por tabla, ordenado descendentemente por el conteo estimado. El conteo estimado se deriva de `n_live_tup`, que se actualiza mediante operaciones de vacuum. Debido a la forma en que `n_live_tup` se completa, las páginas dispersas frente a las densas pueden resultar en estimaciones significativamente alejadas del recuento real de filas.

```
       NAME    │ ESTIMATED COUNT
  ─────────────┼──────────────────
    logs       │          322943
    emails     │            1103
    job        │               1
    migrations │               0
```

### Uso

```
supabase inspect db table-record-counts
```

### Banderas

- **--db-url <string>** _Opcional_
    
    Inspecciona la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Inspecciona el proyecto vinculado.
    
- **--local** _Opcional_
    
    Inspecciona la base de datos local.