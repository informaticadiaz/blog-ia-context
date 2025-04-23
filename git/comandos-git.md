# Comandos comunes para trabajar con repositorios de GitHub

1.   Añade cambios de un archivo específico al área de preparación (staging).

```bash
git add [archivo]
```

2.  Añade todos los cambios de archivos al área de preparación.

```bash
git add .
```

3. Guarda los cambios en el historial del repositorio con un mensaje descriptivo.

```bash
git commit -m "[mensaje]"
```

4. Muestra el estado actual del repositorio, archivos modificados y preparados.

```bash
git status
```

5. Envía los commits locales a la rama especificada en el repositorio remoto.

```bash
git push origin [rama]
```

6.  Obtiene y fusiona los cambios del repositorio remoto a tu copia local.

```bash
git pull origin [rama]
```

7.  Lista todas las ramas locales del repositorio.

```bash
git branch
```

8. Crea una nueva rama con el nombre especificado.

```bash
git branch [nombre-rama]
```

9. Cambia a la rama especificada.

```bash
git checkout [rama]
```

10. Crea una nueva rama y cambia a ella en un solo comando.

```bash
git checkout -b [rama]
```

11. Fusiona la rama especificada con la rama actual.

```bash
git merge [rama]
```

12. `git remote add origin [url]` - Conecta tu repositorio local con un repositorio remoto en GitHub.


13. `git log` - Muestra el historial de commits del repositorio.

14. `git diff` - Muestra las diferencias entre los archivos modificados y la última versión guardada.

15. `git reset [archivo]` - Quita un archivo del área de preparación sin descartar los cambios.

16. `git reset --hard` - Descarta todos los cambios y vuelve al último commit.

17. `git fetch` - Descarga el contenido del repositorio remoto sin fusionarlo con tu copia local.

18. `git stash` - Guarda temporalmente cambios que no están listos para ser confirmados.
