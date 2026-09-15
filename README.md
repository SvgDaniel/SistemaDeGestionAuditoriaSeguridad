# Sistema de Gestión de Auditorías de Pentesting

[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-2.0+-D71100?style=for-the-badge&logo=sqlalchemy&logoColor=white)](https://www.sqlalchemy.org/)
[![OWASP](https://img.shields.io/badge/OWASP-Top_10:2025-000000?style=for-the-badge&logo=owasp&logoColor=white)](https://top10.owasp.org/2025/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

> Plataforma web centralizada para la gestión operativa, estandarización de hallazgos bajo **OWASP Top 10:2025**, almacenamiento de evidencias de solo lectura y generación consolidada de reportes en auditorías de seguridad informática.

---

## Tabla de Contenidos
- [Sobre el Proyecto](#-sobre-el-proyecto)
- [Problema que Resuelve](#-problema-que-resuelve)
- [Características Principales](#-características-principales)
- [Roles del Sistema](#-roles-del-sistema)
- [Arquitectura y Stack Tecnológico](#-arquitectura-y-stack-tecnológico)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Guía de Instalación y Despliegue](#-guía-de-instalación-y-despliegue)
- [Modelado y Diagramas (UML / ER)](#-modelado-y-diagramas-uml--er)
- [Metodología de Trabajo](#-metodología-de-trabajo)
- [Licencia](#-licencia)

---

## Sobre el Proyecto

El **Sistema de Gestión de Auditorías de Pentesting** es una solución web desarrollada en **Python** diseñada para empresas de consultoría de ciberseguridad[cite: 4, 10]. Permite controlar el ciclo de vida completo de las auditorías de seguridad[cite: 3, 4]: desde la creación y asignación de equipos, pasando por el registro normalizado de vulnerabilidades y la validación de evidencias, hasta la emisión automatizada de informes de cara al cliente[cite: 3, 4].

Este proyecto se desarrolla en el marco académico de la asignatura **Fundamentos de Ingeniería de Software**[cite: 11, 12].

---

## Problema que Resuelve

En las operaciones tradicionales de ciberseguridad, la falta de una herramienta unificada genera ineficiencias críticas[cite: 11, 12]:
- **Información Desorganizada y Dispersa:** Uso heterogéneo de herramientas (Word, Markdown, hojas de cálculo) por parte de cada Pentester[cite: 2, 11, 12].
- **Construcción Manual de Reportes:** Proceso propenso a errores al copiar, pegar y consolidar hallazgos manualmente[cite: 2, 11, 12].
- **Falta de Trazabilidad y Control:** Imposibilidad de consultar en tiempo real el estado global de auditorías activas o disponer de métricas históricas[cite: 2, 11, 12].

---

## Características Principales

- **Gestión Centralizada de Auditorías:** Creación, asignación de equipos y seguimiento por estados (`Sin asignar`, `Asignada`, `En curso`, `En revisión`, `Reporte Disponible`)[cite: 3, 4].
- **Taxonomía Estándar OWASP Top 10:2025:** Clasificación obligatoria de hallazgos mediante el catálogo oficial vigente[cite: 3, 4, 6].
- **Gestión Segura de Evidencias:** Carga de imágenes, logs, capturas de tráfico (PCAP) y pruebas de concepto (PoC) de hasta **10 MB**, almacenadas como **archivos de solo lectura** sin permisos de ejecución por seguridad[cite: 4].
- **Control de Calidad (QA) por el Líder:** Módulo para validar hallazgos, devolverlos con observaciones al Pentester o marcarlos como duplicados[cite: 3, 4].
- **Generación Automática de Reportes:** Compilación inmediata en PDF de auditorías cerradas con hallazgos validados[cite: 3, 4].
- **Historial e Inalterabilidad:** Bitácora inalterable de auditoría (quién hizo qué y cuándo)[cite: 4].

---

## Roles del Sistema

| Rol | Permisos y Responsabilidades Clave |
|---|---|
| **Líder de Auditoría** | Crea auditorías, asigna Pentesters, valida/devuelve hallazgos, genera reportes y consulta métricas[cite: 2, 3, 4]. |
| **Pentester** | Registra hallazgos en auditorías asignadas, adjunta evidencias y realiza correcciones[cite: 2, 3, 4]. |
| **Administrador** | Gestiona usuarios (alta, cambio de rol, desactivación) y audita la trazabilidad del sistema[cite: 2, 3, 4]. |
| **Cliente** | Consulta el estado de su auditoría en curso y descarga el reporte final publicado[cite: 2, 3, 4]. |

---

## Arquitectura y Stack Tecnológico

El sistema sigue una **Arquitectura en Capas (Layered Architecture / MVC)** para garantizar el desacoplamiento y la mantenibilidad[cite: 4, 12]:

- **Lenguaje:** Python 3.11+[cite: 4, 10]
- **Backend / Framework Web:** FastAPI (o Flask)[cite: 4, 12]
- **ORM / Persistencia:** SQLAlchemy 2.0+[cite: 4]
- **Base de Datos:** PostgreSQL / SQLite[cite: 4]
- **Seguridad & Auth:** Passlib (Hashing Bcrypt/Argon2 con *salt*), RBAC[cite: 4]
- **Motor de Reportes:** WeasyPrint / ReportLab[cite: 4]
- **Frontend / UI:** Jinja2 + HTML5 + TailwindCSS[cite: 4]

---

## Estructura del Repositorio

```text
gestion-auditorias-pentesting/
├── .github/                 # Workflows de integración continua (CI/CD)
├── docs/                    # Documentación de ingeniería de software
│   ├── 00_PROMPT_MAESTRO.md
│   ├── 01_ESTADO_PROYECTO.md
│   ├── 02_DECISIONES.md
│   ├── 03_CHECKPOINT.md
│   ├── 04_INVESTIGACION_METODOLOGIAS.md
│   ├── REFERENCIAS-FUENTES.md
│   └── diagrams/            # Fuentes de diagramas (Mermaid / PlantUML)
├── src/                     # Código fuente de la aplicación Python
│   ├── app/
│   │   ├── api/             # Controladores y rutas HTTP
│   │   ├── core/            # Configuración, seguridad y RBAC
│   │   ├── models/          # Modelos de entidad SQLAlchemy (ORM)
│   │   ├── services/        # Lógica de negocio (Hallazgos, Reportes, etc.)
│   │   └── templates/       # Vistas e interfaz gráfica (Jinja2 / HTML5)
│   └── main.py
├── storage/                 # Almacenamiento local protegido para evidencias (Solo Lectura)
├── tests/                   # Pruebas automatizadas (pytest)
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
