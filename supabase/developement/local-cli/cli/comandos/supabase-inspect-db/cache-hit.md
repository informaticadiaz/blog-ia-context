## supabase inspect db cache-hit

Este comando proporciona información sobre la eficiencia del búfer de caché y con qué frecuencia tus consultas deben acceder al disco en lugar de leer desde la memoria. Se muestra información tanto sobre lecturas de índice (`index hit rate`) como lecturas de tabla (`table hit rate`). En general, las bases de datos con tasas bajas de aciertos de caché tienen peor rendimiento ya que es más lento acceder al disco que recuperar datos de la memoria. Si tu tasa de aciertos de tabla es baja, esto puede indicar que no tienes suficiente RAM y podrías beneficiarte de actualizar a un complemento de cómputo más grande con más memoria. Si tu tasa de aciertos de índice es baja, esto puede indicar que hay margen para agregar índices más apropiados.

Las tasas de aciertos se calculan como la proporción entre el número de bloques de tabla o índice recuperados del búfer de caché de postgres y la suma de bloques en caché y bloques sin caché leídos desde el disco.

En planes de cómputo más pequeños (gratuito, pequeño, mediano), una proporción inferior al 99% puede indicar un problema. En planes más grandes, las tasas de aciertos pueden ser más bajas, pero el rendimiento se mantendrá constante ya que los datos pueden utilizar la caché del sistema operativo en lugar del búfer de caché de Postgres.

```
         NAME      │  RATIO
  ─────────────────┼───────────
    index hit rate │ 0.996621
    table hit rate │ 0.999341
```

### Uso

```
supabase inspect db cache-hit
```

### Banderas

- **--db-url <string>** _Opcional_
    
    Inspecciona la base de datos especificada por la cadena de conexión (debe estar codificada por porcentaje).
    
- **--linked** _Opcional_
    
    Inspecciona el proyecto vinculado.
    
- **--local** _Opcional_
    
    Inspecciona la base de datos local.