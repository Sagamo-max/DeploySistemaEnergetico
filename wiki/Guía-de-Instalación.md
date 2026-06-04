# 📦 Guía de Instalación

Esta guía te ayudará a instalar y configurar EnergyHome en tu ambiente local.

## 📋 Requisitos Previos

Asegúrate de tener instalados los siguientes componentes:

| Requisito | Versión Mínima | Descripción |
|-----------|----------------|------------|
| Node.js | v16.0+ | Entorno de ejecución JavaScript |
| npm | v8.0+ | Gestor de paquetes |
| PostgreSQL | v12+ | Base de datos relacional |
| Git | Cualquiera | Control de versiones |

**Opcionales (para Docker):**
- Docker (v20.10+)
- Docker Compose (v1.29+)

## 🔧 Instalación Local

### Paso 1: Clonar el Repositorio

```bash
git clone https://github.com/Sagamo-max/DeploySistemaEnergetico.git
cd DeploySistemaEnergetico
```

### Paso 2: Instalar Dependencias Globales

```bash
npm install
```

Esto instalará las dependencias para el workspace raíz y todos los paquetes configurados.

### Paso 3: Configurar Base de Datos

#### 3a. Crear la Base de Datos

```bash
createdb energyhome
```

O usando psql:

```bash
psql -U postgres -c "CREATE DATABASE energyhome;"
```

#### 3b. Aplicar el Esquema

```bash
psql -h localhost -U postgres -d energyhome -f database/schema.sql
```

**Tablas creadas:**
- `users` - Información de usuarios
- `appliances` - Electrodomésticos registrados
- `consumption_history` - Histórico de consumo

### Paso 4: Configurar Variables de Entorno

#### Backend (`.env` en la carpeta `backend/`)

```bash
# Puerto del servidor
PORT=4000

# Autenticación JWT
JWT_SECRET=tu-secreto-muy-seguro-aqui

# Configuración de PostgreSQL
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=postgres
DB_NAME=energyhome

# Ambiente
NODE_ENV=development
```

#### Frontend (`.env` en la carpeta `frontend/`)

```bash
# URL de la API backend
VITE_API_URL=http://localhost:4000/api

# Usar datos mock para desarrollo
VITE_USE_MOCKS=true
```

### Paso 5: Levantar el Backend

En una terminal, ejecuta:

```bash
npm run dev --workspace backend
```

Expected output:
```
Server running on port 4000
Database connected successfully
```

### Paso 6: Levantar el Frontend

En otra terminal, ejecuta:

```bash
npm run dev --workspace frontend
```

Expected output:
```
VITE v5.x.x  ready in 500 ms

➜  Local:   http://localhost:3000/
```

### ✅ Verificación de Instalación

1. Abre tu navegador en `http://localhost:3000`
2. Deberías ver la página de inicio de EnergyHome
3. Verifica que la API esté disponible en `http://localhost:4000/api-docs`

## 🐳 Instalación con Docker

### Opción Más Sencilla: Docker Compose

```bash
docker compose up --build
```

Esto levantará automáticamente:
- Frontend (React): http://localhost:3000
- Backend (Express): http://localhost:4000
- PostgreSQL: localhost:5432
- Swagger: http://localhost:4000/api-docs

### Parar los Servicios

```bash
docker compose down
```

### Reconstruir Imágenes

```bash
docker compose up --build --no-cache
```

## 🧪 Verificar la Instalación

### Backend

```bash
# Correr pruebas unitarias
npm run test --workspace backend

# Verificar linting
npm run lint --workspace backend
```

### Frontend

```bash
# Correr pruebas E2E
npm run test --workspace frontend

# Build de producción
npm run build --workspace frontend
```

## 📡 Prueba la API

### Registrar un Usuario

```bash
curl -X POST http://localhost:4000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "usuario@example.com",
    "password": "contraseña123"
  }'
```

### Iniciar Sesión

```bash
curl -X POST http://localhost:4000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "usuario@example.com",
    "password": "contraseña123"
  }'
```

### Obtener Perfil de Usuario

```bash
curl -X GET http://localhost:4000/api/users/profile \
  -H "Authorization: Bearer <token>"
```

## 🐛 Solución de Problemas

### Error: "Connection refused" a PostgreSQL

**Problema**: PostgreSQL no está corriendo
**Solución**:
```bash
# En macOS
brew services start postgresql

# En Linux
sudo systemctl start postgresql

# En Windows (cmd como administrador)
pg_ctl -D "C:\Program Files\PostgreSQL\14\data" start
```

### Error: "Port 3000 already in use"

**Solución**: Mata el proceso en el puerto
```bash
# En macOS/Linux
lsof -ti:3000 | xargs kill -9

# En Windows (PowerShell como admin)
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

### Error: "JWT_SECRET not defined"

**Solución**: Verifica que `.env` en `backend/` contiene:
```bash
JWT_SECRET=tu-secreto-aqui
```

### Base de datos no sincronizada

**Solución**: Reinicia la base de datos
```bash
dropdb energyhome
createdb energyhome
psql -h localhost -U postgres -d energyhome -f database/schema.sql
```

## 📚 Próximos Pasos

- Lee la [Documentación de Características](Documentación-de-Características) para entender todas las funcionalidades
- Consulta los [endpoints disponibles](Documentación-de-Características#-endpoints-principales)
- Revisa la [Guía de Contribución](Guía-de-Contribución) si deseas contribuir

## ✨ Tips Útiles

- Usa `npm run dev` en la raíz para levantar todo (si está configurado en monorepo)
- Activa el hot reload en desarrollo para cambios en tiempo real
- Consulta `docs/api/swagger.yaml` para la especificación completa de la API
- Las variables de entorno pueden variar según tu setup local

---

¿Necesitas ayuda? Abre un [issue](https://github.com/Sagamo-max/DeploySistemaEnergetico/issues) en el repositorio.
