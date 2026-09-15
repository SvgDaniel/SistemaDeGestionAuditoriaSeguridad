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
---

## Sobre el Proyecto

El **Sistema de Gestión de Auditorías de Pentesting** es una solución web desarrollada en **Python** diseñada para empresas de consultoría de ciberseguridad. Permite controlar el ciclo de vida completo de las auditorías de seguridad: desde la creación y asignación de equipos, pasando por el registro normalizado de vulnerabilidades y la validación de evidencias, hasta la emisión automatizada de informes de cara al cliente.

Este proyecto se desarrolla en el marco académico de la asignatura **Fundamentos de Ingeniería de Software**.

---

## Problema que Resuelve

En las operaciones tradicionales de ciberseguridad, la falta de una herramienta unificada genera ineficiencias críticas:
- **Información Desorganizada y Dispersa:** Uso heterogéneo de herramientas (Word, Markdown, hojas de cálculo) por parte de cada Pentester.
- **Construcción Manual de Reportes:** Proceso propenso a errores al copiar, pegar y consolidar hallazgos manualmente.
- **Falta de Trazabilidad y Control:** Imposibilidad de consultar en tiempo real el estado global de auditorías activas o disponer de métricas históricas.

---

## Características Principales

- **Gestión Centralizada de Auditorías:** Creación, asignación de equipos y seguimiento por estados (`Sin asignar`, `Asignada`, `En curso`, `En revisión`, `Reporte Disponible`).
- **Taxonomía Estándar OWASP Top 10:2025:** Clasificación obligatoria de hallazgos mediante el catálogo oficial vigente.
- **Gestión Segura de Evidencias:** Carga de imágenes, logs, capturas de tráfico (PCAP) y pruebas de concepto (PoC) de hasta **10 MB**, almacenadas como **archivos de solo lectura** sin permisos de ejecución por seguridad.
- **Control de Calidad (QA) por el Líder:** Módulo para validar hallazgos, devolverlos con observaciones al Pentester o marcarlos como duplicados.
- **Generación Automática de Reportes:** Compilación inmediata en PDF de auditorías cerradas con hallazgos validados.
- **Historial e Inalterabilidad:** Bitácora inalterable de auditoría (quién hizo qué y cuándo).

---

## Roles del Sistema

| Rol | Permisos y Responsabilidades Clave |
|---|---|
| **Líder de Auditoría** | Crea auditorías, asigna Pentesters, valida/devuelve hallazgos, genera reportes y consulta métricas. |
| **Pentester** | Registra hallazgos en auditorías asignadas, adjunta evidencias y realiza correcciones. |
| **Administrador** | Gestiona usuarios (alta, cambio de rol, desactivación) y audita la trazabilidad del sistema. |
| **Cliente** | Consulta el estado de su auditoría en curso y descarga el reporte final publicado. |

---

## Arquitectura y Stack Tecnológico

El sistema sigue una **Arquitectura en Capas (Layered Architecture / MVC)** para garantizar el desacoplamiento y la mantenibilidad:

- **Lenguaje:** Python 3.11+
- **Backend / Framework Web:** FastAPI (o Flask)
- **ORM / Persistencia:** SQLAlchemy 2.0+
- **Base de Datos:** PostgreSQL / SQLite
- **Seguridad & Auth:** Passlib (Hashing Bcrypt/Argon2 con *salt*), RBAC
- **Motor de Reportes:** WeasyPrint / ReportLab
- **Frontend / UI:** Jinja2 + HTML5 + TailwindCSS

---
## Prototipo Figma
<img width="1870" height="991" alt="Screenshot 2026-09-15 at 18-46-34 Gestion de auditorias – Figma Make" src="https://github.com/user-attachments/assets/568a0bc8-020a-4058-ac29-926046867a6a" />
## Estructura del Repositorio

```text
gestion-auditorias-pentesting/
├── .github/                 # Workflows de integración continua (CI/CD)
├── docs/                    # Documentación de ingeniería de software
│   ├── 01_INVESTIGACION_METODOLOGIAS.pdf
│   ├── 02_QUESTIONARIO.pdf
│   ├── 03_HISTORIAS_DE_USUARIO.pdf
│   ├── 04_REQUERIMIENTOS_FUNCIONALES_Y_NO_FUNCIONALES.pdf
│   └── diagrams/            
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
