---
title: Heterocedasticidad
date: 2025-09-09 10:00 +0100
categories: [Data Science, Estadística]
tags: [heterocedasticidad, preprocesamiento, etl, ciencia-de-datos, big-data, estadística]
author: Norberto Ruiz
---

## Heterocedasticidad: qué es, cómo detectarla y cómo corregirla en regresión

Este artículo forma parte de la serie “Preprocesamiento de Datos con Enfoque Estadístico”, cuyo objetivo es aportar las bases conceptuales y prácticas que muchas veces se pasan por alto en procesos ETL y de análisis de datos. Aunque hoy en día abundan las herramientas para mover, transformar y almacenar datos, no siempre se tienen en cuenta los supuestos estadísticos que garantizan que los resultados sean válidos. En esta serie repasaremos, paso a paso, cómo preparar los datos con rigor para que los modelos y conclusiones sean fiables.

### ¿Qué es la heterocedasticidad?

En un modelo de regresión lineal asumimos que los errores (la diferencia entre lo que predice el modelo y lo que observamos en la realidad) tienen varianza constante para todos los valores de las variables explicativas. A este supuesto se le llama homocedasticidad.

Cuando esta condición no se cumple y la varianza de los errores cambia sistemáticamente a lo largo de las observaciones, hablamos de heterocedasticidad.

Un ejemplo intuitivo:
- Imagina que analizamos la relación entre nivel de ingresos y gasto en ocio.
- A bajos niveles de ingresos, las diferencias de gasto entre individuos son pequeñas.
- A altos niveles de ingresos, las diferencias crecen mucho: hay personas que gastan modestamente y otras que gastan en exceso.
- En ese caso, la dispersión de los errores del modelo no es constante: tenemos heterocedasticidad.

### ¿Por qué es un problema?

La heterocedasticidad no invalida los coeficientes estimados por mínimos cuadrados ordinarios (OLS): siguen siendo insesgados. El verdadero problema está en la precisión de las estimaciones:

- Los errores estándar de los coeficientes resultan incorrectos.
- Como consecuencia, las pruebas de significación (t de Student, F de Snedecor) y los intervalos de confianza dejan de ser fiables.
- Esto puede llevarnos a creer que una variable es significativa cuando no lo es, o a subestimar la incertidumbre del modelo.

En términos sencillos: la heterocedasticidad no estropea la media del estimador, pero sí su fiabilidad para hacer inferencias.

### ¿Cómo detectar la heterocedasticidad?
#### 1. Métodos gráficos
Son la primera herramienta de diagnóstico:
- Gráfico de residuos vs valores ajustados: si la nube de puntos tiene forma de abanico (varianza creciente o decreciente), sospechamos heterocedasticidad.
- Residuos absolutos o al cuadrado vs variable explicativa: la tendencia creciente o decreciente es otro indicador.

#### 2. Test estadísticos
Existen pruebas formales que permiten verificar la hipótesis nula de homocedasticidad:

- Test de Breusch–Pagan: evalúa si la varianza de los errores está relacionada con los regresores.

- Test de White: más general, no requiere especificar la forma de la heterocedasticidad.

- Test de Goldfeld–Quandt: útil cuando sospechamos que la varianza cambia con el tamaño de una variable en particular.

En la práctica, se suele comenzar con gráficos y luego confirmar con uno o varios de estos tests.

###Ejemplo aplicado (simplificado)

Supongamos que estimamos un modelo de regresión lineal para predecir el consumo energético de los hogares en función de su renta.

1. Ajustamos el modelo y calculamos los residuos.

2. Al graficar residuos vs renta, vemos un patrón en abanico: a mayor renta, mayor dispersión en los errores.

3. Aplicamos el test de Breusch–Pagan y obtenemos un p-valor menor a 0.05 → rechazamos la hipótesis de homocedasticidad.

4. Concluimos que hay heterocedasticidad y debemos corregirla para realizar inferencias fiables.

### ¿Cómo corregirla o mitigarla?

Existen varias estrategias, que pueden aplicarse según el contexto:

1. Transformaciones de variables
- Aplicar logaritmos, raíces cuadradas u otras transformaciones reduce la dispersión relativa.
- En el ejemplo de ingresos, modelar log(renta) suele estabilizar la varianza.

2. Errores estándar robustos
- También llamados “de White”. Corrigen la estimación de la varianza sin modificar los coeficientes.
- Es la solución más común cuando la forma de la heterocedasticidad no es conocida.

3. Mínimos Cuadrados Ponderados (WLS)
- Si conocemos o podemos estimar la forma de la heterocedasticidad, podemos asignar pesos inversamente proporcionales a la varianza de los errores.
- Esto devuelve eficiencia a los estimadores.

4. Redefinición del modelo
- A veces la heterocedasticidad surge por omitir variables relevantes. Incluirlas puede mejorar el ajuste y estabilizar la varianza.

### Conexión con otros supuestos de la regresión

La heterocedasticidad es solo una de las condiciones necesarias para confiar en un modelo de regresión. Junto a ella encontramos:
- Linealidad de la relación entre variables.
- Independencia de los errores (sin autocorrelación).
- Normalidad de los errores, necesaria para ciertas inferencias.
- Ausencia de multicolinealidad entre explicativas.

Comprender cómo se relacionan estos supuestos nos ayuda a tener una visión más amplia: no se trata solo de ajustar un modelo, sino de validar que sus conclusiones son sólidas.

### Conclusión

La heterocedasticidad es un fenómeno común en datos económicos, financieros y sociales. Aunque no invalida los coeficientes, sí afecta directamente la credibilidad de nuestras conclusiones. Detectarla y corregirla es parte esencial del preprocesamiento estadístico y del buen uso de la regresión lineal.

En este artículo hemos visto qué es, cómo detectarla y cómo tratarla. En próximos textos de la serie continuaremos explorando otros problemas frecuentes en los datos y cómo solucionarlos con un enfoque estadístico riguroso.

\#heterocedasticidad \#preprocesamiento \#etl \#ciencia-de-datos \#big-data \#estadística 
