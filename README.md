# Prácticas de Sistemas Operativos

Repositorio de trabajos prácticos y ejercicios de **Sistemas Operativos**. Reúne resoluciones experimentales sobre administración de procesos, señales, archivos, concurrencia, comunicación entre procesos, redes y automatización de tareas mediante scripts.

## Stack y tecnologías

- **C (GNU/Linux):** procesos y jerarquías con `fork`, señales, espera de procesos, archivos, memoria compartida, hilos POSIX (`pthreads`), sockets TCP y estructuras de datos.
- **Bash:** scripting de consola, parámetros, permisos, filtros de texto, archivos de registro, señales y análisis de directorios.
- **AWK:** procesamiento de reportes y registros desde scripts Bash.
- **PowerShell:** automatización en Windows, navegación del sistema de archivos, jobs, edición de texto, XML, HTML, CSV y gestión de procesos.
- **Formatos de apoyo:** `.txt`, `.log`, `.csv`, `.xml` y `.html`.

El código fue realizado como material de práctica y conserva archivos de entrada, salidas y pruebas de cada ejercicio para poder reproducir los escenarios originales.

## Contenido del repositorio

### Bash y AWK

| Ruta | Temas principales |
| --- | --- |
| [`bash/ejercicio1`](bash/ejercicio1) | Parámetros de scripts, permisos, copias de seguridad y modificación de archivos con herramientas Unix. |
| [`bash/ejercicio2`](bash/ejercicio2) | Procesamiento de texto, diccionarios, transformación de mayúsculas y validación de archivos. |
| [`bash/ejercicio3`](bash/ejercicio3) | Operaciones sobre archivos y directorios de prueba. |
| [`bash/ejercicio4`](bash/ejercicio4) | Lectura de logs, generación de reportes y consulta por legajo; incluye [`ejercicio4.awk`](bash/ejercicio4/ejercicio4.awk). |
| [`bash/ejercicio5`](bash/ejercicio5) | Manejo de señales (`SIGUSR1`, `SIGUSR2` y `SIGTERM`) y registro de eventos. |
| [`bash/ejercicio6`](bash/ejercicio6) | Búsqueda de los subdirectorios hoja más grandes y conteo de archivos. |

### C

| Ruta | Temas principales |
| --- | --- |
| [`c/ejercicio1`](c/ejercicio1) | Creación de una jerarquía de procesos, identificación de generaciones y tratamiento de señales, zombies y demonios. |
| [`c/ejercicio2`](c/ejercicio2) | Procesamiento concurrente de archivos `.txt` con `pthread`; cuenta vocales, consonantes y caracteres, y genera estadísticas. |
| [`c/ejercicio3`](c/ejercicio3) | Trabajo con archivos y registros usando llamadas POSIX de bajo nivel. |
| [`c/ejercicio4`](c/ejercicio4) | Cliente-servidor TCP con hilos y colas; el servidor escucha en el puerto `5000`. |
| [`c/ejercicio5`](c/ejercicio5) | Comunicación entre procesos mediante memoria compartida. |

El ejercicio 4 incluye una guía específica en [`como_compilar_y_ejecutar.txt`](c/ejercicio4/como_compilar_y_ejecutar.txt). El directorio `c/ejercicio2` también contiene datos de entrada y binarios generados durante las pruebas.

### PowerShell

| Ruta | Temas principales |
| --- | --- |
| [`powershell/EJ 1`](powershell/EJ%201) | Recorrido y procesamiento de archivos de texto, con material de prueba anidado. |
| [`powershell/EJ 2`](powershell/EJ%202) | Trabajo con páginas HTML locales y navegación entre archivos. |
| [`powershell/EJ 3`](powershell/EJ%203) | Lanzador y corrector de texto: monitorización de un editor, jobs, modificación de párrafos y generación de logs. |
| [`powershell/EJ 4`](powershell/EJ%204) | Actualización de un inventario XML a partir de precios y stocks de proveedores, con opción de backup. |
| [`powershell/EJ 5`](powershell/EJ%205) | Procesamiento y consulta de procesos, con salida de errores y resultados. |
| [`powershell/EJ 6`](powershell/EJ%206) | Lectura y actualización de puntajes desde CSV, registro de jugadores y consulta de los mejores resultados. |

## Requisitos

### Entorno Linux

Para Bash, AWK y C se necesita:

- Bash, coreutils y `awk`.
- GCC y `make` opcionalmente.
- Bibliotecas POSIX disponibles en un sistema GNU/Linux, incluyendo `pthread`.

En Debian/Ubuntu:

```bash
sudo apt update
sudo apt install build-essential bash gawk
```

### Entorno Windows

Para las prácticas de PowerShell:

- PowerShell 5.1 o PowerShell 7+.
- Permisos suficientes para ejecutar scripts y crear/modificar archivos en las carpetas de prueba.
- Un editor compatible para el ejercicio 3, por ejemplo `notepad.exe`.

## Cómo ejecutar

No existe un ejecutable único ni un sistema de build global: cada ejercicio es independiente. Antes de ejecutarlo, hay que situarse en su directorio para que las rutas relativas a los archivos de prueba funcionen correctamente.

### Bash

```bash
cd bash/ejercicio4
chmod +x ej4.sh
./ej4.sh -h
./ej4.sh ./reporteA.log -r
```

Los parámetros disponibles dependen del ejercicio. Cuando existe ayuda integrada, consultar `-h`, `-help` o `-?`.

### C

Ejemplo para el ejercicio concurrente:

```bash
cd c/ejercicio2
gcc -Wall -Wextra -pthread main.c -o programa
mkdir -p archivos_de_salida
./programa ./archivos_de_entrada ./archivos_de_salida 3
```

El primer argumento es el directorio de entrada, el segundo el de salida y el tercero el nivel de paralelismo. El programa analiza archivos `.txt`.

Para el cliente-servidor:

```bash
cd c/ejercicio4
gcc -Wall -Wextra servidor.c -o servidor -lpthread
gcc -Wall -Wextra cliente.c -o cliente -lpthread

# Terminal 1
./servidor

# Terminal 2
./cliente 127.0.0.1
```

### PowerShell

Desde PowerShell, ejecutar cada script desde su propia carpeta:

```powershell
Set-Location .\powershell\EJ 4
.\ejercicio4.ps1 -inventario .\invLibreria.xml -proveedor .\Proveedores -backup
```

Si la política de ejecución lo impide, puede habilitarse para el usuario actual:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

## Conceptos practicados

- Procesos padre e hijo, PID/PPID y árboles de procesos.
- Señales, bloqueo y espera de señales.
- Procesos zombies y demonios.
- Lectura y escritura de archivos y logs.
- Hilos, mutexes y reparto de trabajo.
- Sockets TCP y modelo cliente-servidor.
- Memoria compartida y comunicación entre procesos.
- Parámetros, validación de entradas y códigos de salida.
- Automatización multiplataforma con Bash y PowerShell.
- Transformación de datos estructurados en XML, CSV y HTML.

## Notas

- Las rutas con espacios deben escribirse entre comillas.
- Los scripts pueden depender del shell y del sistema operativo desde el que se ejecutan.
- Los datos de `prueba/`, `PRUEBA/`, `Proveedores/` y `archivos_de_entrada/` forman parte de los escenarios de prueba.
- Los archivos binarios presentes en `c/` son artefactos de compilación; para reproducirlos se recomienda recompilar desde el código fuente.

## Autoría

Material académico de prácticas de Sistemas Operativos. Los encabezados de los ejercicios conservan la información de autores y entregas correspondiente a cada trabajo práctico.
