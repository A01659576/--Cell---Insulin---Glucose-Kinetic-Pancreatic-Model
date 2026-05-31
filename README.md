# Modelo Cinético Pancreático Célula-Insulina-Glucosa

Este repositorio contiene el desarrollo y análisis de un modelo matemático para el estudio de la dinámica entre células pancreáticas, insulina y glucosa. El trabajo se divide en varias fases, cada una documentada en archivos Jupyter Notebook y MATLAB.

## Estructura del repositorio

- **Fase2_Code.ipynb**: Notebook de Python donde se realiza la verificación de cálculos numéricos, obtención de puntos de equilibrio y análisis del Jacobiano del sistema.
- **Phase4.ipynb**: Notebook de Python dedicado al análisis de estabilidad de los puntos de equilibrio usando el criterio de Hurwitz-Routh y el cálculo de autovalores del Jacobiano.
- **Diagrama_Global.md**: Código y explicación en MATLAB para la simulación y visualización del diagrama global del sistema, incluyendo trayectorias y puntos de equilibrio.
- **README.md**: Este archivo.

## Descripción de las fases principales

### Fase 2
- Cálculo de puntos de equilibrio del sistema célula-insulina-glucosa.
- Análisis simbólico y numérico del Jacobiano en cada punto de equilibrio.
- Obtención de autovalores para determinar la estabilidad local.

### Fase 3
- Simulación numérica del sistema usando MATLAB y Python
- Visualización de trayectorias en el espacio de fases (G, I, β).

### Fase 4
- Evaluación de la estabilidad de los puntos de equilibrio mediante el criterio de Hurwitz-Routh.
- Análisis de los signos de los coeficientes del polinomio característico.
- Discusión sobre la influencia de parámetros libres en la estabilidad.


## Autores
- Paulina Leal Mosqueda A01659576
- Santiago Nava Figueroa A01174557
- Carlo Crivelli Hernández A01656171
- Ricardo Villareal Bazán A01666859

## Requisitos
- Python 3.x con las librerías: numpy, sympy, matplotlib (para notebooks de Python).
- MATLAB (para simulaciones y visualizaciones en Diagrama_Global.md).
