# 📚 Guía Completa de Git y GitHub

## 📖 Tabla de Contenidos
- [Introducción a Git](#introducción-a-git)
- [Instalación y Configuración](#instalación-y-configuración)
- [Conceptos Fundamentales](#conceptos-fundamentales)
- [Comandos Básicos](#comandos-básicos)
- [Trabajo con Ramas](#trabajo-con-ramas)
- [Repositorios Remotos y GitHub](#repositorios-remotos-y-github)
- [Resolución de Conflictos](#resolución-de-conflictos)
- [Comandos Avanzados](#comandos-avanzados)
- [Buenas Prácticas](#buenas-prácticas)

---

## 🎯 Introducción a Git

### ¿Qué es Git?
Git es un **sistema de control de versiones distribuido** que te permite:
- 📝 Rastrear cambios en tu código a lo largo del tiempo
- 🔄 Colaborar con otros desarrolladores de forma eficiente
- 🔙 Volver a versiones anteriores de tu proyecto
- 🌿 Trabajar en múltiples funcionalidades simultáneamente
- 🛡️ Mantener un historial completo de tu proyecto

### ¿Qué es GitHub?
GitHub es una **plataforma de alojamiento** para repositorios Git que ofrece:
- ☁️ Almacenamiento remoto de tus repositorios
- 👥 Herramientas de colaboración (Pull Requests, Issues)
- 🔍 Revisión de código
- 🤖 Integración continua (CI/CD)
- 📊 Gestión de proyectos

---

## ⚙️ Instalación y Configuración

### Instalación de Git

**Linux (Debian/Ubuntu):**
```bash
sudo apt-get update
sudo apt-get install git
```

**Linux (Fedora):**
```bash
sudo dnf install git
```

**macOS:**
```bash
# Usando Homebrew
brew install git

# O descarga desde: https://git-scm.com/download/mac
```

**Windows:**
Descarga el instalador desde: https://git-scm.com/download/win

### Verificar instalación
```bash
git --version
```

## 🔧 Comandos Iniciales de Git

### Configuración inicial

> ⚠️ **Importante:** Esta configuración es necesaria antes de hacer tu primer commit. Git usa esta información para identificar al autor de cada cambio.

```bash
# Configurar nombre de usuario (aparecerá en tus commits)
git config --global user.name "Tu Nombre"

# Configurar email (debe coincidir con tu email de GitHub)
git config --global user.email "tu@email.com"

# Configurar editor por defecto (opcional)
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "nano"          # Nano

# Ver toda la configuración
git config --list

# Ver una configuración específica
git config user.name
```

---

## 📦 Conceptos Fundamentales

### Las Tres Áreas de Git

Git trabaja con tres áreas principales:

1. **Working Directory (Directorio de Trabajo)**
   - Donde editas tus archivos
   - Los cambios aquí NO están guardados en Git todavía

2. **Staging Area (Área de Preparación)**
   - Archivos preparados para el próximo commit
   - Puedes seleccionar qué cambios incluir

3. **Repository (Repositorio)**
   - Historial de commits guardados permanentemente
   - Base de datos de Git con todas las versiones

```
Working Directory  →  Staging Area  →  Repository
   (git add)           (git commit)
```

### Estados de los Archivos

- **Untracked (No rastreado):** Archivo nuevo que Git no conoce
- **Modified (Modificado):** Archivo rastreado que ha cambiado
- **Staged (Preparado):** Cambios listos para commit
- **Committed (Confirmado):** Cambios guardados en el repositorio

---

## 🚀 Comandos Básicos

### Inicializar un repositorio

```bash
# Crear un nuevo repositorio Git en el directorio actual
git init

# Esto crea una carpeta oculta .git/ que contiene toda la información del repositorio
```

**Ejemplo práctico:**
```bash
mkdir mi-proyecto
cd mi-proyecto
git init
echo "# Mi Proyecto" > README.md
```

### Ver el estado del repositorio

```bash
# Ver el estado de los archivos (comando más usado)
git status

# Ver estado de forma resumida
git status -s
```

**Interpretando git status:**
- `??` = Archivo no rastreado (untracked)
- `M` = Archivo modificado
- `A` = Archivo añadido al staging
- `D` = Archivo eliminado

### Ver diferencias

```bash
# Ver cambios en archivos modificados (no staged)
git diff

# Ver cambios en archivos en staging
git diff --staged

# Ver diferencias de un archivo específico
git diff nombre_archivo.txt
```

### Añadir archivos al área de preparación (Staging Area)

```bash
# Añadir un archivo específico
git add nombre_archivo.txt

# Añadir múltiples archivos
git add archivo1.txt archivo2.txt

# Añadir todos los archivos modificados y nuevos
git add .

# Añadir todos los archivos con una extensión específica
git add *.txt

# Añadir interactivamente (te pregunta por cada cambio)
git add -p
```

**💡 Tip:** Usa `git add .` con cuidado. Asegúrate de no incluir archivos innecesarios.

### Crear commits

Un **commit** es una instantánea de tu proyecto en un momento específico.

```bash
# Crear un commit con mensaje
git commit -m "Mensaje descriptivo del commit"

# Commit con mensaje multilínea
git commit -m "Título del commit" -m "Descripción detallada"

# Añadir y hacer commit en un solo paso (solo archivos ya rastreados)
git commit -am "Mensaje del commit"

# Modificar el último commit (agregar cambios o cambiar mensaje)
git commit --amend -m "Nuevo mensaje"
```

**Ejemplo de flujo completo:**
```bash
# 1. Crear un archivo
echo "console.log('Hola Mundo');" > app.js

# 2. Ver el estado
git status  # Verás app.js como untracked

# 3. Añadir al staging
git add app.js

# 4. Verificar
git status  # Verás app.js listo para commit

# 5. Hacer commit
git commit -m "Agregar archivo app.js con mensaje inicial"
```

### Ver el historial de commits

```bash
# Ver el historial completo
git log

# Ver el historial en una línea por commit
git log --oneline

# Ver el historial con gráfico de ramas
git log --oneline --graph --all

# Ver últimos N commits
git log -n 5

# Ver commits de un autor específico
git log --author="Nombre"

# Ver commits con cambios en archivos
git log --stat

---

## 🌿 Trabajo con Ramas

### ¿Qué son las ramas?

Las **ramas** (branches) son líneas de desarrollo independientes que te permiten:
- 🔧 Trabajar en nuevas funcionalidades sin afectar el código principal
- 🐛 Corregir bugs de forma aislada
- 🧪 Experimentar con nuevas ideas
- 👥 Colaborar en paralelo con otros desarrolladores

**Analogía:** Imagina que estás escribiendo un libro. La rama principal (`main`) es tu manuscrito oficial. Cuando quieres probar un nuevo capítulo sin alterar el original, creas una rama. Si te gusta, la fusionas; si no, la descartas.

```
main:     A---B---C---F---G
               \       /
feature:        D-----E
```

### Comandos básicos de ramas

```bash
# Ver todas las ramas locales (* indica la rama actual)
git branch

# Ver todas las ramas (locales y remotas)
git branch -a

# Ver ramas con último commit
git branch -v

# Crear una nueva rama (sin cambiar a ella)
git branch nombre-rama

# Cambiar a una rama existente
git checkout nombre-rama

# Crear y cambiar a una nueva rama en un solo comando
git checkout -b nombre-rama

# Alternativa moderna para cambiar de rama (Git 2.23+)
git switch nombre-rama

# Crear y cambiar a una nueva rama (alternativa moderna)
git switch -c nombre-rama
```

**Ejemplo práctico - Crear una funcionalidad nueva:**
```bash
# Estás en main
git branch                    # Verifica que estás en main

# Crear rama para nueva funcionalidad
git checkout -b feature/login

# Trabajar en la funcionalidad
echo "function login() {}" > login.js
git add login.js
git commit -m "Agregar función de login"

# Volver a main
git checkout main
```

### Fusionar ramas (Merge)

**Merge** combina los cambios de una rama en otra.

```bash
# Fusionar una rama en la rama actual
git merge nombre-rama

# Fusionar sin fast-forward (crea un commit de merge explícito)
git merge --no-ff nombre-rama

# Abortar un merge en caso de conflictos
git merge --abort
```

**Tipos de merge:**

1. **Fast-forward:** Cuando no hay commits nuevos en la rama destino
   ```
   main:     A---B
                  \
   feature:        C---D
   
   Después del merge:
   main:     A---B---C---D
   ```

2. **Three-way merge:** Cuando ambas ramas tienen commits nuevos
   ```
   main:     A---B---E
                  \   \
   feature:        C---D
   
   Después del merge:
   main:     A---B---E---M
                  \     /
   feature:        C---D
   ```

**Ejemplo completo de merge:**
```bash
# 1. Asegurarte de estar en la rama destino (main)
git checkout main

# 2. Fusionar la rama feature
git merge feature/login

# 3. Si todo va bien, eliminar la rama feature
git branch -d feature/login
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

**Rebase** reescribe el historial aplicando tus commits sobre otra rama, creando un historial lineal.

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

**Merge vs Rebase:**

```
Merge:                    Rebase:
main:   A---B---E---M     main:   A---B---E---C'---D'
             \     /                           
feature:      C---D       (historial lineal)
```

**¿Cuándo usar cada uno?**
- **Merge:** Para ramas públicas y colaborativas
- **Rebase:** Para limpiar tu historial local antes de compartir

> ⚠️ **Regla de oro:** Nunca hagas rebase de commits que ya hayas compartido públicamente.

---

## ☁️ Repositorios Remotos y GitHub

### ¿Qué es un repositorio remoto?

Un **repositorio remoto** es una versión de tu proyecto alojada en internet o en una red. GitHub, GitLab y Bitbucket son plataformas populares.

### Conectar con un repositorio remoto

```bash
# Agregar un repositorio remoto (normalmente llamado 'origin')
git remote add origin https://github.com/usuario/repositorio.git

# Ver los repositorios remotos configurados
git remote -v

# Ver información detallada de un remoto
git remote show origin

# Cambiar la URL de un remoto
git remote set-url origin https://github.com/usuario/nuevo-repositorio.git

# Renombrar un remoto
git remote rename origin upstream

# Eliminar un remoto
git remote remove origin
```

**Configurar autenticación con GitHub:**

1. **HTTPS (con token):**
   ```bash
   git remote add origin https://github.com/usuario/repo.git
   # GitHub te pedirá tu token personal en lugar de contraseña
   ```

2. **SSH (recomendado):**
   ```bash
   # Generar clave SSH
   ssh-keygen -t ed25519 -C "tu@email.com"
   
   # Agregar a GitHub: Settings → SSH Keys → New SSH Key
   
   # Usar URL SSH
   git remote add origin git@github.com:usuario/repo.git
   ```

### Subir cambios (Push)

**Push** envía tus commits locales al repositorio remoto.

```bash
# Subir cambios de la rama actual al remoto
git push origin nombre-rama

# Subir y establecer la rama remota como upstream (primera vez)
git push -u origin nombre-rama

# Después de establecer upstream, simplemente:
git push

# Subir todas las ramas
git push --all origin

# Subir tags
git push --tags

# Forzar push (PELIGROSO - sobrescribe historial remoto)
git push --force origin nombre-rama
```

**Flujo típico de trabajo:**
```bash
# 1. Hacer cambios locales
echo "nuevo código" >> archivo.js
git add archivo.js
git commit -m "Agregar nueva funcionalidad"

# 2. Subir al remoto
git push origin main

# O si ya estableciste upstream:
git push
```

> ⚠️ **Cuidado con --force:** Solo úsalo si estás seguro. Puede sobrescribir el trabajo de otros.

### Descargar cambios (Pull y Fetch)

**Fetch** descarga cambios sin fusionarlos. **Pull** descarga y fusiona automáticamente.

```bash
# Descargar y fusionar cambios del remoto (fetch + merge)
git pull origin nombre-rama

# Después de establecer upstream:
git pull

# Descargar cambios sin fusionar (solo actualiza referencias)
git fetch origin

# Descargar cambios de todas las ramas
git fetch --all

# Pull con rebase en lugar de merge (historial más limpio)
git pull --rebase origin nombre-rama

# Ver qué cambios hay en el remoto sin descargar
git fetch origin
git log origin/main..main  # Commits locales no subidos
git log main..origin/main  # Commits remotos no descargados
```

**Diferencia entre fetch y pull:**
```
fetch: remoto → local (sin fusionar)
pull:  remoto → local (con fusión automática)
```

### Clonar repositorios

**Clonar** crea una copia local completa de un repositorio remoto.

```bash
# Clonar un repositorio remoto
git clone https://github.com/usuario/repositorio.git

# Clonar en un directorio específico
git clone https://github.com/usuario/repositorio.git mi-carpeta

# Clonar solo una rama específica
git clone -b nombre-rama https://github.com/usuario/repositorio.git

# Clonar con profundidad limitada (más rápido, menos historial)
git clone --depth 1 https://github.com/usuario/repositorio.git
```

**Primer flujo completo con GitHub:**
```bash
# 1. Crear repositorio en GitHub (vía web)

# 2. En tu computadora
git init
git add .
git commit -m "Primer commit"
git branch -M main
git remote add origin https://github.com/usuario/repo.git
git push -u origin main

# 3. Para colaboradores
git clone https://github.com/usuario/repo.git
cd repo
# Trabajar normalmente
```

---

## ⚔️ Resolución de Conflictos

### ¿Cuándo ocurre un conflicto?

Los conflictos ocurren cuando:
- Dos personas modifican las mismas líneas de un archivo
- Una persona elimina un archivo que otra modificó
- Hay cambios incompatibles en el mismo código

Git no puede decidir automáticamente qué cambios mantener, así que te pide ayuda.

### Pasos para resolver conflictos
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

---

## ↩️ Deshacer Cambios

### Niveles de deshacer

Git te permite deshacer cambios en diferentes niveles:

```
Working Directory → Staging Area → Repository
    (restore)         (restore --staged)  (reset/revert)
```

### Deshacer cambios en el working directory

**Situación:** Modificaste un archivo pero quieres descartar los cambios.

```bash
# Descartar cambios en un archivo específico
git restore nombre-archivo.txt

# Descartar todos los cambios no guardados
git restore .

# Comando antiguo (aún funciona)
git checkout -- nombre-archivo.txt
```

**Ejemplo:**
```bash
# Modificaste app.js pero quieres volver a la última versión
git restore app.js
```

### Deshacer cambios en staging

**Situación:** Hiciste `git add` pero quieres quitar el archivo del staging (sin perder cambios).

```bash
# Quitar un archivo del staging area (mantiene los cambios)
git restore --staged nombre-archivo.txt

# Quitar todos los archivos del staging
git restore --staged .

# Comando antiguo (aún funciona)
git reset HEAD nombre-archivo.txt
```

### Deshacer commits

**Tres formas de deshacer commits:**

1. **`git reset --soft`** (mantiene cambios en staging)
   ```bash
   git reset --soft HEAD~1
   # Útil cuando quieres rehacer el commit con cambios adicionales
   ```

2. **`git reset --mixed`** (mantiene cambios en working directory)
   ```bash
   git reset HEAD~1
   # Útil cuando quieres reorganizar qué incluir en el commit
   ```

3. **`git reset --hard`** (elimina TODO - PELIGROSO)
   ```bash
   git reset --hard HEAD~1
   # ⚠️ Pierdes todos los cambios permanentemente
   ```

**Comparación visual:**
```
Antes:  A---B---C (HEAD)

--soft:  A---B (HEAD), cambios en staging
--mixed: A---B (HEAD), cambios en working directory
--hard:  A---B (HEAD), sin cambios
```

### Revertir un commit (seguro para historial público)

**Situación:** Ya hiciste push y quieres deshacer un commit sin reescribir historial.

```bash
# Crear un nuevo commit que deshace un commit anterior
git revert <hash-del-commit>

# Revertir sin hacer commit automático
git revert -n <hash-del-commit>

# Revertir múltiples commits
git revert <hash1> <hash2>
```

**Diferencia clave:**
- **reset:** Reescribe historial (solo para commits locales)
- **revert:** Crea nuevo commit (seguro para commits públicos)

---

## 💾 Guardar Cambios Temporalmente (Stash)

### ¿Qué es stash?

**Stash** guarda temporalmente tus cambios sin hacer commit, útil cuando necesitas:
- Cambiar de rama rápidamente sin perder tu trabajo
- Hacer un pull sin conflictos
- Probar algo sin commitear cambios incompletos

```bash
# Guardar cambios temporalmente
git stash

# Guardar con un mensaje descriptivo (recomendado)
git stash save "WIP: implementando login"

# Guardar incluyendo archivos no rastreados
git stash -u

# Ver lista de stashes
git stash list

# Aplicar el último stash (mantiene el stash)
git stash apply

# Aplicar un stash específico
git stash apply stash@{2}

# Aplicar y eliminar el último stash
git stash pop

# Ver contenido de un stash
git stash show -p stash@{0}

# Eliminar un stash específico
git stash drop stash@{0}

# Eliminar todos los stashes
git stash clear
```

**Ejemplo práctico:**
```bash
# Estás trabajando en feature-x
git status  # Archivos modificados

# Te piden urgente arreglar un bug en main
git stash save "WIP: feature-x en progreso"

# Cambias a main y arreglas el bug
git checkout main
# ... arreglar bug ...
git add .
git commit -m "Fix: corregir bug crítico"

# Vuelves a tu trabajo
git checkout feature-x
git stash pop  # Recuperas tus cambios
```

---

## 🏷️ Etiquetas (Tags)

### ¿Qué son los tags?

Los **tags** son referencias a puntos específicos en el historial, generalmente usados para marcar versiones de lanzamiento (v1.0, v2.0, etc.).

```bash
# Crear una etiqueta ligera (solo un puntero)
git tag v1.0.0

# Crear una etiqueta anotada (recomendado - incluye metadata)
git tag -a v1.0.0 -m "Versión 1.0.0 - Primera versión estable"

# Ver todas las etiquetas
git tag

# Ver etiquetas que coinciden con un patrón
git tag -l "v1.*"

# Ver información completa de una etiqueta
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

# Checkout a un tag específico
git checkout v1.0.0
```

**Ejemplo de versionado semántico:**
```bash
# Versión inicial
git tag -a v1.0.0 -m "Primera versión estable"

# Corrección de bugs
git tag -a v1.0.1 -m "Corrección de bugs menores"

# Nueva funcionalidad
git tag -a v1.1.0 -m "Agregar autenticación"

# Cambios mayores incompatibles
git tag -a v2.0.0 -m "Rediseño completo de la API"

# Subir todos los tags
git push origin --tags
```

---

## 📋 Archivo .gitignore

### ¿Qué es .gitignore?

El archivo `.gitignore` le indica a Git qué archivos o directorios **NO** debe rastrear. Útil para:
- 🔒 Archivos con información sensible (contraseñas, API keys)
- 📦 Dependencias que se pueden reinstalar (node_modules, venv)
- 🗑️ Archivos temporales y de compilación
- ⚙️ Configuraciones locales del IDE

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
*.swp

# Archivos de IDE
.vscode/
.idea/
*.sublime-project
*.sublime-workspace

# Dependencias de Node.js
node_modules/
npm-debug.log
yarn-error.log

# Dependencias de Python
venv/
env/
__pycache__/
*.pyc
*.pyo
*.egg-info/

# Archivos de compilación
*.o
*.class
*.exe
dist/
build/
target/

# Archivos de configuración sensibles
.env
.env.local
config.local.js
secrets.json
*.key
*.pem

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

# Forzar agregar un archivo ignorado (usar con cuidado)
git add -f archivo-ignorado.txt

# Dejar de rastrear un archivo ya commiteado (sin eliminarlo)
git rm --cached archivo.txt

# Dejar de rastrear una carpeta ya commiteada
git rm -r --cached carpeta/

# Después de modificar .gitignore, aplicar cambios:
git add .gitignore
git commit -m "Actualizar .gitignore"
```

**Ejemplo práctico:**
```bash
# Accidentalmente commiteaste node_modules/
echo "node_modules/" >> .gitignore
git rm -r --cached node_modules/
git add .gitignore
git commit -m "Agregar node_modules a .gitignore"
```

---

## ✅ Buenas Prácticas

### Mensajes de commit

**Formato recomendado:**
```
<tipo>: <descripción corta>

<descripción detallada opcional>

<referencias opcionales>
```

**Tipos comunes:**
- `feat:` Nueva funcionalidad
- `fix:` Corrección de bug
- `docs:` Cambios en documentación
- `style:` Formato, espacios (sin cambios de código)
- `refactor:` Refactorización de código
- `test:` Agregar o modificar tests
- `chore:` Tareas de mantenimiento

**Ejemplos buenos:**
```bash
git commit -m "feat: agregar autenticación con JWT"
git commit -m "fix: corregir error de validación en formulario de login"
git commit -m "docs: actualizar README con instrucciones de instalación"
```

**Ejemplos malos:**
```bash
git commit -m "cambios"
git commit -m "fix"
git commit -m "actualizacion"
```

**Reglas de oro:**
- ✅ Usa el imperativo: "Agrega" no "Agregado" ni "Agregando"
- ✅ Primera línea máximo 50 caracteres
- ✅ Sé específico y descriptivo
- ✅ Explica el "qué" y el "por qué", no el "cómo"
- ❌ No uses punto final en el título
- ❌ No hagas commits de código que no funciona

### Flujo de trabajo recomendado (Git Flow simplificado)

```
main (producción)
  ↓
develop (desarrollo)
  ↓
feature/nueva-funcionalidad (ramas de funcionalidad)
```

**Pasos:**
1. **Crear rama para cada tarea:**
   ```bash
   git checkout -b feature/login
   ```

2. **Hacer commits pequeños y frecuentes:**
   ```bash
   # Mal: un commit gigante con todo
   # Bien: varios commits específicos
   git commit -m "feat: agregar formulario de login"
   git commit -m "feat: agregar validación de email"
   git commit -m "feat: conectar con API de autenticación"
   ```

3. **Mantener tu rama actualizada:**
   ```bash
   git checkout main
   git pull
   git checkout feature/login
   git merge main  # o git rebase main
   ```

4. **Revisar antes de commitear:**
   ```bash
   git diff          # Ver cambios
   git status        # Verificar qué se incluirá
   git add -p        # Agregar selectivamente
   ```

5. **Usar Pull Requests para revisión:**
   - Crea PR en GitHub/GitLab
   - Pide revisión de código
   - Discute cambios si es necesario
   - Fusiona solo después de aprobación

### Convenciones de nombres de ramas

```bash
# Funcionalidades
feature/nombre-descriptivo
feature/user-authentication
feature/payment-integration

# Correcciones
fix/nombre-del-bug
fix/login-error
fix/memory-leak

# Hotfixes (correcciones urgentes en producción)
hotfix/critical-bug

# Releases
release/v1.2.0

# Experimentos
experiment/nueva-arquitectura
```

### Comandos que debes evitar (o usar con cuidado)

```bash
# ⚠️ PELIGROSO - Reescribe historial público
git push --force

# ⚠️ PELIGROSO - Elimina cambios permanentemente
git reset --hard

# ⚠️ PELIGROSO - Reescribe commits públicos
git rebase (en ramas compartidas)

# ⚠️ Puede causar conflictos
git merge (sin revisar cambios primero)
```

### Checklist antes de hacer push

- [ ] ¿Compilé/ejecuté el código localmente?
- [ ] ¿Pasaron todos los tests?
- [ ] ¿Revisé los cambios con `git diff`?
- [ ] ¿El mensaje de commit es descriptivo?
- [ ] ¿Actualicé la documentación si es necesario?
- [ ] ¿Eliminé código comentado o debug?
- [ ] ¿No incluí archivos sensibles (.env, keys)?

---

## 🔧 Comandos Avanzados

### Git Blame - Rastrear cambios por línea

```bash
# Ver quién modificó cada línea de un archivo
git blame nombre-archivo.txt

# Ver blame con formato más legible
git blame -L 10,20 archivo.txt  # Solo líneas 10-20

# Ignorar cambios de espacios en blanco
git blame -w archivo.txt

# Ver blame con hash corto
git blame --abbrev archivo.txt
```

### Buscar en el historial

```bash
# Buscar en mensajes de commit
git log --grep="palabra-clave"

# Buscar commits que modificaron una cadena específica
git log -S "función_importante"

# Buscar por autor
git log --author="Nombre"

# Buscar por fecha
git log --since="2024-01-01" --until="2024-12-31"

# Combinar filtros
git log --author="Andrea" --since="1 week ago" --oneline
```

### Ver información de commits

```bash
# Ver cambios de un commit específico
git show <hash-del-commit>

# Ver solo archivos modificados en un commit
git show --name-only <hash-del-commit>

# Ver estadísticas de un commit
git show --stat <hash-del-commit>

# Ver el último commit
git show HEAD
```

### Limpiar archivos no rastreados

```bash
# Ver qué se eliminará (simulación)
git clean -n

# Eliminar archivos no rastreados
git clean -f

# Eliminar archivos y directorios no rastreados
git clean -fd

# Incluir archivos ignorados en la limpieza
git clean -fx
```

> ⚠️ **Cuidado:** `git clean` elimina archivos permanentemente. Siempre usa `-n` primero para ver qué se eliminará.

---

## 🍒 Cherry Pick - Aplicar Commits Específicos

### ¿Qué es cherry-pick?

**Cherry-pick** te permite copiar un commit específico de una rama a otra, sin fusionar toda la rama.

**Casos de uso:**
- Aplicar un bugfix de una rama a otra
- Mover un commit que se hizo en la rama incorrecta
- Aplicar una funcionalidad específica sin traer todo

```bash
# Aplicar un commit específico a la rama actual
git cherry-pick <hash-del-commit>

# Aplicar múltiples commits
git cherry-pick <hash1> <hash2> <hash3>

# Aplicar un rango de commits
git cherry-pick <hash-inicio>..<hash-fin>

# Cherry-pick sin hacer commit automático (para revisar primero)
git cherry-pick -n <hash-del-commit>

# Continuar después de resolver conflictos
git cherry-pick --continue

# Abortar el cherry-pick
git cherry-pick --abort
```

**Ejemplo práctico:**
```bash
# Situación: Hiciste un bugfix en develop pero necesitas aplicarlo a main
git checkout main
git log develop --oneline  # Encontrar el hash del commit
git cherry-pick abc1234    # Aplicar solo ese commit
git push origin main
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

---

## 🔍 Bisect - Encontrar el Commit que Introdujo un Bug

### ¿Qué es bisect?

**Git bisect** usa búsqueda binaria para encontrar rápidamente el commit que introdujo un bug.

**Proceso:**
1. Marcas un commit "malo" (con bug)
2. Marcas un commit "bueno" (sin bug)
3. Git te muestra commits intermedios
4. Pruebas cada uno y lo marcas como bueno o malo
5. Git encuentra el commit problemático

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

**Ejemplo práctico:**
```bash
# El código actual tiene un bug, pero hace 10 commits funcionaba
git bisect start
git bisect bad                    # Commit actual tiene el bug
git bisect good HEAD~10           # Hace 10 commits funcionaba

# Git te muestra un commit intermedio
# Pruebas tu aplicación...
git bisect good  # o bad según el resultado

# Repites hasta que Git encuentre el commit exacto
# Git te dirá: "abc1234 is the first bad commit"

git bisect reset  # Volver a la rama original
```

---

## 🔄 Reflog - Recuperar Commits "Perdidos"

### ¿Qué es reflog?

**Reflog** (reference log) registra **todos** los movimientos de HEAD, incluso commits que parecen "perdidos" después de un reset o rebase.

**Es tu red de seguridad:** Si borraste algo por error, probablemente puedas recuperarlo con reflog.

```bash
# Ver el historial de reflog
git reflog

# Ver reflog con más detalle
git reflog show --all

# Ver reflog de una rama específica
git reflog show nombre-rama

# Recuperar un commit "perdido"
git reflog                        # Encontrar el hash
git checkout <hash-del-commit>
git branch recuperar-rama         # Crear rama desde ese commit

# Deshacer un reset hard
git reflog
git reset --hard HEAD@{n}         # donde n es el número en reflog
```

**Ejemplo de rescate:**
```bash
# ¡Oh no! Hiciste reset --hard y perdiste commits
git reset --hard HEAD~3  # Perdiste 3 commits

# Recuperar con reflog
git reflog
# Verás algo como:
# abc1234 HEAD@{0}: reset: moving to HEAD~3
# def5678 HEAD@{1}: commit: Mi commit importante  ← Este queremos recuperar

# Recuperar
git reset --hard HEAD@{1}
# o
git reset --hard def5678

# ¡Commits recuperados!
```

> 💡 **Nota:** Reflog solo guarda información por 90 días por defecto.

---

## ⚡ Alias - Atajos Personalizados

### ¿Por qué usar alias?

Los **alias** te permiten crear atajos para comandos que usas frecuentemente, ahorrando tiempo y tecleo.

### Crear alias útiles

```bash
# Alias básicos para comandos comunes
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'

# Alias para ver historial bonito
git config --global alias.lg "log --oneline --graph --all --decorate"
git config --global alias.lol "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# Alias útiles
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual "log --graph --oneline --all"
git config --global alias.undo 'reset --soft HEAD~1'
git config --global alias.amend 'commit --amend --no-edit'
git config --global alias.contributors 'shortlog -sn'

# Ver todos los alias configurados
git config --global --get-regexp alias

# Eliminar un alias
git config --global --unset alias.nombre
```

### Usar los alias

```bash
# En lugar de: git status
git st

# En lugar de: git log --oneline --graph --all
git lg

# Ver último commit
git last

# Modificar último commit sin cambiar mensaje
git amend
```

**Alias recomendados para copiar:**
```bash
git config --global alias.st 'status -sb'
git config --global alias.co checkout
git config --global alias.br 'branch -v'
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
git config --global alias.undo 'reset --soft HEAD~1'
git config --global alias.amend 'commit --amend --no-edit'
```

---

## 🌳 Worktree - Múltiples Directorios de Trabajo

### ¿Qué es worktree?

**Worktree** te permite tener múltiples copias de trabajo del mismo repositorio, cada una en una rama diferente.

**Casos de uso:**
- Trabajar en una funcionalidad mientras revisas un PR en otra rama
- Comparar código entre ramas sin hacer checkout
- Ejecutar tests en una rama mientras desarrollas en otra

```bash
# Crear un nuevo worktree
git worktree add ../proyecto-feature feature-branch

# Crear worktree con nueva rama
git worktree add -b nueva-rama ../proyecto-nueva

# Listar todos los worktrees
git worktree list

# Eliminar un worktree
git worktree remove ../proyecto-feature

# Limpiar worktrees obsoletos
git worktree prune
```

**Ejemplo práctico:**
```bash
# Estás en /home/usuario/proyecto trabajando en feature-x
# Te piden revisar urgente un PR en otra rama

# Crear worktree temporal
git worktree add ../proyecto-review review-branch

# Ahora tienes:
# /home/usuario/proyecto        → feature-x
# /home/usuario/proyecto-review → review-branch

cd ../proyecto-review
# Revisar, probar, etc.

# Cuando termines
cd ../proyecto
git worktree remove ../proyecto-review
```

---

## 🔎 Comandos de Inspección Avanzados

### Historial de archivos

```bash
# Ver el historial de un archivo específico
git log --follow archivo.txt

# Ver cambios en un archivo a través del tiempo
git log -p archivo.txt

# Ver quién cambió qué en un archivo
git log --pretty=format:"%h - %an, %ar : %s" archivo.txt

# Ver commits que afectaron un archivo
git log --oneline -- archivo.txt
```

### Estadísticas y análisis

```bash
# Ver estadísticas de commits por autor
git shortlog -sn

# Ver estadísticas con emails
git shortlog -sne

# Commits de la última semana
git log --since="1 week ago" --oneline

# Commits entre fechas
git log --since="2024-01-01" --until="2024-12-31"

# Actividad por día de la semana
git log --format="%ad" --date=format:"%A" | sort | uniq -c
```

### Búsqueda avanzada

```bash
# Ver commits que modificaron una función específica
git log -L :nombre_funcion:archivo.py

# Buscar en el contenido de commits (cuando se agregó/eliminó texto)
git log -S "texto-a-buscar"

# Buscar con regex
git log -G "patron.*regex"

# Ver árbol de archivos en un commit
git ls-tree -r <hash-del-commit>

# Ver solo nombres de archivos en un commit
git diff-tree --no-commit-id --name-only -r <hash-del-commit>
```

### Comparaciones

```bash
# Comparar dos commits
git diff <commit1> <commit2>

# Ver cambios entre branches con estadísticas
git diff --stat main..feature

# Ver archivos que cambiaron entre branches
git diff --name-only main..feature

# Ver diferencias de un archivo específico entre branches
git diff main..feature -- archivo.txt
```

---

## 📚 Recursos Adicionales

### Documentación oficial
- [Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [Git Book (Pro Git)](https://git-scm.com/book/es/v2)

### Herramientas visuales
- **GitKraken** - Cliente Git visual multiplataforma
- **SourceTree** - Cliente Git gratuito de Atlassian
- **GitHub Desktop** - Cliente oficial de GitHub
- **Git Extensions** - Interfaz gráfica para Windows

### Cheat Sheets
- [GitHub Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Atlassian Git Cheat Sheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)

### Práctica interactiva
- [Learn Git Branching](https://learngitbranching.js.org/?locale=es_ES) - Tutorial interactivo
- [Git Immersion](https://gitimmersion.com/) - Tour guiado de Git
- [Oh My Git!](https://ohmygit.org/) - Juego para aprender Git

---

## 🎓 Resumen de Comandos Esenciales

### Configuración inicial
```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
```

### Flujo básico
```bash
git init                          # Inicializar repositorio
git add .                         # Añadir archivos
git commit -m "mensaje"           # Hacer commit
git status                        # Ver estado
git log --oneline                 # Ver historial
```

### Trabajo con ramas
```bash
git branch nombre-rama            # Crear rama
git checkout nombre-rama          # Cambiar de rama
git checkout -b nombre-rama       # Crear y cambiar
git merge nombre-rama             # Fusionar rama
git branch -d nombre-rama         # Eliminar rama
```

### Trabajo remoto
```bash
git clone url                     # Clonar repositorio
git remote add origin url         # Agregar remoto
git push -u origin main           # Subir cambios
git pull origin main              # Descargar cambios
git fetch origin                  # Descargar sin fusionar
```

### Deshacer cambios
```bash
git restore archivo               # Descartar cambios
git restore --staged archivo      # Quitar de staging
git reset --soft HEAD~1           # Deshacer último commit
git revert hash                   # Revertir commit
```

### Comandos de emergencia
```bash
git stash                         # Guardar cambios temporalmente
git reflog                        # Ver historial completo
git clean -fd                     # Limpiar archivos no rastreados
```

---

## 💡 Consejos Finales

1. **Commitea frecuentemente** - Commits pequeños son más fáciles de entender y revertir
2. **Escribe buenos mensajes** - Tu yo del futuro te lo agradecerá
3. **Usa ramas** - Nunca trabajes directamente en main
4. **Haz pull antes de push** - Evita conflictos innecesarios
5. **Revisa antes de commitear** - Usa `git diff` y `git status`
6. **No hagas push de secretos** - Usa `.gitignore` para archivos sensibles
7. **Aprende a resolver conflictos** - Es parte normal del desarrollo colaborativo
8. **Usa .gitignore desde el inicio** - Evita commitear archivos innecesarios
9. **Practica en un repositorio de prueba** - Experimenta sin miedo
10. **Lee los mensajes de Git** - Git te da pistas útiles cuando algo sale mal

---

## 🤝 Contribuciones

¿Encontraste un error o quieres agregar algo? ¡Las contribuciones son bienvenidas!

Saludos si llegaste hasta aca

---

**¡Feliz coding con Git! 🚀**
