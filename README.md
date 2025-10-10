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
