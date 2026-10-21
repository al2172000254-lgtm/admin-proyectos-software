# 1. Evolución de los modelos de lenguaje

## ¿Qué es un modelo de lenguaje?

Un modelo de lenguaje (*Language Model*, LM) es un sistema capaz de estimar la probabilidad de una secuencia de texto y, en los modelos autorregresivos, predecir el siguiente *token* a partir del contexto anterior. Un token puede representar una palabra, una parte de ella o un símbolo. Durante el entrenamiento con grandes cantidades de datos, estos modelos aprenden patrones estadísticos y relaciones lingüísticas que les permiten generar texto coherente.

## La evolución hacia los LLM (*Large Language Models*)

La evolución hacia los modelos de lenguaje grandes (*Large Language Models*, LLM) se vio impulsada por los avances en las arquitecturas neuronales, la disponibilidad de grandes conjuntos de datos y el incremento de la capacidad de cómputo. Un avance decisivo fue la arquitectura *Transformer*, presentada en 2017, que facilitó el entrenamiento de modelos a gran escala mediante mecanismos de atención.

Al aumentar el tamaño de los modelos, la cantidad de datos de entrenamiento y los recursos computacionales, fue posible desarrollar sistemas con miles de millones de parámetros, capaces de procesar contextos extensos, generar texto y realizar tareas diversas, como resumir documentos, traducir idiomas y escribir código. Sin embargo, el aumento de escala no garantiza por sí solo la precisión ni la capacidad de razonamiento en todas las tareas.

## Modelos con razonamiento explícito

Más recientemente, han surgido modelos diseñados para dedicar cómputo adicional a la resolución de problemas antes de producir una respuesta final. Entre los ejemplos se encuentran los modelos de razonamiento de OpenAI y DeepSeek-R1. A diferencia de un sistema que genera una respuesta directamente, estos modelos pueden utilizar procesos de razonamiento en varios pasos para abordar tareas complejas.

**¿De dónde proviene esta capacidad?** No depende únicamente del tamaño del modelo, sino también de técnicas de entrenamiento y de la asignación de recursos computacionales durante la inferencia. Entre los mecanismos relevantes se encuentran:

1. **Aprendizaje por refuerzo (*Reinforcement Learning*, RL):** se optimiza el comportamiento del modelo mediante señales de recompensa asociadas con la calidad de sus resultados. En determinadas tareas, esto puede favorecer estrategias de resolución de problemas más eficaces.
2. **Cómputo adicional durante la inferencia (*Test-time Compute*):** se asignan recursos computacionales adicionales cuando el modelo responde a una consulta. Esto permite explorar o desarrollar soluciones más elaboradas antes de generar la respuesta final.

Estas técnicas pueden mejorar el desempeño en determinadas tareas de razonamiento, aunque sus resultados dependen del modelo, del método de entrenamiento y del problema que se busca resolver.
