# supabase login

Conecta la CLI de Supabase con tu cuenta de Supabase iniciando sesión con tu [token de acceso personal](https://supabase.com/dashboard/account/tokens).

Tu token de acceso se almacena de forma segura en el [almacenamiento nativo de credenciales](https://github.com/zalando/go-keyring#dependencies). Si el almacenamiento nativo de credenciales no está disponible, se escribirá en un archivo de texto plano en `~/.supabase/access-token`.

> Si este comportamiento no es deseable, como en un entorno de CI, puedes omitir el inicio de sesión especificando la variable de entorno `SUPABASE_ACCESS_TOKEN` en otros comandos.

La CLI de Supabase utiliza el token almacenado para acceder a las APIs de Administración para proyectos, funciones, secretos, etc.

## Uso

```
supabase login [flags]
```

## Banderas

|Bandera|Opcional|Descripción|
|---|---|---|
|`--name <string>`|Opcional|Nombre que se utilizará para almacenar el token en tu configuración|
|`--no-browser`|Opcional|No abrir el navegador automáticamente|
|`--token <string>`|Opcional|Usar el token proporcionado en lugar del flujo de inicio de sesión automático|

## Ejemplos

### Uso básico

```
supabase login
```

Respuesta:

```
You can generate an access token from https://supabase.com/dashboard/account/tokens
Enter your access token: sbp_****************************************
Finished supabase login.
```