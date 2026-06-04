# 🏠 EnergyHome - Página de Inicio

## Descripción General del Proyecto

**EnergyHome** es una aplicación web moderna y robusta para registrar, analizar y visualizar el consumo energético de electrodomésticos en el hogar. Diseñada con una arquitectura cliente-servidor REST, permite a los usuarios monitorear su consumo de energía en tiempo real y recibir recomendaciones personalizadas para optimizar su uso.

### 🎯 Objetivo Principal

Proporcionar una herramienta intuitiva y eficiente que ayude a los usuarios a entender y reducir su consumo energético, contribuyendo a la sostenibilidad ambiental y el ahorro económico.

## ✨ Características Principales

- 🔐 **Autenticación Segura**: Registro e inicio de sesión con JWT y contraseñas cifradas
- 📱 **Dashboard Interactivo**: Visualización de consumo con gráficos y KPI en tiempo real
- ⚙️ **Gestión de Electrodomésticos**: Crear, editar, eliminar y listar dispositivos
- 📊 **Análisis de Consumo**: Cálculo automático de consumo mensual y generación de reportes
- 💡 **Recomendaciones Inteligentes**: Sugerencias personalizadas para optimizar el consumo
- 📡 **API RESTful Documentada**: Swagger integrado para fácil integración

## 🏗️ Arquitectura Técnica

EnergyHome sigue una arquitectura cliente-servidor bien definida con separación clara de responsabilidades:

### Stack Tecnológico

#### Frontend
- **React 19**: Framework de UI moderno
- **React Router**: Enrutamiento de aplicación
- **Axios**: Cliente HTTP
- **Material UI**: Componentes de diseño
- **Chart.js**: Visualización de datos
- **Vite**: Herramienta de construcción rápida

#### Backend
- **Node.js**: Entorno de ejecución
- **Express**: Framework web
- **JWT**: Autenticación
- **bcrypt**: Cifrado de contraseñas
- **Swagger**: Documentación API
- **Jest**: Testing

#### Base de Datos
- **PostgreSQL**: Base de datos relacional

#### DevOps
- **Docker**: Containerización
- **Docker Compose**: Orquestación de servicios
- **GitHub Actions**: CI/CD

## 📊 Composición del Repositorio

| Lenguaje | Porcentaje |
|----------|-----------|
| HTML | 76.2% |
| JavaScript | 21.7% |
| CSS | 1.2% |
| Otros | 0.9% |

## 📁 Estructura del Proyecto

```
DeploySistemaEnergetico/
├── frontend/          # Aplicación React
├── backend/           # Servidor Express
├── database/          # Scripts y esquema PostgreSQL
└── docs/              # Documentación API
```

## 🚀 Inicio Rápido

### Requisitos Previos
- Node.js (v16+)
- PostgreSQL (v12+)
- Docker y Docker Compose (opcional)

### Instalación Local
```bash
# Instalar dependencias
npm install

# Configurar base de datos
psql -h localhost -U postgres -d energyhome -f database/schema.sql

# Iniciar backend
npm run dev --workspace backend

# Iniciar frontend (en otra terminal)
npm run dev --workspace frontend
```

La aplicación estará disponible en `http://localhost:3000`

### Con Docker
```bash
docker compose up --build
```

- Frontend: http://localhost:3000
- Backend API: http://localhost:4000
- Swagger: http://localhost:4000/api-docs

## 📚 Documentación

- **[Guía de Instalación](Guía-de-Instalación)** - Configuración detallada
- **[Documentación de Características](Documentación-de-Características)** - Funcionalidades y endpoints
- **[Guía de Contribución](Guía-de-Contribución)** - Cómo contribuir al proyecto

## 🔐 Seguridad

- Contraseñas cifradas con bcrypt
- Autenticación basada en JWT
- Validación de datos en frontend y backend
- CORS configurado apropiadamente

## 📈 Fórmula de Cálculo de Consumo

$$
kWh = \frac{\text{potencia\_watts} \times \text{horas\_uso} \times 30}{1000}
$$

## 📝 Licencia

Este proyecto está bajo licencia abierta. Consulta el repositorio para más detalles.

## 👥 Contacto y Soporte

Para preguntas, reportar bugs o sugerir mejoras, abre un [issue](https://github.com/Sagamo-max/DeploySistemaEnergetico/issues) en el repositorio.

---

**¡Bienvenido a EnergyHome! 🌱**
