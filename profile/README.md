<div align="center">

  <!-- Si subes el logo al repositorio, reemplaza la URL de abajo por la ruta de tu imagen (ej. ./assets/logo.png) -->
  <h1>🥔 AgroVision Carchi</h1>
  <h3>Plataforma inteligente de monitoreo, diagnóstico fitosanitario y predicción comercial para el cultivo de papa</h3>

  <p>
    <img src="https://img.shields.io/badge/Estado-En%20An%C3%A1lisis%20(Bloque%201)-2D6A4F?style=for-the-badge" alt="Estado" />
    <img src="https://img.shields.io/badge/UCE-Arquitectura%20de%20Software-1B4332?style=for-the-badge" alt="Asignatura" />
    <img src="https://img.shields.io/badge/Paralelo-S7--P2-D97706?style=for-the-badge" alt="Curso" />
  </p>

  <p>
    <b>Universidad Central del Ecuador</b> • Facultad de Ingeniería y Ciencias Aplicadas (FICA)<br>
    <b>Docente:</b> Ing. Mario Morales
  </p>

  <p>
    <a href="https://agrovisionuce.atlassian.net/wiki/x/VoET">📚 Documentación en Confluence</a> •
    <a href="#-propuesta-de-valor">💡 Propuesta de Valor</a> •
    <a href="#-funcionalidades-por-rol">🚀 Funcionalidades</a> •
    <a href="#-enfoque-arquitectónico-y-stack">🏗️ Arquitectura</a> •
    <a href="#-equipo-de-proyecto">👥 Equipo</a>
  </p>

</div>

---

## 💡 Propuesta de Valor

> **No es un sistema transaccional de compra-venta.** **AgroVision Carchi** es una plataforma web de información, diagnóstico y predicción que acompaña todo el ciclo del cultivo de papa en la provincia del Carchi mediante **inteligencia artificial y datos abiertos**, conectando a productores y comerciantes con información confiable para tomar decisiones (los acuerdos comerciales se cierran fuera del sistema).

### 🎯 Tres Problemas Críticos que Resuelve

| Problemática en el Carchi | Impacto Actual | Solución con AgroVision Carchi |
| :--- | :--- | :--- |
| **1. Siembra a Ciegas** | Detección tardía de plagas (como la rancha) y desconocimiento de sobreoferta; pérdida de cosechas y caída de precios. | **Diagnóstico por foto con IA** y alertas tempranas de focos infecciosos cercanos. |
| **2. Precios Impuestos** | El productor vende sin referencia del mercado real; el intermediario fija el precio y reduce el margen del agricultor. | **Estimación de rendimiento** y semáforo de recomendación sobre cuándo conviene vender. |
| **3. Abastecimiento Incierto** | El comerciante mayorista no sabe dónde ni cuándo saldrá cosecha; compras improvisadas y rutas ineficientes. | **Mapa de oferta regional** y módulo de demanda planificada por variedad y semana. |

---

## 🚀 Funcionalidades por Rol

### 👨‍🌾 1. Rol Agricultor (Vendedor) — *App Web Responsive / Móvil*
* **🔬 Doctor IA (Diagnóstico por Foto):** Detección automática de enfermedades y plagas (*rancha, alternaria, fusarium*) en hojas o tubérculos con porcentaje de confianza, nivel de severidad y tratamiento técnico recomendado.
* **🗺️ Mi Lote (Cuaderno de Campo Digital):** Dibujo georreferenciado del terreno en el mapa y registro completo del ciclo (siembra, fumigaciones, costos y avances).
* **🔥 Mapa de Calor y Alertas Fitosanitarias:** Geolocalización colaborativa de diagnósticos y notificaciones preventivas según radio de cercanía y riesgo climático.
* **🌾 Estimación de Rendimiento y Recomendación de Venta:** Proyección de quintales a cosechar y cruce con la oferta regional para recomendar si vender ahora o esperar.
* **🛰️ Salud Satelital NDVI *(Fase Futura)*:** Monitoreo cromático del vigor del lote mediante imágenes satelitales.

### 🚚 2. Rol Comerciante Mayorista (Comprador) — *Panel Web de Abastecimiento*
* **📍 Inteligencia de Abastecimiento:** Mapa interactivo de dónde, cuándo y qué variedad de papa (*Superchola, Fripapa, Capiro, Única*) saldrá a cosecha para planificar compras y logística.
* **📋 Demanda Planificada:** Registro de intenciones de compra (tonelaje requerido por variedad, cantón y semana objetivo) que alimenta el motor predictivo de precios y muestra el porcentaje de cobertura en campo.

### 🧑‍🔬 3. Rol Técnico Agrícola (Validador) — *Consola Técnica y MLOps*
* **✅ Bandeja de Validación (*Human-in-the-Loop*):** Revisión de diagnósticos con baja confianza de la IA para confirmar o corregir la patología adjuntando una nota técnica.
* **📊 Estado del Modelo y Dataset:** Monitoreo de métricas de calidad (*F1-Score, Precisión, Recall*) y disparo del *pipeline* de reentrenamiento con las nuevas imágenes validadas.

---

## 🏗️ Enfoque Arquitectónico y Stack

AgroVision Carchi no es un CRUD tradicional; está diseñado como un ecosistema de subsistemas distribuidos:

| Subsistema / Funcionalidad | Estrategia y Reto Arquitectónico |
| :--- | :--- |
| **📸 Subida de fotos en campo** | Almacenamiento de objetos (**S3 / MinIO**), compresión en cliente y soporte **offline-first** para zonas rurales sin señal. |
| **🧠 Diagnóstico con IA** | Inferencia asíncrona mediante **colas de mensajería**; servicio de Machine Learning separado del API principal para no bloquear la app. |
| **🗺️ Mapas de calor** | Base de datos geoespacial (**PostGIS**) y generación dinámica de *tiles*. |
| **🔔 Alertas de foco** | Arquitectura orientada a eventos mediante patrón publicador/suscriptor (**Pub/Sub**). |
| **🌦️ Satélite y clima** | *Pipeline* de ingesta *batch* programada y resiliente. |
| **📈 Predicción comercial** | *Workers* de cómputo escalables para proyecciones de precios y cosecha. |
| **🔄 Validación experta** | Ciclo **MLOps** para versionado y reentrenamiento continuo del modelo. |

### 🌐 Fuentes de Datos Abiertos y Reales (APIs)
* **Sentinel Hub (Copernicus):** Imágenes satelitales e índice NDVI (plan académico gratuito).
* **Open-Meteo & NASA POWER:** Clima abierto (temperatura, heladas, precipitación y humedad).
* **SIPA – MAG:** Series históricas de precios del quintal de papa por variedad y mercado.
* **INEC – ESPAC:** Estadísticas oficiales de superficie sembrada y rendimiento por provincia.
* **Datos Propios:** Lotes georreferenciados, fotos diagnosticadas e intenciones de siembra y compra.

---

## 👥 Equipo de Proyecto

| Integrante | Rol Principal | Rol Secundario | Responsabilidad en Bloque 1 (Confluence) |
| :--- | :--- | :--- | :--- |
| **Kevin Tenorio** | Scrum Master | Product Owner / Analista de negocio | `0 · Inicio` y `1 · Problemática` |
| **Victor Cañar** | Backend | Ingeniero de datos / ML | `2 · Idea de negocio` |
| **Ricardo Chapi** | DevOps / QA | Arquitecto de software | Infraestructura Confluence, GitHub y entrega oficial |
| **Luis Paspuezán** | Diseñador UX/UI | Frontend | `3 · Actores y alcance`, `4 · Línea gráfica` y Figma |

---

## 🗂️ Estructura de Documentación (Bloque 1 – Confluence)

1. **`0 · Inicio`** — Ficha general del proyecto, roles, estado y enlaces.
2. **`1 · Problemática`** — Contexto actual del cultivo de papa en el Carchi y los 3 problemas centrales.
3. **`2 · Idea de negocio`** — Propuesta de valor, diferenciación arquitectónica y objetivos.
4. **`3 · Actores y alcance`** — Roles del sistema, corte vertical implementado, supuestos y restricciones.
5. **`4 · Línea gráfica`** — Identidad visual, paleta de colores, tipografías y plantillas de diagramas.

---

<div align="center">
  <sub>Desarrollado por el equipo de <b>AgroVision Carchi</b> • Universidad Central del Ecuador (2026)</sub>
</div>
