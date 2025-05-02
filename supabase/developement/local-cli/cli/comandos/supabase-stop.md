# supabase stop

## Descripción

Detiene el stack de desarrollo local de Supabase.

Requiere que el archivo `supabase/config.toml` haya sido creado en tu directorio de trabajo actual mediante la ejecución de `supabase init`.

Todos los recursos de Docker se mantienen entre reinicios. Usa la bandera `--no-backup` para reiniciar tus datos de desarrollo local entre reinicios.

Usa la bandera `--all` para detener todas las instancias locales de proyectos Supabase en la máquina. Utiliza con precaución la opción `--no-backup` ya que eliminará todos los datos de los proyectos locales de Supabase.

## Uso

```
supabase stop [flags]
```

## Opciones

|Opción|Descripción|
|---|---|
|`--all`|Detiene todas las instancias locales de Supabase de todos los proyectos en la máquina. (Opcional)|
|`--no-backup`|Elimina todos los volúmenes de datos después de detener. (Opcional)|
|`--project-id <string>`|ID del proyecto local a detener. (Opcional)|

## Ejemplos

### Uso básico

```
supabase stop
```

**Respuesta:**

```
Stopped supabase local development setup.
Local data are backed up to docker volume.
```

### Limpiar datos locales después de detener

Si quieres eliminar todos los datos locales al detener Supabase, puedes usar:

```
supabase stop --no-backup
```

Esto detendrá el stack de desarrollo local y eliminará todos los volúmenes de datos, lo que efectivamente reiniciará tu base de datos local la próxima vez que inicies Supabase.

### Detener todas las instancias de Supabase

Para detener todas las instancias locales de Supabase en tu máquina:

```
supabase stop --all
```

### Detener todas las instancias y eliminar todos los datos

Para detener todas las instancias locales de Supabase y eliminar todos los datos:

```
supabase stop --all --no-backup
```

Ten precaución al usar esta opción, ya que eliminará todos los datos de todos los proyectos locales de Supabase.