# LRS - Longest Run Subsequence Problem

Este repositorio contiene la implementación de un BRKGA guiado por LLM para resolver el problema de la Subsecuencia de Carrera Más Larga (Longest Run Subsequence).

## Descripción del Problema

El problema LRS consiste en encontrar una subsecuencia de una cadena de entrada que maximice la suma de las longitudes de las carreras (runs) consecutivas de caracteres idénticos.

## Estructura del Proyecto

```
├── src/                    # Código fuente de los algoritmos BRKGA y BRKGA-LLM guided
├── bin/             	   # ejecutables
├── Instances/             # Instancias
├── CD/                    # Análisis estadístico y resultados
├── tuning_instances/      # Instancias generadas aleatoriamente para dataset tuning
└── LLM_probabilities/     # Probabilidades LLM
```

## Compilación

Para compilar todos los algoritmos, use los siguientes comandos:

```bash

# Compilar BRKGA
g++ brkga src/brkga.cpp -o brkga


# Compilar BRKGA-LLM
g++ src/brkgallm.cpp -o brkgallm 

```

## Ejecución de Algoritmos

### Formato de Instancias

Las instancias están en formato de texto plano, cada archivo contiene una cadena de caracteres. Ejemplo:
```
BAABAABABBAABAABBABBBABAABBBBAAAAAABBAAABBBAABABBABBABBBBABAAABBBAAABAABBAABBABBBABAABBBAAAABAABABAB
```

### Parámetros

```bash
./brkga -i <archivo_instancia> [-p <tamaño_pob>] [-pe <prop_elite>] [-pm <prop_mutante>] [-rhoe <prob_herencia>] [-t <tiempo>] [-tuning] [-stnweb]
```
- `-p`: Tamaño de población (default: valor por defecto)
- `-pe`: Proporción de élite (default: valor por defecto)
- `-pm`: Proporción de mutantes (default: valor por defecto)
- `-rhoe`: Probabilidad de herencia élite (default: valor por defecto)
- `-t`: Límite de tiempo (default: valor por defecto)
- `-tuning`: Modo tuning
- `-stnweb`: Modo stnweb

- `-model(LLM)`: nombre de la carpeta de probabilidades dentro de LLM_probabilities



### Ejemplos de Ejecución


# Ejecutar BRKGA
./brkga -i Instances/len_100_sigma2_1.txt -p 200 -pe 0.27 -pm 0.13 -rhoe 0.6

# Ejecutar LLM
./brkgallm -i Instances/len_100_sigma32_1.txt -p 18 -pe 0.23 -pm 0.2 -rhoe 0.69 -model Lama-4-Maverick


## Análisis Estadístico

El directorio `CD/` contiene herramientas para análisis estadístico:

1. Prepare un archivo `results.dat` con los resultados de todos los algoritmos
2. Use R con el script `statistical_evaluation.R` para generar análisis estadísticos

Ver `CD/Readme` para instrucciones detalladas sobre el análisis estadístico.

## Instancias

El directorio `Instances/` contiene instancias de prueba con diferentes características:
- `len_{100,200,300,500,1000,2000}_sigma{2,4,6,8,16,32}_{1..30}.txt`: 30 Cadenas de combinación length-sigma

## Instancias de Tuning

El directorio `Tuning_instances/` contiene un dataset generado de manera aleatoria:
- `len_{100,200,300,500,1000,2000}_sigma{2,4,6,8,16,32}.txt` : 1 instancia por cada combinación length-sigma (35)
- `len_{100,200,300,500,1000,2000}_sigma{random}_1.txt` 1 instancia por cada length eligiendo aleatoriamente un sigma (7)
con un total de 42 instancias.


## Requisitos

- Compilador C++ con soporte para C++11 o superior
- Para análisis estadístico: R con paquete 'scmamp'

## Notas

- Todas las probabilidades utilizadas para la experimentación del articulo se encuentran disponibles en https://drive.google.com/drive/folders/11yOIscf7erpN0toJf6U-1c528Tc-cY1S?usp=sharing para utilizarlas solo debe descargar la carpeta de probabilidades y ejecutar el ./brkgallm con el parámetro -model {nombre de la carpeta}
