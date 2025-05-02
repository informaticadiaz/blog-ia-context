# supabase migration repair

Repara la tabla de historial de migraciones remotas.

Requiere que tu proyecto local esté vinculado a una base de datos remota ejecutando `supabase link`.

Si tu historial de migración local y remoto se desincroniza, puedes reparar el historial remoto marcando migraciones específicas como `--status applied` o `--status reverted`. Marcar como `reverted` eliminará un registro existente de la tabla de historial de migración, mientras que marcar como `applied` insertará un nuevo registro.

Por ejemplo, tu historial de migración puede verse como la tabla a continuación, con entradas faltantes en el local o remoto.

```bash
$ supabase migration list
        LOCAL      │     REMOTE     │     TIME (UTC)
  ─────────────────┼────────────────┼──────────────────────
                   │ 20230103054303 │ 2023-01-03 05:43:03
   20230103054315  │                │ 2023-01-03 05:43:15
```

Para restablecer tu historial de migración a un estado limpio, primero elimina tu archivo de migración local.

```bash
$ rm supabase/migrations/20230103054315_remote_commit.sql

$ supabase migration list
        LOCAL      │     REMOTE     │     TIME (UTC)
  ─────────────────┼────────────────┼──────────────────────
                   │ 20230103054303 │ 2023-01-03 05:43:03
```

Luego marca la migración remota `20230103054303` como revertida.

```bash
$ supabase migration repair 20230103054303 --status reverted
Connecting to remote database...
Repaired migration history: [20220810154537] => reverted
Finished supabase migration repair.

$ supabase migration list
        LOCAL      │     REMOTE     │     TIME (UTC)
  ─────────────────┼────────────────┼──────────────────────
```

Ahora puedes ejecutar `db pull` nuevamente para volcar el esquema remoto como un archivo de migración local.

```bash
$ supabase db pull
Connecting to remote database...
Schema written to supabase/migrations/20240414044403_remote_schema.sql
Update remote migration history table? [Y/n]
Repaired migration history: [20240414044403] => applied
Finished supabase db pull.

$ supabase migration list
        LOCAL      │     REMOTE     │     TIME (UTC)
  ─────────────────┼────────────────┼──────────────────────
    20240414044403 │ 20240414044403 │ 2024-04-14 04:44:03
```

## Uso

```
supabase migration repair [version] ... [flags]
```

## Banderas

- **--db-url <string>** _Opcional_
    
    Repara las migraciones de la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Repara el historial de migración del proyecto vinculado.
    
- **--local** _Opcional_
    
    Repara el historial de migración de la base de datos local.
    
- **-p, --password <string>** _Opcional_
    
    Contraseña para tu base de datos Postgres remota.
    
- **--status <[ applied | reverted ]>** _Requerido_
    
    Estado de versión a actualizar.
    

## Ejemplo: Marcar una migración como revertida

```
supabase migration repair 20230103054303 --status reverted
```

### Respuesta

```
Repaired migration history: 20230103054303 => reverted
```