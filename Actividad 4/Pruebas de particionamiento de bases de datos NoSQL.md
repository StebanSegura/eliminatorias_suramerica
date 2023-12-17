# Documento de Casos de Prueba para Validar el Particionamiento

**Proyecto: Sistema de Gestión para Eliminatorias de Suramérica**

## 1. Introducción

Este documento establece los casos de prueba necesarios para validar la efectividad del particionamiento horizontal implementado en el Sistema de Gestión para las Eliminatorias de Suramérica. El objetivo es garantizar que el particionamiento cumple con los criterios de calidad especificados en los requerimientos no funcionales, incluyendo desempeño, escalabilidad y distribución equitativa de la carga.

## 2. Casos de Prueba

### 2.1 Verificación del Desempeño

#### Caso de Prueba 1: Respuesta Rápida a Consultas

**Objetivo:** Verificar que las consultas mantienen una respuesta rápida incluso bajo carga.

1. **Pasos:**
   - Ejecutar consultas frecuentes durante un periodo de alta carga simulada.
2. **Resultado Esperado:**
   - El tiempo de respuesta de las consultas se mantiene por debajo de los 500 ms en al menos el 95% de las solicitudes.

#### Caso de Prueba 2: Capacidad de Procesamiento

**Objetivo:** Evaluar la capacidad de procesamiento del sistema durante eventos de alto tráfico.

1. **Pasos:**
   - Simular operaciones de escritura intensiva y evaluar la capacidad del sistema para manejar al menos 1000 operaciones por segundo.
   - Realizar operaciones de lectura simultáneamente y verificar que el sistema atienda a 500 usuarios activos.
2. **Resultado Esperado:**
   - El sistema puede manejar la carga especificada sin degradación significativa del desempeño.

### 2.2 Validación del Particionamiento

#### Caso de Prueba 3: Distribución Equitativa de Datos

**Objetivo:** Confirmar que los datos se distribuyen equitativamente entre las particiones.

1. **Pasos:**
   - Analizar la distribución de documentos en las particiones.
2. **Resultado Esperado:**
   - Los documentos relacionados con equipos de diferentes países se distribuyen de manera equitativa entre las particiones.

#### Caso de Prueba 4: Escalabilidad

**Objetivo:** Verificar que al agregar nuevos nodos, se mejora linealmente el desempeño.

1. **Pasos:**
   - Agregar nuevos nodos shard al entorno.
   - Realizar operaciones de escritura y lectura y evaluar si la adición de nodos mejora el desempeño.
2. **Resultado Esperado:**
   - El sistema muestra una mejora lineal en el desempeño al agregar nuevos nodos shard.

## 3. Reporte de Resultados y Análisis

### 3.1 Resultados Generales

- Porcentaje de éxito en cada caso de prueba.
- Identificación de cualquier caso que no cumpla con los criterios de aceptación.

### 3.2 Análisis

- Observaciones sobre el desempeño y la escalabilidad durante la ejecución de los casos de prueba.
- Recomendaciones para ajustes o mejoras si es necesario.

