# NY-Trips-to-CosmosDB

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=flat-square&logo=python&logoColor=white)
![Azure Functions](https://img.shields.io/badge/Azure_Functions-2.0+-0062AD?style=flat-square&logo=azure-functions&logoColor=white)
![Azure Cosmos DB](https://img.shields.io/badge/Azure_Cosmos_DB-SQL_API-0078D4?style=flat-square&logo=microsoft-azure&logoColor=white)

## Descripcion

Proyecto de practica que demonstra el uso de Azure Functions para procesar datos de viajes de Nueva York y almacenarlos en Azure Cosmos DB. El objetivo es aprender y experimentar con arquitecturas serverless en Azure, gestionando datos de manera eficiente en una base de datos NoSQL.

Este proyecto consume un dataset publico de viajes de Nueva York (NYC Taxi Data) y lo carga en Cosmos DB para su posterior analisis y consultas.

## Arquitectura

```
+------------------+     +-------------------+     +------------------+
|                  |     |                   |     |                  |
|  Dataset NYC     | --> |  Azure Functions  | --> |  Azure Cosmos DB |
|  Trips (CSV)     |     |  (Trigger/Timer)  |     |  (SQL API)       |
|                  |     |                   |     |                  |
+------------------+     +-------------------+     +------------------+
```

### Componentes

- **Azure Functions**: Procesa y transforma los datos de viajes de manera serverless
- **Azure Cosmos DB**: Almacena los documentos de viajes en formato JSON
- **Python**: Lenguaje principal para la logica de procesamiento

## Como Funciona

1. **Ingestion**: La funcion Azure se ejecuta automaticamente mediante un trigger (HTTP, Timer o Blob)
2. **Lectura**: Se leen los datos del dataset de viajes de NYC desde la fuente configurada
3. **Transformacion**: Los datos se transforman y validan segun el esquema definido
4. **Persistencia**: Cada viaje se guarda como un documento JSON en Cosmos DB
5. **Monitoreo**: Los logs y metricas se envian a Application Insights

## Tecnologias Utilizadas

| Tecnologia | Version | Proposito |
|------------|---------|-----------|
| Python | 3.8+ | Lenguaje de programacion |
| Azure Functions | v2 | Computo serverless |
| Azure Cosmos DB | SQL API | Base de datos NoSQL |
| Azure SDK | Latest | Cliente de Cosmos DB |

## Requisitos Previos

- Python 3.8 o superior
- Azure Functions Core Tools
- Una cuenta de Azure con suscripcion activa
- Azure Cosmos DB Emulator (para desarrollo local) o cuenta de Cosmos DB en Azure
- Azure Storage Emulator (opcional, para desarrollo local)

## Como Ejecutar

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/NY-trips-to-cosmosdb.git
cd NY-trips-to-cosmosdb
```

### 2. Crear un entorno virtual e instalar dependencias

```bash
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Configurar las variables de entorno

Crea un archivo `local.settings.json` con la siguiente estructura:

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_WORKER_RUNTIME": "python",
    "COSMOS_DB_CONNECTION_STRING": "tu-string-de-conexion-de-cosmos-db"
  }
}
```

### 4. Ejecutar localmente

```bash
func start
```

La funcion se ejecutara en `http://localhost:7071`.

### 5. Desplegar en Azure

```bash
func azure functionapp publish <nombre-de-tu-function-app>
```

## Estructura del Proyecto

```
NY-trips-to-cosmosdb/
├── README.md
├── requirements.txt
├── host.json
└── <nombre-funcion>/
    ├── __init__.py
    ├── function.json
    └── __init__.py
```

## Contribuir

Los contribuciones son bienvenidas. Por favor, abre un issue primero para discutir los cambios que te gustaria realizar.

## Licencia

Este proyecto esta bajo la licencia MIT. Consulta el archivo LICENSE para mas detalles.
