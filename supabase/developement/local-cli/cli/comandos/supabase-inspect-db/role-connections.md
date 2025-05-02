## supabase inspect db role-connections

Este comando muestra el número de conexiones activas para cada rol de base de datos para ver qué rol específico podría estar consumiendo más conexiones de lo esperado.

Este es un comando específico de Supabase. También puedes ver este desglose en el panel de control: https://app.supabase.com/project/_/database/roles

El número máximo de conexiones activas depende [del tamaño de tu instancia](https://supabase.com/docs/guides/platform/compute-add-ons). Puedes [sobrescribir manualmente](https://supabase.com/docs/guides/platform/performance#allowing-higher-number-of-connections) el número permitido de conexiones, pero no es recomendable.

```

            ROLE NAME         │ ACTIVE CONNCTION
  ────────────────────────────┼───────────────────
    authenticator             │                5
    postgres                  │                5
    supabase_admin            │                1
    pgbouncer                 │                1
    anon                      │                0
    authenticated             │                0
    service_role              │                0
    dashboard_user            │                0
    supabase_auth_admin       │                0
    supabase_storage_admin    │                0
    supabase_functions_admin  │                0
    pgsodium_keyholder        │                0
    pg_read_all_data          │                0
    pg_write_all_data         │                0
    pg_monitor                │                0

Active connections 12/90

```

### Uso

```
supabase inspect db role-connections
```

### Banderas

- **--db-url <string>** _Opcional_
    
    Inspecciona la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Inspecciona el proyecto vinculado.
    
- **--local** _Opcional_
    
    Inspecciona la base de datos local.