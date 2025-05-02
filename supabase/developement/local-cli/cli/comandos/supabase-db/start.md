# supabase db start

## Descripción

Inicia la base de datos local de Supabase para desarrollo. Este comando permite iniciar únicamente el contenedor de la base de datos Postgres sin necesidad de iniciar todo el entorno de Supabase.

Es particularmente útil cuando necesitas trabajar solo con la base de datos, sin requerir otros servicios como Auth, Storage o Edge Functions. También puede utilizarse para iniciar una base de datos a partir de un archivo de copia de seguridad.

## Uso

```
supabase db start [banderas]
```

## Banderas

|Bandera|Descripción|
|---|---|
|`--from-backup <string>`|Ruta a un archivo de copia de seguridad lógica. Permite iniciar la base de datos restaurando los datos desde una copia de seguridad previamente creada.|

## Ejemplo de uso básico

```
supabase db start
```

## Restaurar desde copia de seguridad

```
supabase db start --from-backup ruta/a/archivo/backup.sql
```

## Notas adicionales

- Este comando es diferente de `supabase start`, que inicia todo el entorno de desarrollo local, incluyendo la base de datos, Auth, Storage, y otros servicios.
- Después de iniciar la base de datos, puedes conectarte a ella usando herramientas como `psql` o cualquier cliente de Postgres.
- La base de datos iniciada con este comando estará disponible en el puerto predeterminado (normalmente 54322 para el entorno local).
- La ejecución del comando aplicará automáticamente las migraciones ubicadas en el directorio `supabase/migrations`.