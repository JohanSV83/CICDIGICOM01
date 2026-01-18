<div align="center">

# Comercio Digital Ventas & Ingresos en medios anuncios digitales   ETL Pipeline
### Arquitectura Medallion en Azure Databricks

[![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)](https://databricks.com/)
[![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=for-the-badge&logo=apache-spark&logoColor=white)](https://spark.apache.org/)
[![Delta Lake](https://img.shields.io/badge/Delta_Lake-00ADD8?style=for-the-badge&logo=delta&logoColor=white)](https://delta.io/)
[![Databricks Dashboards](https://img.shields.io/badge/Databricks Dashboards-F2C81?style=for-the-badge&logo=databricks&logoColor=black)](https://databricks.com/)
[![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)](https://github.com/features/actions)

*Pipeline de Analisis de Ventas y/o Ingresos en Medios Digitales desde en punto de Ventas comercio digital  con arquitectura de tres capas y despliegue continuo*

</div>

---

## 🎯 Descripción

Pipeline ETL enterprise-grade que extrae desde un origen de base de datos relacional en nube azure sqldatabase y transforma para realizar una analisis de Ventas y/o Ingresos en los Medios digitales musicales a travez de los distintos productos (Anuncios, publicidad en medios digitales como diarios digital y/o medios musicales)  **Arquitectura Medallion** (Bronze-Silver-Gold) en Azure Databricks con **CI/CD completo** y **Delta Lake** para garantizar consistencia ACID.

### ✨ Características Principales

- 🔄 **ETL Automatizado** - Pipeline completo con despliegue automático via GitHub Actions
- 🏗️ **Arquitectura Medallion** - Separación clara de capas Bronze → Silver → Gold
- 📊 **Modelo Dimensional** - Star Schema optimizado para análisis de negocio
- 🚀 **CI/CD Integrado** - Deploy automático en cada push a master
- 📈 **Databricks Dashboards** - Visualización
- ⚡ **Delta Lake** - ACID transactions y time travel capabilities
- 🔔 **Monitoreo** - Notificaciones automáticas y logs detallados

---

## 🏛️ Arquitectura

### Flujo de Datos

```
📄 Enpoint Azure sql database (db-datacom)
    ↓
🥉 Bronze Layer (Ingesta sin transformación)
    ↓
🥈 Silver Layer (Limpieza + Modelo Dimensional)
    ↓
🥇 Gold Layer (Tabla final desnormalizada Analisis comercio Dígital)
    ↓
📊 Databricks Dashboards (Visualización)
```

![image alt]https://github.com/JohanSV83/CICDIGICOM01/blob/a57494cf4cceed8cc3ab174b36a6b5357ee6e94f/Seguridad/Arquitectura.jpg


### 📦 Capas del Pipeline

<table>
<tr>
<td width="33%" valign="top">

#### 🥉 Bronze Layer
**Propósito**: Zona de aterrizaje

**Tablas**: 
- `atalog_comercial.bronze.cliente` 
- `catalog_comercial.bronze.cobertura` 
- `catalog_comercial.bronze.medio`
- `catalog_comercial.bronze.tipo_medio` 
- `catalog_comercial.bronze.producto`
- `catalog_comercial.bronze.tipo_producto`
- `catalog_comercial.bronze.ejecutivo`
- `catalog_comercial.bronze.ejecutivo_digital`
- `catalog_comercial.bronze.grupo_laboral`
- `catalog_comercial.bronze.contrato`
- `catalog_comercial.bronze.condicion_pago`
- `catalog_comercial.bronze.forma_factura`
- `catalog_comercial.bronze.tipo_venta`
- `catalog_comercial.bronze.pedido`
- `catalog_comercial.bronze.pedido_detalle`
- `catalog_comercial.bronze.orden`
- `catalog_comercial.bronze.orden_detalle`

**Características**:
- ✅ Datos tal como vienen de origen
- ✅ Timestamp de ingesta
- ✅ Preservación histórica
- ✅ Sin validaciones

</td>
<td width="33%" valign="top">

#### 🥈 Silver Layer
**Propósito**: Modelo dimensional

**Tablas**:
- `catalog_comercial.silver.cliente`
- `catalog_comercial.silver.ejecutivo`
- `catalog_comercial.silver.ejecutivo_digital`
- `catalog_comercial.silver.tipo_medio`
- `catalog_comercial.silver.medio`
- `catalog_comercial.silver.producto`
- `catalog_comercial.silver.tipo_producto`
- `catalog_comercial.silver.grupo_laboral`
- `catalog_comercial.silver.tipo_venta`
- `catalog_comercial.silver.cobertura`
- `catalog_comercial.silver.condicion_pago`
- `catalog_comercial.silver.contrato`
- `catalog_comercial.silver.forma_factura`
- `catalog_comercial.silver.pedido`
- `catalog_comercial.silver.pedido_detalle`
- `catalog_comercial.silver.orden`
- `catalog_comercial.silver.orden_detalle`


**Características**:
- ✅ Star Schema
- ✅ Datos normalizados
- ✅ Validaciones completas

</td>
<td width="33%" valign="top">

#### 🥇 Gold Layer
**Propósito**: Analytics-Comercial Digital

**Tablas**:
- `catalog_comercial.golden.ordenes_digitales`        : tabla desnormalizada para analisis de Ventas de Ventas / Ingresos en medios digitales (Anuncios, banner, video, display, content, contenido, etc)


**Características**:
- ✅ Pre-agregados
- ✅ Optimizado para BI
- ✅ Performance máximo
- ✅ Actualizaciones automáticas

</td>
</tr>
</table>

---

## 📁 Estructura del Proyecto

```
etl-apple/
│
├── 📂 .github/
│   └── 📂 workflows/
│       └── 📄 cicd_dev_to_prod.yml   # Pipeline CI/CD deploy a certification workspace databricks
├── 📂 procesos/
│   ├── 🐍 Preparacion_com_ambiente.ipynb           # Bronze layer
│   ├── 🐍 ingestion_com_data.ipynb              # Bronze Layer
│   ├── 🐍 cleaning_com_data.ipynb          # Silver Layer
│   ├── 🐍 transform_com_data.ipynb       # Silver Layer
│   └── 🐍 kpi_com_data.ipynb               # Gold Layer
├── 📂 scrips/
|   ├── 🐍 Preparacion_com_ambiente.ipynb    # Create Schema, Tables, External location
├── 📂 seguridad/
|   ├── 🐍 Seguridad/permisos_external_invite_group.ipynb               # Sql Grant
├── 📂 reversion/
|   ├── 🐍 reversion/revoke_external_invite_group.ipynb               # Revoke permissions
├── 📂 dashboards/                 # dashboards/Ingresos Comercial Por Medios Digitales.lvdash.json dashboards/Ingresos_Digitales.jpg 
└── 📄 README.md
```

---

## 🛠️ Tecnologías

<div align="center">

| Tecnología | Propósito |
|:----------:|:----------|
| ![Databricks](https://img.shields.io/badge/Azure_Databricks-FF3621?style=flat-square&logo=databricks&logoColor=white) | Motor de procesamiento distribuido Spark |
| ![Delta Lake](https://img.shields.io/badge/Delta_Lake-00ADD8?style=flat-square&logo=delta&logoColor=white) | Storage layer con ACID transactions |
| ![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=flat-square&logo=apache-spark&logoColor=white) | Framework de transformación de datos |
| ![ADLS](https://img.shields.io/badge/ADLS_Gen2-0078D4?style=flat-square&logo=microsoft-azure&logoColor=white) | Data Lake para almacenamiento persistente |
| ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white) | Automatización CI/CD |
| ![Databricks Dashboards](https://img.shields.io/badge/Databricks Dashboards-F2C81?style=for-the-badge&logo=databricks&logoColor=black) |  Visualización |

</div>

---

## ⚙️ Requisitos Previos

- ☁️ Cuenta de Azure con acceso a Databricks
- ☁️ Servicio azure sql Database
- 💻 Workspace de Databricks configurado
- 🖥️ Cluster activo (nombre: `Cluster1`)
- 🐙 Cuenta de GitHub con permisos de administrador
- 📦 Azure Data Lake Storage Gen2 configurado
- 📊 Power BI Desktop (opcional para visualización)

---

## 🚀 Instalación y Configuración

### 1️⃣ Clonar el Repositorio

```bash
git clone https://github.com/JohanSV83/CICDIGICOM01.git
cd CICDIGICOM01
```

### 2️⃣ Configurar Databricks Token

1. Ir a Databricks Workspace
2. **User Settings** → **Developer** → **Access Tokens**
3. Click en **Generate New Token**
4. Configurar:
   - **Comment**: `GitHub CI/CD`
   - **Lifetime**: `90 days`
5. ⚠️ Copiar y guardar el token

### 3️⃣ Configurar GitHub Secrets

En tu repositorio: **Settings** → **Secrets and variables** → **Actions**

| Secret Name | Valor Ejemplo |
|------------|---------------|
| `DATABRICKS_HOST` | `https://adb-xxxxx.azuredatabricks.net` |
| `DATABRICKS_TOKEN` | `dapi_xxxxxxxxxxxxxxxx` |

### 4️⃣ Tener conexion a origen al servicio  AZURE SQL DATABASE developer

```Notebook
conexion a azure sql database con las credenciales del servicio como :
servidor : srv-datacom.database.windows.net
enpoint
driver='com.microsoft.sqlserver.jdbc.SQLServerDriver'
database : db-datacom
puerto : ****
password :****
username:sqladmin
servername='srv-datacom.database.windows.net'
databasename='db-datacom'
```

<div align="center">

✅ **¡Configuración completa!**

</div>

---

## 💻 Uso

### 🔄 Despliegue Automático (Recomendado)

```bash
git add .
git commit -m "✨ feat: mejoras en pipeline"
git push origin master
```

**GitHub Actions ejecutará**:
- 📤 Deploy de notebooks a `/proyecto_digicom`
- 🔧 Creación del workflow `WF_ADB`
- ▶️ Ejecución completa:  Bronze → Silver → Gold
- 📧 Notificaciones de resultados



### 🔧 Ejecución Local en Databricks

Navegar a `/Production/ETL-APPLE` y ejecutar en orden:

```
- Preparacion_com_ambiente.py         → Crear esquema , esquemas, tablas y eliminacion de parquets de cada datalake bronze, silver y golden
- ingestion_com_data.py                → Bronze Layer
- cleaning_com_data.py                   → Silver Layer
- transform_com_data.py                   → Silver Layer
- procesos/kpi_com_data.py                   → Golden Layer

```

---


## 🔄 CI/CD

### Pipeline de GitHub Actions

```yaml
Workflow: Deploy ETL Apple Sales And Warranty
├── Deploy notebooks → /Production/ETL-APPLE
├── Eliminar workflow antiguo (si existe)
├── Buscar cluster configurado
├── Crear nuevo workflow con 5 tareas
├── Ejecutar pipeline automáticamente
└── Monitorear y notificar resultados
```

### 🔄  Workflow Databricks
![Texto descriptivo](CICDGICOM.png)
```
⏰ Schedule: on demand AM (Lima)
 🔒 Max concurrent runs: 1
⏰ Notificaciones: 
      success: johanvillano83@gmail.com
      failed:  johanvillano83@gmail.com
```

---

## 📈 Dashboards
https://github.com/JohanSV83/CICDIGICOM01/tree/main/dashboards

## 🔍 Monitoreo

### En Databricks

**Workflows**:
- Ir a **Workflows** en el menú lateral
- Buscar `WF_ADB`
- Ver historial de ejecuciones

**Logs por Tarea**:
- Click en una ejecución específica
- Click en cada tarea para ver logs detallados
- Revisar stdout/stderr en caso de errores

### En GitHub Actions

- Tab **Actions** del repositorio
- Ver historial de workflows
- Click en ejecución específica para detalles
- Revisar logs de cada step

---

## 👤 Autor

<div align="center">

### Johan Hernan Sanchez Villano

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/johan-hernan-sanchez-villano-a4082492/)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/JohanSV83)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:isc.johanvillano83@gmail.com)

**Data Engineering** | **Azure Databricks** | **Delta Lake** | **CI/CD**

</div>

---

copyrigth JOHAN HERNAN SANCHEZ VILLANO
---

<div align="center">

**Proyecto**: Data Engineering - Arquitectura Medallion  
**Tecnología**: Azure Databricks + Delta Lake + CI/CD  
**Última actualización**: 2026


</div>
