# supabase test db

Ejecuta pruebas pgTAP contra la base de datos local.

Requiere que el stack de desarrollo local esté iniciado mediante la ejecución de `supabase start`.

Ejecuta `pg_prove` en un contenedor con archivos de prueba unitaria montados desde el directorio `supabase/tests`. El archivo de prueba puede tener la extensión `.sql` o `.pg`.

Dado que cada prueba está envuelta en su propia transacción, se revertirá individualmente independientemente de si tiene éxito o falla.

## Uso

```
supabase test db [path] ... [flags]
```

## Flags

### --db-url <string>

_Opcional_

Prueba la base de datos especificada por la cadena de conexión (debe estar codificada con porcentaje).

### --linked

_Opcional_

Ejecuta pruebas pgTAP en el proyecto vinculado.

### --local

_Opcional_

Ejecuta pruebas pgTAP en la base de datos local.

## Uso básico

```
supabase test db
```

### Respuesta

```
/tmp/supabase/tests/nested/order_test.pg .. ok
/tmp/supabase/tests/pet_test.sql .......... ok
All tests successful.
Files=2, Tests=2,  6 wallclock secs ( 0.03 usr  0.01 sys +  0.05 cusr  0.02 csys =  0.11 CPU)
Result: PASS
```