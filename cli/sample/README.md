# Ejemplo para scantailor-cli

Carpeta de ejemplo para probar el CLI con un proyecto que usa opciones automáticas.

## Contenido

- `in/` – Dos imágenes PNG de ejemplo (page1.png, page2.png).
- `scantailor-cli.conf` – Config por defecto: proyecto `project.ScanTailor`, 2 hilos.
- `project.ScanTailor` – Proyecto mínimo (generado por script o creado con la GUI).
- `generate_project.py` – Script que genera `project.ScanTailor` a partir de las imágenes en `in/`.

## Generar el proyecto (recomendado)

Para tener un proyecto listo sin abrir la GUI:

```bash
python3 cli/sample/generate_project.py
```

Eso crea o sobrescribe `project.ScanTailor` con opciones automáticas para las dos imágenes.

## Alternativa: crear el proyecto con la GUI

Si prefieres crearlo manualmente con la aplicación gráfica:

1. Abre **ScanTailor Advanced** (la versión GUI).
2. **Nuevo proyecto** → elige como directorio de imágenes la carpeta `in/` de este sample.
3. Añade las imágenes (page1.png, page2.png).
4. En cada etapa (Orientación, División, Deskew, Contenido, Márgenes, Salida) deja o elige **automático**.
5. En **Salida**, define el directorio de salida (por ejemplo `out` o la ruta absoluta a `cli/sample/out`).
6. **Guardar proyecto** como `project.ScanTailor` en esta misma carpeta (`cli/sample/`).

## Probar el CLI

La ruta `project=` en el config es **relativa al directorio del archivo de config**, así que puedes ejecutar desde la raíz del repo:

```bash
# Desde la raíz del repositorio (usando el ejecutable en build/)
./build/scantailor-cli -c cli/sample/scantailor-cli.conf

# O pasando el proyecto directamente
./build/scantailor-cli cli/sample/project.ScanTailor

# Con override de hilos
./build/scantailor-cli -t 1 cli/sample/project.ScanTailor
```

(Necesitas haber creado antes `project.ScanTailor` con la GUI, como se indica arriba.)

## Crear proyecto desde cualquier directorio de imágenes (sin GUI)

Para generar un proyecto y procesar **sin abrir la GUI** desde un directorio con imágenes (tif, png, jpg, etc.):

```bash
# Desde la raíz del repo
python3 cli/create_project_from_dir.py /ruta/a/tus/imagenes --run
```

Eso crea `project.ScanTailor` en ese directorio (con todo en automático), crea la carpeta `out/` y ejecuta `scantailor-cli` para procesar todas las imágenes. Opciones útiles:

- `--output-dir NOMBRE` – carpeta de salida (default: `out`)
- `--project RUTA.ScanTailor` – dónde guardar el proyecto
- `--threads N` – número de hilos (con `--run`)
- `--scantailor-cli RUTA` – ruta al ejecutable si no está en `build/` ni en PATH

Ejemplo con tu carpeta de imágenes:

```bash
python3 cli/create_project_from_dir.py ~/mios/libros-enriquecidos/outputs/imagenes --run --threads 2
```

Las páginas procesadas se escribirán en el directorio de salida configurado en el proyecto (p. ej. `out/`).
