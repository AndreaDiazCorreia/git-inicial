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
git log --oneline

# Ver el historial con gráfico
git log --oneline --graph
```

## Comandos iniciales 

holaaaaaa

