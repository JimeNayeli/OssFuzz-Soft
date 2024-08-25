Para configurar y ejecutar pruebas de fuzzing para el proyecto usando OSS-Fuzz con javascript.

Tabla de contenido
Introducción
Prerrequisitos
Estructura del proyecto
Construyendo la imagen de Docker
Compilación de fuzzers
Ejecutando los Fuzzers
Análisis de los resultados de fuzzing
Contribuyendo
Licencia
Introducción
Este proyecto integra javascript con OSS-Fuzz para encontrar automáticamente errores en el software mediante pruebas fuzz. Las pruebas fuzz son un tipo de pruebas automatizadas que generan datos aleatorios para probar varias partes de un programa e identificar vulnerabilidades y fallos.

Prerrequisitos
Antes de comenzar, asegúrese de tener instalado lo siguiente:

Docker
Python 3.x
Git
Repositorio OSS-Fuzz.

Estructura del proyecto
A continuación se muestra un desglose de los archivos y directorios relevantes:

Dockerfile : define el entorno para crear y ejecutar fuzzers para Angular.
build.sh : Script para compilar Angular y sus fuzzers.
compiler/ : contiene cualquier modificación o configuración específica para el compilador Angular.
babel.config.json : Archivo de configuración para Babel, utilizado para transpilar código JavaScript.
infra/helper.py : script auxiliar OSS-Fuzz para crear y ejecutar fuzzers.
Construyendo la imagen de Docker

Copiar código
python3 infra/helper.py build_image softwareSeguro
Este comando utiliza el Dockerfiledirectorio raíz del proyecto para crear una imagen que incluye todas las dependencias y herramientas necesarias para compilar y los fuzzers asociados.

Compilación de fuzzers
Una vez que se crea la imagen de Docker, puedes compilar los fuzzers. La compilación de fuzzers los prepara para ejecutarse dentro del marco OSS-Fuzz.

python3 infra/helper.py build_fuzzers softwareSeguro
Opcionalmente, puede especificar un sanitizador (por ejemplo, AddressSanitizer) para detectar tipos específicos de errores:

python3 infra/helper.py build_fuzzers --sanitizer address angular
Ejecutando los Fuzzers
Para ejecutar los fuzzers, utilice el siguiente comando:
python3 infra/helper.py run_fuzzer angular fuzz_parser
Aquí fuzz_parserse encuentra el nombre del fuzzer específico que desea ejecutar. Este fuzzer generará entradas aleatorias en busca de fallas o vulnerabilidades.

Salida
Durante la ejecución, verá una salida en la consola que detalla el progreso del proceso de fuzzing, que incluye:

El tipo de error (por ejemplo, falla de segmentación, desbordamiento de búfer).
La entrada que provocó el bloqueo.
Un seguimiento de la pila que muestra dónde se produjo el error en el código.
Los informes normalmente se guardan en el out/angular/directorio o donde OSS-Fuzz está configurado para almacenar los resultados.
