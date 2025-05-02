## supabase inspect db bloat

Este comando muestra una estimación del "bloat" (hinchazón) de tabla - Debido al [MVCC](https://www.postgresql.org/docs/current/mvcc.html) de Postgres, cuando los datos se actualizan o eliminan, se crean nuevas filas y las filas antiguas se vuelven invisibles y se marcan como "tuplas muertas". Normalmente, el proceso de [autovacuum](https://supabase.com/docs/guides/platform/database-size#vacuum-operations) limpiará asincrónicamente las tuplas muertas. A veces, el autovacuum no puede trabajar lo suficientemente rápido para reducir o prevenir que las tablas se hinchen. Un alto nivel de hinchazón puede ralentizar las consultas, causar IOPS excesivas y desperdiciar espacio en tu base de datos.

Las tablas con una alta proporción de hinchazón deberían ser investigadas para ver si el proceso de aspirado no es lo suficientemente rápido o si hay otros problemas.

```
    TYPE  │ SCHEMA NAME │        OBJECT NAME         │ BLOAT │ WASTE
  ────────┼─────────────┼────────────────────────────┼───────┼─────────────
    table │ public      │ very_bloated_table         │  41.0 │ 700 MB
    table │ public      │ my_table                   │   4.0 │ 76 MB
    table │ public      │ happy_table                │   1.0 │ 1472 kB
    index │ public      │ happy_table::my_nice_index │   0.7 │ 880 kB
```

### Uso

```
supabase inspect db bloat
```

### Banderas

- **--db-url <string>** _Opcional_
    
    Inspecciona la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Inspecciona el proyecto vinculado.
    
- **--local** _Opcional_
    
    Inspecciona la base de datos local.