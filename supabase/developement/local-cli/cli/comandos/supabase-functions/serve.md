# supabase functions serve

Ejecuta todas las Funciones localmente.

El comando `supabase functions serve` incluye flags adicionales para ayudar a los desarrolladores a depurar Edge Functions a través del protocolo del inspector v8, permitiendo la depuración mediante Chrome DevTools, VS Code e IntelliJ IDEA, por ejemplo. Consulta la [guía de documentación](https://claude.ai/docs/guides/functions/debugging-tools) para obtener instrucciones de configuración.

1. `--inspect`
    
    - Alias de `--inspect-mode brk`.
2. `--inspect-mode [ run | brk | wait ]`
    
    - Activa la capacidad del inspector.
    - El modo `run` simplemente permite una conexión sin comportamiento adicional. No es ideal para scripts cortos, pero puede ser útil para scripts de larga duración donde ocasionalmente quieras establecer puntos de interrupción.
    - El modo `brk` es igual que el modo `run`, pero además establece un punto de interrupción en la primera línea para pausar la ejecución del script antes de que se ejecute cualquier código.
    - El modo `wait` es similar al modo `brk`, pero en lugar de establecer un punto de interrupción en la primera línea, pausa la ejecución del script hasta que se conecte una sesión de inspector.
3. `--inspect-main`
    
    - Solo se puede usar cuando uno de los dos flags anteriores está habilitado.
    - Por defecto, no se permite crear una sesión de inspector para el worker principal, pero este flag lo permite.
    - Otros comportamientos siguen el flag `inspect-mode` mencionado anteriormente.

Además, las siguientes propiedades se pueden personalizar a través de `supabase/config.toml` en la sección `edge_runtime`.

1. `inspector_port`
    
    - El puerto utilizado para escuchar la sesión del Inspector, por defecto es 8083.
2. `policy`
    
    - Un valor que indica cómo el edge-runtime debe reenviar las solicitudes HTTP entrantes al worker.
    - `per_worker` permite que varias solicitudes HTTP se reenvíen a un worker que ya ha sido creado.
    - `oneshot` forzará al worker a procesar una única solicitud HTTP y luego salir. (Propósito de depuración, esto es especialmente útil si quieres reflejar los cambios que has realizado inmediatamente).

## Uso

```
supabase functions serve [flags]
```

## Flags

- **--env-file <string>** _Opcional_
    
    Ruta a un archivo env que se poblará en el entorno de la Función.
    
- **--import-map <string>** _Opcional_
    
    Ruta al archivo de mapa de importación.
    
- **--inspect** _Opcional_
    
    Alias de --inspect-mode brk.
    
- **--inspect-main** _Opcional_
    
    Permite inspeccionar el worker principal.
    
- **--inspect-mode <[ run | brk | wait ]>** _Opcional_
    
    Activa la capacidad del inspector para depuración.
    
- **--no-verify-jwt** _Opcional_
    
    Deshabilita la verificación JWT para la Función.