# Supabase DB

Esta guía proporciona una referencia completa de los comandos `supabase db` disponibles en la CLI de Supabase. Estos comandos te permiten gestionar y manipular bases de datos de Supabase tanto locales como remotas.

## Índice de Comandos

1. [supabase db diff](https://claude.ai/chat/96883b00-9d83-4c15-962a-1bc609081f18#supabase-db-diff) - Compara los cambios de esquema entre bases de datos
2. [supabase db dump](https://claude.ai/chat/96883b00-9d83-4c15-962a-1bc609081f18#supabase-db-dump) - Vuelca (exporta) contenidos desde una base de datos
3. [supabase db lint](https://claude.ai/chat/96883b00-9d83-4c15-962a-1bc609081f18#supabase-db-lint) - Analiza esquemas de base de datos en busca de errores
4. [supabase db pull](https://claude.ai/chat/96883b00-9d83-4c15-962a-1bc609081f18#supabase-db-pull) - Extrae cambios de esquema desde una base de datos remota
5. [supabase db push](https://claude.ai/chat/96883b00-9d83-4c15-962a-1bc609081f18#supabase-db-push) - Envía migraciones locales a una base de datos remota
6. [supabase db reset](https://claude.ai/chat/96883b00-9d83-4c15-962a-1bc609081f18#supabase-db-reset) - Restablece una base de datos a un estado limpio
7. [supabase db start](https://claude.ai/chat/96883b00-9d83-4c15-962a-1bc609081f18#supabase-db-start) - Inicia la base de datos local

## Descripción de los Comandos

### supabase db diff

Compara los cambios de esquema realizados en la base de datos local o remota. Útil para identificar diferencias antes de hacer migraciones.

**Uso básico:**

```bash
supabase db diff -f nombre_migracion
```

[Ver documentación completa](https://claude.ai/chat/supabase-db-diff.md)

### supabase db dump

Vuelca (exporta) contenidos desde una base de datos remota. Permite exportar esquemas, datos y roles para crear copias de seguridad o migrar datos.

**Uso básico:**

```bash
supabase db dump -f supabase/schema.sql
```

[Ver documentación completa](https://claude.ai/chat/supabase-db-dump.md)

### supabase db lint

Analiza la base de datos local en busca de errores de esquema. Útil para detectar problemas antes de implementar en producción.

**Uso básico:**

```bash
supabase db lint
```

[Ver documentación completa](https://claude.ai/chat/supabase-db-lint.md)

### supabase db pull

Extrae cambios de esquema desde una base de datos remota. Crea un nuevo archivo de migración con los cambios detectados.

**Uso básico:**

```bash
supabase db pull
```

[Ver documentación completa](https://claude.ai/chat/supabase-db-pull.md)

### supabase db push

Envía todas las migraciones locales a una base de datos remota. Aplica los cambios de esquema en el servidor.

**Uso básico:**

```bash
supabase db push
```

[Ver documentación completa](https://claude.ai/chat/supabase-db-push.md)

### supabase db reset

Restablece la base de datos local a un estado limpio. Recrea el contenedor de Postgres y aplica todas las migraciones locales.

**Uso básico:**

```bash
supabase db reset
```

[Ver documentación completa](https://claude.ai/chat/supabase-db-reset.md)

### supabase db start

Inicia la base de datos local de Supabase para desarrollo. Permite iniciar solo el contenedor de la base de datos Postgres sin necesidad de iniciar todo el entorno de Supabase.

**Uso básico:**

```bash
supabase db start
```

**Restaurar desde copia de seguridad:**

```bash
supabase db start --from-backup ruta/a/archivo/backup.sql
```

[Ver documentación completa](https://claude.ai/chat/supabase-db-start.md)

## Flujos de Trabajo Comunes

### Desarrollo Local

1. Inicia el entorno local: `supabase start`
2. Realiza cambios en la base de datos local
3. Genera un archivo de migración: `supabase db diff -f nombre_migracion`
4. Prueba la migración: `supabase db reset`

### Sincronización con Proyecto Remoto

1. Vincula tu proyecto local: `supabase link --project-ref tu-ref-proyecto`
2. Extrae cambios remotos: `supabase db pull`
3. Desarrolla localmente y crea migraciones
4. Envía cambios al proyecto remoto: `supabase db push`

### Migración de Bases de Datos

1. Exporta el esquema de la base de datos de origen: `supabase db dump -f origen.sql`
2. Crea un nuevo proyecto Supabase
3. Importa el esquema: `psql -f origen.sql postgres://...`
4. Verifica la integridad: `supabase db lint --linked`

## Mejores Prácticas

- Usa siempre migraciones versionadas para rastrear cambios en el esquema
- Realiza `db lint` antes de implementar para detectar posibles problemas
- Mantén las migraciones idempotentes (pueden ejecutarse varias veces sin efectos secundarios)
- Divide migraciones complejas en pasos más pequeños y manejables
- Haz copias de seguridad antes de realizar migraciones importantes