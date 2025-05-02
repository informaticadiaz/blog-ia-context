# supabase db lint

## Descripción

Analiza la base de datos local en busca de errores de esquema.

Requiere que el entorno de desarrollo local esté en ejecución cuando se realiza el análisis contra la base de datos local. Para analizar una base de datos remota o autoalojada, especifica la bandera `--linked` o `--db-url` respectivamente.

Ejecuta la extensión `plpgsql_check` en el contenedor local de Postgres para verificar errores en todos los esquemas. El nivel de análisis predeterminado es `warning` (advertencia) y puede elevarse a error mediante la bandera `--level`.

Para analizar solo esquemas específicos, utiliza la bandera `--schema`.

La bandera `--fail-on` puede usarse para controlar cuándo el comando debe salir con un código de estado distinto de cero. Los valores posibles son:

- `none` (predeterminado): Siempre sale con un código de estado cero, independientemente de los resultados del análisis.
- `warning`: Sale con un código de estado distinto de cero si se encuentran advertencias o errores.
- `error`: Sale con un código de estado distinto de cero solo si se encuentran errores.

Esta bandera es particularmente útil en tuberías de CI/CD donde quieres que la compilación falle según ciertas condiciones de análisis.

## Uso

```
supabase db lint [banderas]
```

## Banderas

|Bandera|Descripción|
|---|---|
|`--db-url <string>`|Analiza la base de datos especificada por la cadena de conexión (debe estar codificada en porcentaje).|
|`--fail-on <[ none \| warning \| error ]>`|Nivel de error para salir con estado distinto de cero.|
|`--level <[ warning \| error ]>`|Nivel de error a emitir.|
|`--linked`|Analiza el proyecto vinculado en busca de errores de esquema.|
|`--local`|Analiza la base de datos local en busca de errores de esquema.|
|`-s, --schema <strings>`|Lista separada por comas de esquemas a incluir.|

## Ejemplo de uso básico

```
supabase db lint
```

### Respuesta

```
Linting schema: public

No schema errors found
```