## supabase inspect db replication-slots

Este comando muestra información sobre los [slots de replicación lógica](https://www.postgresql.org/docs/current/logical-replication.html) que están configurados en la base de datos. Muestra si el slot está activo, el estado del proceso emisor de WAL ('startup', 'catchup', 'streaming', 'backup', 'stopping'), la dirección del cliente de replicación y el retraso de replicación en GB.

Este comando es útil para verificar que la cantidad de retraso de replicación sea lo más baja posible. El retraso de replicación puede ocurrir debido a problemas de latencia de red, E/S de disco lenta, transacciones de larga duración o falta de capacidad del suscriptor para consumir WAL lo suficientemente rápido.

```
                       NAME                    │ ACTIVE │ STATE   │ REPLICATION CLIENT ADDRESS │ REPLICATION LAG GB
  ─────────────────────────────────────────────┼────────┼─────────┼────────────────────────────┼─────────────────────
    supabase_realtime_replication_slot         │ t      │ N/A     │ N/A                        │                  0
    datastream                                 │ t      │ catchup │ 24.201.24.106              │                 45
```

### Uso

```
supabase inspect db replication-slots
```

### Banderas

- **--db-url <string>** _Opcional_
    
    Inspecciona la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Inspecciona el proyecto vinculado.
    
- **--local** _Opcional_
    
    Inspecciona la base de datos local.