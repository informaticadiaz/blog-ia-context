## supabase inspect db long-running-queries

Este comando muestra las consultas actualmente en ejecución que han estado funcionando durante más de 5 minutos, ordenadas de forma descendente por duración. Las consultas de muy larga duración pueden ser una fuente de múltiples problemas, como impedir que se completen las declaraciones DDL o que vacuum no pueda actualizar `relfrozenxid`.

```
  PID  │     DURATION    │                                         QUERY
───────┼─────────────────┼───────────────────────────────────────────────────────────────────────────────────────
 19578 | 02:29:11.200129 | EXPLAIN SELECT  "students".* FROM "students"  WHERE "students"."id" = 1450645 LIMIT 1
 19465 | 02:26:05.542653 | EXPLAIN SELECT  "students".* FROM "students"  WHERE "students"."id" = 1889881 LIMIT 1
 19632 | 02:24:46.962818 | EXPLAIN SELECT  "students".* FROM "students"  WHERE "students"."id" = 1581884 LIMIT 1
```

### Uso

```
supabase inspect db long-running-queries
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