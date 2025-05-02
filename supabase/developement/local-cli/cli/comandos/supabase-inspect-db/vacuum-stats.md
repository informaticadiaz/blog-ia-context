## supabase inspect db vacuum-stats

Esto te muestra estadísticas sobre las actividades de vacío para cada tabla. Debido al [MVCC](https://www.postgresql.org/docs/current/mvcc.html) de Postgres, cuando los datos se actualizan o eliminan, se crean nuevas filas y las filas antiguas se vuelven invisibles y se marcan como "tuplas muertas". Normalmente, el proceso de [autovacuum](https://supabase.com/docs/guides/platform/database-size#vacuum-operations) limpiará asincrónicamente las tuplas muertas.

El comando muestra cuándo tuvo lugar el último vacío y el último auto vacío, el recuento de filas en la tabla, así como el recuento de filas muertas y si se espera que se ejecute el autovacuum o no. Si el número de filas muertas es mucho mayor que el recuento de filas, o si se espera un autovacuum pero no se ha realizado durante algún tiempo, esto puede indicar que el autovacuum no puede mantenerse al día y que tus configuraciones de vacío necesitan ser ajustadas o que requieres más potencia de cómputo o IOPS de disco para permitir que el autovacuum se complete.

```
        SCHEMA        │              TABLE               │ LAST VACUUM │ LAST AUTO VACUUM │      ROW COUNT       │ DEAD ROW COUNT │ EXPECT AUTOVACUUM?
──────────────────────┼──────────────────────────────────┼─────────────┼──────────────────┼──────────────────────┼────────────────┼─────────────────────
 auth                 │ users                            │             │ 2023-06-26 12:34 │               18,030 │              0 │ no
 public               │ profiles                         │             │ 2023-06-26 23:45 │               13,420 │             28 │ no
 public               │ logs                             │             │ 2023-06-26 01:23 │            1,313,033 │      3,318,228 │ yes
 storage              │ objects                          │             │                  │             No stats │              0 │ no
 storage              │ buckets                          │             │                  │             No stats │              0 │ no
 supabase_migrations  │ schema_migrations                │             │                  │             No stats │              0 │ no

```

### Uso

```
supabase inspect db vacuum-stats
```

### Banderas

- **--db-url <string>** _Opcional_
    
    Inspecciona la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Inspecciona el proyecto vinculado.
    
- **--local** _Opcional_
    
    Inspecciona la base de datos local.