# README de la clase de Git y github inicial

## Comandos iniciales de Git

### Configuración inicial
```bash
# Configurar nombre de usuario
git config --global user.name "Tu Nombre"

# Configurar email
git config --global user.email "tu@email.com"

# Ver la configuración
git config --list
```

### Inicializar un repositorio
```bash
# Inicializar un nuevo repositorio Git
git init
```

### Área de trabajo (Working Directory)
```bash
# Ver el estado de los archivos
git status

# Ver diferencias en archivos modificados
git diff
```

### Añadir archivos al área de preparación (Staging Area)
```bash
# Añadir un archivo específico
git add nombre_archivo.txt

# Añadir todos los archivos modificados
git add .

# Añadir todos los archivos con una extensión específica
git add *.txt
```

### Crear commits
```bash
# Crear un commit con mensaje
git commit -m "Mensaje descriptivo del commit"

# Añadir y hacer commit en un solo paso (solo para archivos ya rastreados)
git commit -am "Mensaje del commit"

# Ver el historial de commits
git log

# Ver el historial de commits en una línea

# Ver el historial con gráfico
git log --oneline --graph

## Manejo de Ramas (Branches)

### ¿Qué son las ramas?
Las ramas en Git permiten trabajar en diferentes versiones del proyecto de forma paralela. La rama principal suele llamarse `main` o `master`.

### Comandos básicos de ramas
```bash
# Ver todas las ramas locales
git branch

# Ver todas las ramas (locales y remotas)
git branch -a

# Crear una nueva rama
git branch nombre-rama

# Cambiar a una rama existente
git checkout nombre-rama

# Crear y cambiar a una nueva rama en un solo comando
git checkout -b nombre-rama

# Alternativa moderna para cambiar de rama
git switch nombre-rama

# Crear y cambiar a una nueva rama (alternativa moderna)
git switch -c nombre-rama
```

### Fusionar ramas (Merge)
```bash
# Fusionar una rama en la rama actual
git merge nombre-rama

# Fusionar sin fast-forward (crea un commit de merge)
git merge --no-ff nombre-rama

# Abortar un merge en caso de conflictos
git merge --abort
```

### Eliminar ramas
```bash
# Eliminar una rama local (solo si ya fue fusionada)
git branch -d nombre-rama

# Forzar eliminación de una rama local
git branch -D nombre-rama

# Eliminar una rama remota
git push origin --delete nombre-rama
```

### Renombrar ramas
```bash
# Renombrar la rama actual
git branch -m nuevo-nombre

# Renombrar una rama específica
git branch -m nombre-viejo nombre-nuevo
```

### Ver diferencias entre ramas
```bash
# Ver diferencias entre dos ramas
git diff rama1..rama2

# Ver commits que están en una rama pero no en otra
git log rama1..rama2

# Ver el historial de todas las ramas con gráfico
git log --oneline --graph --all
```

### Rebase (alternativa a merge)
```bash
# Aplicar commits de la rama actual sobre otra rama
git rebase nombre-rama

# Continuar un rebase después de resolver conflictos
git rebase --continue

# Abortar un rebase
git rebase --abort

# Rebase interactivo (para reorganizar, editar o combinar commits)
git rebase -i HEAD~n  # donde n es el número de commits
```

## Trabajo con Repositorios Remotos

### Conectar con un repositorio remoto
```bash
# Agregar un repositorio remoto
git remote add origin https://github.com/usuario/repositorio.git

# Ver los repositorios remotos configurados
git remote -v

# Cambiar la URL de un remoto
git remote set-url origin https://github.com/usuario/nuevo-repositorio.git

# Eliminar un remoto
git remote remove origin
```

### Subir cambios (Push)
```bash
# Subir cambios de la rama actual al remoto
git push origin nombre-rama

# Subir y establecer la rama remota como upstream
git push -u origin nombre-rama

# Subir todas las ramas
git push --all origin

# Subir tags
git push --tags
```

### Descargar cambios (Pull y Fetch)
```bash
# Descargar y fusionar cambios del remoto
git pull origin nombre-rama

# Descargar cambios sin fusionar
git fetch origin

# Descargar cambios de todas las ramas
git fetch --all

# Pull con rebase en lugar de merge
git pull --rebase origin nombre-rama
```

### Clonar repositorios
```bash
# Clonar un repositorio remoto
git clone https://github.com/usuario/repositorio.git

# Clonar en un directorio específico
git clone https://github.com/usuario/repositorio.git nombre-directorio

# Clonar solo una rama específica
git clone -b nombre-rama https://github.com/usuario/repositorio.git
```

## Resolución de Conflictos

### Cuando ocurre un conflicto
Los conflictos ocurren cuando Git no puede fusionar automáticamente los cambios. Los archivos en conflicto tendrán marcadores como:

Tu versión del código


### Resolver conflictos
```bash
# 1. Ver archivos en conflicto
git status

# 2. Editar manualmente los archivos para resolver conflictos

# 3. Marcar como resuelto añadiendo los archivos
git add archivo-resuelto.txt

# 4. Completar el merge o rebase
git commit  # para merge
git rebase --continue  # para rebase

# Abortar si no puedes resolver
git merge --abort  # para merge
git rebase --abort  # para rebase
```

## Deshacer Cambios

### Deshacer cambios en el working directory
```bash
# Descartar cambios en un archivo específico
git checkout -- nombre-archivo.txt

# Descartar todos los cambios no guardados
git checkout -- .

# Alternativa moderna
git restore nombre-archivo.txt
git restore .
```

### Deshacer cambios en staging
```bash
# Quitar un archivo del staging area (mantiene los cambios)
git reset HEAD nombre-archivo.txt

# Alternativa moderna
git restore --staged nombre-archivo.txt
```

### Deshacer commits
```bash
# Deshacer el último commit manteniendo los cambios
git reset --soft HEAD~1

# Deshacer el último commit y quitar del staging (mantiene cambios en working directory)
git reset HEAD~1

# Deshacer el último commit y eliminar todos los cambios (PELIGROSO)
git reset --hard HEAD~1

# Crear un nuevo commit que deshace un commit anterior
git revert <hash-del-commit>
```

## Guardar Cambios Temporalmente (Stash)

```bash
# Guardar cambios temporalmente
git stash

# Guardar con un mensaje descriptivo
git stash save "mensaje descriptivo"

# Ver lista de stashes
git stash list

# Aplicar el último stash
git stash apply

# Aplicar un stash específico
git stash apply stash@{n}

# Aplicar y eliminar el último stash
git stash pop

# Eliminar un stash específico
git stash drop stash@{n}

# Eliminar todos los stashes
git stash clear
```

## Etiquetas (Tags)

```bash
# Crear una etiqueta ligera
git tag v1.0.0

# Crear una etiqueta anotada (recomendado)
git tag -a v1.0.0 -m "Versión 1.0.0"

# Ver todas las etiquetas
git tag

# Ver información de una etiqueta
git show v1.0.0

# Etiquetar un commit específico
git tag -a v1.0.0 <hash-del-commit> -m "Mensaje"

# Subir una etiqueta al remoto
git push origin v1.0.0

# Subir todas las etiquetas
git push origin --tags

# Eliminar una etiqueta local
git tag -d v1.0.0

# Eliminar una etiqueta remota
git push origin --delete v1.0.0
```

## Buenas Prácticas

### Mensajes de commit
- Usa el imperativo: "Agrega función" en lugar de "Agregada función"
- Primera línea: resumen corto (50 caracteres o menos)
- Deja una línea en blanco
- Descripción detallada si es necesario

### Flujo de trabajo recomendado
1. Crea una rama para cada nueva funcionalidad o corrección
2. Haz commits pequeños y frecuentes
3. Escribe mensajes de commit descriptivos
4. Mantén tu rama actualizada con la rama principal
5. Revisa los cambios antes de hacer commit
6. Usa pull requests para revisión de código

### Comandos útiles adicionales
```bash
# Ver quién modificó cada línea de un archivo
git blame nombre-archivo.txt

# Buscar en el historial de commits
git log --grep="palabra-clave"

# Ver cambios de un commit específico
git show <hash-del-commit>

# Ver archivos modificados en un commit
git show --name-only <hash-del-commit>

# Limpiar archivos no rastreados
git clean -n  # ver qué se eliminará
git clean -f  #eliminar archivos no rastreados
git clean -fd  # eliminar archivos y directorios no rastreados
