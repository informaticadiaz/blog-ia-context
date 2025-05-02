## supabase inspect db outliers

Este comando muestra las declaraciones, obtenidas de `pg_stat_statements`, ordenadas por la cantidad de tiempo para ejecutar en conjunto. Esto incluye la declaración en sí, el tiempo total de ejecución para esa declaración, la proporción del tiempo total de ejecución para todas las declaraciones que ha ocupado esa declaración, el número de veces que se ha llamado a esa declaración y la cantidad de tiempo que esa declaración ha dedicado a E/S sincrónica (lectura/escritura desde el sistema de archivos).

Normalmente, una consulta eficiente tendrá una proporción adecuada de llamadas al tiempo total de ejecución, con el menor tiempo posible dedicado a E/S. Las consultas que tienen un alto tiempo total de ejecución pero un bajo recuento de llamadas deben investigarse para mejorar su rendimiento. También deben investigarse las consultas que tienen una alta proporción de tiempo de ejecución dedicado a E/S sincrónica.

```
                 QUERY                   │ EXECUTION TIME   │ PROPORTION OF EXEC TIME │ NUMBER CALLS │ SYNC IO TIME
─────────────────────────────────────────┼──────────────────┼─────────────────────────┼──────────────┼───────────────
 SELECT * FROM archivable_usage_events.. │ 154:39:26.431466 │ 72.2%                   │ 34,211,877   │ 00:00:00
 COPY public.archivable_usage_events (.. │ 50:38:33.198418  │ 23.6%                   │ 13           │ 13:34:21.00108
 COPY public.usage_events (id, reporte.. │ 02:32:16.335233  │ 1.2%                    │ 13           │ 00:34:19.784318
 INSERT INTO usage_events (id, retaine.. │ 01:42:59.436532  │ 0.8%                    │ 12,328,187   │ 00:00:00
 SELECT * FROM usage_events WHERE (alp.. │ 01:18:10.754354  │ 0.6%                    │ 102,114,301  │ 00:00:00
```

### Uso

```
supabase inspect db outliers
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