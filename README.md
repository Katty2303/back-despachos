\# Backend Despachos - SpringBoot



API REST desarrollada en Java Spring Boot para la gestión de despachos de ITPCARGO™.



\## Tecnologías

\- Java 17

\- Spring Boot 3.4.4

\- Spring Data JPA

\- MySQL 8

\- Docker (multi-stage build)

\- GitHub Actions (CI/CD)



\## Requisitos previos

\- Docker Desktop instalado

\- Java 17 o superior

\- Maven 3.9 o superior



\## Cómo ejecutar localmente



\### Con Docker Compose

```bash

docker compose up -d

```

La API estará disponible en: http://localhost:8081



\### Sin Docker

```bash

cd Springboot-API-REST-DESPACHO

mvn spring-boot:run

```



\## Variables de entorno

| Variable | Descripción | Valor por defecto |

|----------|-------------|-------------------|

| SPRING\_DATASOURCE\_URL | URL de conexión a MySQL | jdbc:mysql://localhost:3306/despachos\_db |

| SPRING\_DATASOURCE\_USERNAME | Usuario de la base de datos | appuser |

| SPRING\_DATASOURCE\_PASSWORD | Contraseña de la base de datos | - |

| SERVER\_PORT | Puerto del servidor | 8081 |



\## Endpoints disponibles

| Método | Ruta | Descripción |

|--------|------|-------------|

| GET | /api/v1/despachos | Listar todos los despachos |

| GET | /api/v1/despachos/{id} | Obtener despacho por ID |



\## Estructura del proyecto

back-Despachos\_SpringBoot/

├── Springboot-API-REST-DESPACHO/

│   ├── Dockerfile          # Multi-stage build (Maven builder + JRE)

│   └── src/                # Código fuente Spring Boot

├── docker-compose.yml      # Stack completo con MySQL

├── .dockerignore           # Archivos excluidos del build

└── .github/

└── workflows/

└── cicd-backend-despachos.yml  # Pipeline CI/CD



\## Pipeline CI/CD

El pipeline se activa automáticamente con cada push a la rama `deploy`:

1\. Construye la imagen Docker con Maven

2\. Publica en Docker Hub

3\. Despliega en EC2-App via SSH Jump (pasando por ec2-web)



\## Infraestructura AWS

\- \*\*EC2-App\*\*: Instancia privada (subred privada)

\- \*\*Puerto expuesto\*\*: 8081

\- \*\*Acceso\*\*: Solo desde ec2-web mediante Security Group



\## Persistencia de datos

Se utiliza un \*\*Named Volume\*\* de Docker (`dbdata\_despachos`) para persistir los datos de MySQL.

Esto garantiza que los datos no se pierden al reiniciar los contenedores.



\## Principios DevOps aplicados

\- \*\*Contenedorización\*\*: Dockerfile multi-stage con usuario no-root

\- \*\*CI/CD\*\*: Pipeline automatizado con GitHub Actions

\- \*\*Mínimo privilegio\*\*: Usuario `appuser` sin permisos root en BD y contenedor

\- \*\*Persistencia\*\*: Named Volume para datos críticos

\- \*\*Seguridad\*\*: Credenciales manejadas via GitHub Secrets

