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

### Entendiendo los marcadores de conflicto
Cuando Git encuentra un conflicto, marca las secciones conflictivas en el archivo de esta forma:

```
Este es el código en tu rama actual (HEAD)
Puede ser una o varias líneas
```

**Explicación de los marcadores:**
- `<<<<<<< HEAD`: Inicio del código en tu rama actual
- `=======`: Separador entre las dos versiones
- `>>>>>>> nombre-de-la-rama`: Fin del código de la otra rama

### Tipos de conflictos comunes

#### 1. Conflicto de contenido
Ocurre cuando dos ramas modifican las mismas líneas de un archivo de forma diferente.

**Ejemplo:**
```
def calcular_total(precio):
    return precio * 1.21  # IVA 21%
```

**Solución:** Decide qué versión mantener o combina ambas.

#### 2. Conflicto de eliminación
Una rama elimina un archivo mientras otra lo modifica.

```bash
# Git te preguntará qué hacer
# Mantener el archivo modificado:
git add archivo.txt

# Confirmar la eliminación:
git rm archivo.txt
```

#### 3. Conflicto de renombrado
Dos ramas renombran el mismo archivo de forma diferente.

### Estrategias para resolver conflictos

#### Opción 1: Edición manual (recomendado)
1. Abre el archivo en tu editor
2. Busca los marcadores `<<<<<<<`, `=======`, `>>>>>>>`
3. Decide qué código mantener
4. Elimina los marcadores de conflicto
5. Guarda el archivo
6. Marca como resuelto con `git add`

#### Opción 2: Aceptar una versión completa
```bash
# Aceptar tu versión (HEAD) para un archivo
git checkout --ours archivo.txt

# Aceptar la versión de la otra rama para un archivo
git checkout --theirs archivo.txt

# Marcar como resuelto
git add archivo.txt
```

#### Opción 3: Usar herramientas de merge
```bash
# Abrir herramienta visual de merge (si está configurada)
git mergetool

# Configurar una herramienta de merge (ejemplo con VS Code)
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'
```

### Prevenir conflictos

**Buenas prácticas:**
- Mantén tu rama actualizada con la rama principal frecuentemente
- Haz commits pequeños y específicos
- Comunica con tu equipo sobre qué archivos estás modificando
- Usa `git pull --rebase` para mantener un historial más limpio
- Divide el trabajo en archivos o funciones diferentes cuando sea posible

### Verificar después de resolver
```bash
# Ver el estado después de resolver
git status

# Verificar que no quedan marcadores de conflicto
git diff --check

# Ver los cambios que se van a commitear
git diff --cached
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
```
Inicialmente no hace falta un git ignore pero es buena practica 
## Archivo .gitignore

### ¿Qué es .gitignore?
El archivo `.gitignore` le indica a Git qué archivos o directorios debe ignorar y no rastrear.

### Crear y usar .gitignore
```bash
# Crear archivo .gitignore en la raíz del proyecto
touch .gitignore

# Editar con tu editor favorito
nano .gitignore
```

### Patrones comunes en .gitignore
```gitignore
# Archivos de sistema
.DS_Store
Thumbs.db

# Archivos de IDE
.vscode/
.idea/
*.swp
*.swo

# Dependencias
node_modules/
venv/
env/
__pycache__/
*.pyc

# Archivos de compilación
*.o
*.class
*.exe
dist/
build/

# Archivos de configuración sensibles
.env
config.local.js
secrets.json

# Logs
*.log
logs/

# Archivos temporales
*.tmp
*.temp
.cache/
```

### Comandos útiles con .gitignore
```bash
# Ver archivos ignorados
git status --ignored

# Forzar agregar un archivo ignorado
git add -f archivo-ignorado.txt

# Dejar de rastrear un archivo ya commiteado (sin eliminarlo)
git rm --cached archivo.txt

# Dejar de rastrear una carpeta ya commiteada
git rm -r --cached carpeta/
```

## Cherry Pick - Aplicar Commits Específicos

### ¿Qué es cherry-pick?
Permite aplicar un commit específico de una rama a otra, sin fusionar toda la rama.

```bash
# Aplicar un commit específico a la rama actual
git cherry-pick <hash-del-commit>

# Aplicar múltiples commits
git cherry-pick <hash1> <hash2> <hash3>

# Aplicar un rango de commits
git cherry-pick <hash-inicio>..<hash-fin>

# Cherry-pick sin hacer commit automático
git cherry-pick -n <hash-del-commit>

# Continuar después de resolver conflictos
git cherry-pick --continue

# Abortar el cherry-pick
git cherry-pick --abort
```

## Submódulos - Repositorios Dentro de Repositorios

### Agregar un submódulo
```bash
# Agregar un repositorio como submódulo
git submodule add https://github.com/usuario/repo.git ruta/al/submodulo

# Ver submódulos
git submodule status
```

### Trabajar con submódulos
```bash
# Clonar un repositorio con submódulos
git clone --recursive https://github.com/usuario/repo.git

# Inicializar submódulos después de clonar
git submodule init
git submodule update

# Actualizar todos los submódulos
git submodule update --remote

# Eliminar un submódulo
git submodule deinit ruta/al/submodulo
git rm ruta/al/submodulo
```

## Hooks - Automatización con Git

### ¿Qué son los hooks?
Los hooks son scripts que Git ejecuta automáticamente en ciertos eventos.

### Ubicación de los hooks
Los hooks se encuentran en `.git/hooks/`

### Hooks comunes
```bash
# pre-commit: Se ejecuta antes de hacer commit
# Ejemplo: verificar formato de código
.git/hooks/pre-commit

# commit-msg: Se ejecuta al crear el mensaje de commit
# Ejemplo: validar formato del mensaje
.git/hooks/commit-msg

# pre-push: Se ejecuta antes de hacer push
# Ejemplo: ejecutar tests
.git/hooks/pre-push

# post-merge: Se ejecuta después de un merge
# Ejemplo: instalar dependencias
.git/hooks/post-merge
```

### Crear un hook simple
```bash
# Crear hook pre-commit
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash
echo "Ejecutando verificaciones antes del commit..."
# Agregar tus verificaciones aquí
EOF

# Dar permisos de ejecución
chmod +x .git/hooks/pre-commit
```

## Bisect - Encontrar el Commit que Introdujo un Bug

### Uso de git bisect
```bash
# Iniciar bisect
git bisect start

# Marcar el commit actual como malo
git bisect bad

# Marcar un commit anterior que funcionaba como bueno
git bisect good <hash-commit-bueno>

# Git irá mostrando commits intermedios
# Prueba cada uno y marca como good o bad
git bisect good  # si funciona
git bisect bad   # si tiene el bug

# Git encontrará el commit problemático

# Terminar bisect
git bisect reset
```

## Reflog - Recuperar Commits Perdidos

### ¿Qué es reflog?
El reflog registra todos los movimientos de HEAD, incluso commits "perdidos".

```bash
# Ver el historial de reflog
git reflog

# Ver reflog con más detalle
git reflog show --all

# Recuperar un commit "perdido"
git reflog  # encontrar el hash
git checkout <hash-del-commit>
git branch recuperar-rama  # crear rama desde ese commit

# Deshacer un reset hard
git reflog
git reset --hard HEAD@{n}  # donde n es el número en reflog
```

## Alias - Atajos Personalizados

### Crear alias útiles
```bash
# Alias para comandos comunes
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'

# Alias más complejos
git config --global alias.lg "log --oneline --graph --all --decorate"
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual "log --graph --oneline --all"
git config --global alias.undo 'reset --soft HEAD~1'

# Ver todos los alias configurados
git config --global --get-regexp alias
```

### Usar los alias
```bash
# En lugar de: git status
git st

# En lugar de: git log --oneline --graph --all
git lg
```

## Worktree - Múltiples Directorios de Trabajo

### ¿Qué es worktree?
Permite trabajar en múltiples ramas simultáneamente en diferentes directorios.

```bash
# Crear un nuevo worktree
git worktree add ../proyecto-feature feature-branch

# Listar worktrees
git worktree list

# Eliminar un worktree
git worktree remove ../proyecto-feature

# Limpiar worktrees obsoletos
git worktree prune
```

## Comandos de Inspección Avanzados

```bash
# Ver el historial de un archivo específico
git log --follow archivo.txt

# Ver cambios en un archivo a través del tiempo
git log -p archivo.txt

# Ver estadísticas de commits por autor
git shortlog -sn

# Ver commits por fecha
git log --since="2 weeks ago"
git log --until="2024-01-01"

# Ver commits que modificaron una función específica
git log -L :nombre_funcion:archivo.py

# Buscar en el contenido de commits
git log -S "texto-a-buscar"

# Ver árbol de archivos en un commit
git ls-tree -r <hash-del-commit>

# Comparar dos commits
git diff <commit1> <commit2>

# Ver cambios entre branches con estadísticas
git diff --stat main..feature
