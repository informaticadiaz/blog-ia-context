## supabase inspect db calls

Este comando es muy parecido al comando `supabase inspect db outliers`, pero ordenado por el número de veces que se ha llamado a una sentencia.

Puede usar esta información para ver qué consultas se llaman con más frecuencia, lo que potencialmente puede ser bueno para su optimización.

```
                        QUERY                      │ TOTAL EXECUTION TIME │ PROPORTION OF TOTAL EXEC TIME │ NUMBER CALLS │  SYNC IO TIME
  ─────────────────────────────────────────────────┼──────────────────────┼───────────────────────────────┼──────────────┼──────────────────
    SELECT * FROM users WHERE id = $1              │ 14:50:11.828939      │ 89.8%                         │  183,389,757 │ 00:00:00.002018
    SELECT * FROM user_events                      │ 01:20:23.466633      │ 1.4%                          │       78,325 │ 00:00:00
    INSERT INTO users (email, name) VALUES ($1, $2)│ 00:40:11.616882      │ 0.8%                          │       54,003 │ 00:00:00.000322
```

### Uso

```
supabase inspect db calls
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