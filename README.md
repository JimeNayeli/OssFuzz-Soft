# Proyecto OSS-Fuzz

## Tabla de Contenido
- [Introducción](#introducción)
- [Prerrequisitos](#prerrequisitos)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Construyendo la Imagen de Docker](#construyendo-la-imagen-de-docker)
- [Compilación de Fuzzers](#compilación-de-fuzzers)

## Introducción

Este proyecto integra javascript con **OSS-Fuzz** para encontrar automáticamente errores en el software mediante pruebas fuzz. Las pruebas fuzz son un tipo de pruebas automatizadas que generan datos aleatorios para probar varias partes de un programa e identificar vulnerabilidades y fallos.

## Prerrequisitos

Antes de comenzar, asegúrese de tener instalado lo siguiente:

- **Docker**
- **Python 3.x**
- **Git**
- Acceso al repositorio **OSS-Fuzz**

## Estructura del Proyecto

A continuación se muestra un desglose de los archivos y directorios relevantes:

- **Dockerfile**: Define el entorno para crear y ejecutar fuzzers para Angular.
- **build.sh**: Script para compilar los fuzzers.
- **compiler/**: Contiene cualquier modificación o configuración específica para el compilador Angular.
- **babel.config.json**: Archivo de configuración para Babel, utilizado para transpilar código JavaScript.
- **infra/helper.py**: Script auxiliar OSS-Fuzz para crear y ejecutar fuzzers.

## Construyendo la Imagen de Docker

Para construir la imagen Docker, ejecute el siguiente comando:

```bash
python3 infra/helper.py build_image softwareSeguro
```
### Compilación de Fuzzers

Una vez que la imagen de Docker esté construida, puedes compilar los fuzzers. La compilación de fuzzers los prepara para ejecutarse dentro del marco OSS-Fuzz.

```bash
python3 infra/helper.py build_fuzzers --sanitizer address softwareSeguro
python3 infra/helper.py run_fuzzer softwareSeguro fuzz_parser
```

