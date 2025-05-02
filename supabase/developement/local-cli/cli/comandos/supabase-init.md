# supabase init

Inicializa configuraciones para el desarrollo local de Supabase.

Un archivo `supabase/config.toml` es creado en tu directorio de trabajo actual. Esta configuración es específica para cada proyecto local.

> Puedes sobreescribir la ruta del directorio especificando la variable de entorno `SUPABASE_WORKDIR` o la bandera `--workdir`.

Además de `config.toml`, el directorio `supabase` también puede contener otros objetos de Supabase, como `migrations`, `functions`, `tests`, etc.

## Uso

```
supabase init [flags]
```

## Banderas

|Bandera|Opcional|Descripción|
|---|---|---|
|`--force`|Opcional|Sobreescribir el archivo supabase/config.toml existente.|
|`--use-orioledb`|Opcional|Usar el motor de almacenamiento OrioleDB para Postgres.|
|`--with-intellij-settings`|Opcional|Generar configuraciones para IntelliJ IDEA para Deno.|
|`--with-vscode-settings`|Opcional|Generar configuraciones para VS Code para Deno.|

## Ejemplos

### Uso básico

```
supabase init
```

Respuesta:

```
Finished supabase init.
```

### Inicializar desde un directorio existente

También es posible inicializar Supabase desde un directorio existente (esta opción estaba disponible en la interfaz pero no se mostraban detalles).