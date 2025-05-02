## supabase inspect db blocking

Este comando te muestra las declaraciones que actualmente están manteniendo bloqueos y bloqueando, así como la declaración que está siendo bloqueada. Esto puede usarse junto con `inspect db locks` para determinar qué declaraciones necesitan ser terminadas para resolver la contención de bloqueos.

```
    BLOCKED PID │ BLOCKING STATEMENT           │ BLOCKING DURATION │ BLOCKING PID │ BLOCKED STATEMENT                                                                      │ BLOCKED DURATION
  ──────────────┼──────────────────────────────┼───────────────────┼──────────────┼────────────────────────────────────────────────────────────────────────────────────────┼───────────────────
    253         │ select count(*) from mytable │ 00:00:03.838314   │        13495 │ UPDATE "mytable" SET "updated_at" = '2023─08─03 14:07:04.746688' WHERE "id" = 83719341 │ 00:00:03.821826
```

### Uso

```
supabase inspect db blocking
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