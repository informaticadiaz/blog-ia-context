# supabase functions deploy

Despliega una Función al proyecto Supabase vinculado.

## Uso

```
supabase functions deploy [Nombre de la función] [flags]
```

## Flags

- **--import-map <string>** _Opcional_
    
    Ruta al archivo de mapa de importación.
    
- **-j, --jobs <uint>** _Opcional_
    
    Número máximo de trabajos en paralelo.
    
- **--no-verify-jwt** _Opcional_
    
    Deshabilita la verificación JWT para la Función.
    
- **--project-ref <string>** _Opcional_
    
    Referencia del proyecto de Supabase.
    
- **--use-api** _Opcional_
    
    Usa la API de Gestión para empaquetar funciones.
    
- **--use-docker** _Opcional_
    
    Usa Docker para empaquetar funciones.