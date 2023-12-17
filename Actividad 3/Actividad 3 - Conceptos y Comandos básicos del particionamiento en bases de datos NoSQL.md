# Introducción: Sistema de Gestión para Eliminatorias de Suramérica

En el vibrante mundo del fútbol, donde la emoción y la competencia se entrelazan, surge la necesidad imperante de gestionar de manera eficiente la información relacionada con las Eliminatorias de Suramérica. Este documento establece los requisitos no funcionales para el desarrollo del Sistema de Gestión, una plataforma diseñada para facilitar la administración y organización de este emocionante evento deportivo. Con un enfoque en el desempeño, la redundancia y la escalabilidad, aspiramos a brindar una experiencia sin igual tanto para los entusiastas del fútbol como para los organizadores del torneo.

---

## Documento de Requerimientos No Funcionales - Desempeño y Particionamiento

### 1. Desempeño

#### 1.1 Criterios de Calidad

##### 1.1.1 Respuesta Rápida a Consultas

- **Objetivo:** Garantizar que las consultas a la base de datos tengan una respuesta rápida.
- **Criterios:**
  - El 95% de las consultas debe completarse en menos de 500 ms.
  - El tiempo de respuesta para operaciones críticas, como la actualización de resultados, no debe superar los 2 segundos.

##### 1.1.2 Capacidad de Procesamiento

- **Objetivo:** Manejar de manera eficiente la carga de trabajo del sistema durante eventos de alto tráfico.
- **Criterios:**
  - La base de datos debe ser capaz de manejar al menos 1000 operaciones de escritura por segundo.
  - La capacidad de lectura debe ser suficiente para atender simultáneamente a 500 usuarios activos.

##### 1.1.3 Escalabilidad

- **Objetivo:** Permitir el crecimiento del sistema sin degradación significativa del desempeño.
- **Criterios:**
  - Agregar nuevos nodos debe conducir a una mejora lineal en el desempeño.
  - El sistema debe escalar para manejar el doble de la carga actual al agregar recursos.

### 2. Particionamiento

#### 2.1 Escenario para Particionamiento

- **Descripción:** Se requerirá particionamiento horizontal de la base de datos en el escenario en que la cantidad de datos supera la capacidad de almacenamiento de un solo nodo o cuando se busca mejorar el rendimiento distribuyendo la carga entre varios nodos.
- **Indicadores:**
  - El tamaño total de la base de datos supera los límites de almacenamiento disponibles en un solo nodo.
  - Las consultas y operaciones de escritura muestran signos de degradación del desempeño debido a la carga excesiva en un solo nodo.

#### 2.2 Estrategia de Particionamiento

- **Tipo de Particionamiento:** Particionamiento Horizontal (Sharding)
- **Clave de Particionamiento:** Equipo o Grupo de Equipos (por país)

##### Criterios para la Clave de Particionamiento:

- Los datos relacionados con equipos de diferentes países se agruparán en la misma partición.
- Esto ayudará a distribuir la carga de manera equitativa y reducir la posibilidad de cuellos de botella en nodos específicos.

#### 2.3 Ejecución de Comandos para el Particionamiento

**A) Definir la Estrategia de Particionamiento:**

```bash
# Iniciar el nodo de configuración (Config Server)
mongod --configsvr --replSet configReplSet --bind_ip localhost:27019

# Iniciar los nodos shard
mongod --shardsvr --replSet shard1 --bind_ip localhost:27017
mongod --shardsvr --replSet shard2 --bind_ip localhost:27018
# ... Agregar más nodos shard según sea necesario

# Iniciar el router (mongos)
mongos --configdb configReplSet/localhost:27019 --bind_ip localhost:27020
