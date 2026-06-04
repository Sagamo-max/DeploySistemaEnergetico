# 📖 Documentación de Características

Descripción detallada de todas las funcionalidades y endpoints disponibles en EnergyHome.

## 🎯 Características Principales

### 1. 🔐 Autenticación y Autorización

#### Registro de Usuario
- **Descripción**: Crear una nueva cuenta de usuario
- **Requisitos**:
  - Email válido
  - Contraseña con al menos 8 caracteres
  - Confirmación de contraseña
- **Seguridad**:
  - Las contraseñas se cifran con bcrypt
  - Validación de email duplicado

#### Inicio de Sesión
- **Descripción**: Autenticarse en la aplicación
- **Retorna**: Token JWT válido por 24 horas
- **Seguridad**: Validación de credenciales contra contraseña cifrada

#### Renovación de Token
- **Descripción**: Obtener un nuevo token sin volver a ingresar credenciales
- **Requisito**: Token válido pero próximo a expirar

---

### 2. 👤 Gestión de Perfil de Usuario

#### Obtener Perfil
- **Descripción**: Recuperar información del usuario autenticado
- **Datos incluidos**:
  - Email
  - Fecha de creación
  - Preferencias (idioma, unidades, etc.)
  - Última actualización

#### Actualizar Perfil
- **Descripción**: Modificar información personal del usuario
- **Campos actualizables**:
  - Nombre completo
  - Teléfono
  - Dirección
  - Preferencias de notificación

#### Cambiar Contraseña
- **Descripción**: Actualizar la contraseña del usuario
- **Requisitos**:
  - Contraseña actual
  - Nueva contraseña (diferente)
  - Confirmación de nueva contraseña

---

### 3. ⚙️ Gestión de Electrodomésticos

#### Crear Electrodoméstico
- **Descripción**: Registrar un nuevo dispositivo en la cuenta
- **Datos requeridos**:
  - Nombre del dispositivo
  - Tipo (refrigerador, lavadora, TV, aire acondicionado, etc.)
  - Potencia en watts
  - Marca y modelo
- **Datos opcionales**:
  - Año de compra
  - Ubicación en el hogar
  - Notas

#### Listar Electrodomésticos
- **Descripción**: Obtener todos los dispositivos del usuario
- **Filtros disponibles**:
  - Por tipo de dispositivo
  - Por estado (activo/inactivo)
  - Por rango de potencia
- **Paginación**: Soportada para grandes listas

#### Obtener Detalles de Dispositivo
- **Descripción**: Información completa de un electrodoméstico específico
- **Incluye**:
  - Datos básicos
  - Histórico de consumo
  - Promedio de uso mensual
  - Recomendaciones aplicables

#### Actualizar Electrodoméstico
- **Descripción**: Modificar datos de un dispositivo
- **Campos actualizables**:
  - Nombre
  - Potencia
  - Estado (activo/inactivo)
  - Ubicación

#### Eliminar Electrodoméstico
- **Descripción**: Remover un dispositivo de la cuenta
- **Nota**: El histórico de consumo asociado se preserva para análisis

---

### 4. 📊 Análisis de Consumo

#### Registrar Consumo
- **Descripción**: Crear un registro de consumo para un dispositivo
- **Datos requeridos**:
  - Horas de uso
  - Fecha
  - Notas opcionales
- **Cálculo automático**: 
  ```
  kWh = (potencia_watts × horas_uso × 30) / 1000
  ```

#### Obtener Histórico de Consumo
- **Descripción**: Consumo detallado de un dispositivo
- **Filtros**:
  - Por rango de fechas
  - Por mes/año
  - Agrupación (diaria, semanal, mensual)
- **Salida**: Gráficos y datos crudos

#### Resumen de Consumo
- **Descripción**: Vista general del consumo total
- **Incluye**:
  - Consumo total del mes (kWh)
  - Consumo por dispositivo
  - Consumo por tipo de dispositivo
  - Comparativa mes anterior
  - Estimación de costo mensual

#### Tendencias y Análisis
- **Descripción**: Análisis temporal del consumo
- **Métricas**:
  - Picos de consumo
  - Patrones de uso
  - Variación mes a mes
  - Proyecciones mensuales

---

### 5. 💡 Recomendaciones Inteligentes

#### Generar Recomendaciones
- **Descripción**: Sugerencias personalizadas para reducir consumo
- **Basadas en**:
  - Patrones de uso
  - Tipo de electrodoméstico
  - Comparativa con promedios de uso

#### Ejemplos de Recomendaciones
- "Tu TV está encendida más de 6 horas diarias. Considerar reducir el tiempo de visualización"
- "Tu refrigerador consume 120 kWh/mes. Verifica que las puertas cierren correctamente"
- "Tu aire acondicionado podría ser más eficiente. Considera usar termostato programable"
- "Has optimizado tu consumo un 15% respecto al mes anterior. ¡Continúa así!"

#### Seguimiento de Recomendaciones
- **Descripción**: Marcar recomendaciones como aplicadas o ignoradas
- **Beneficio**: Mejora la precisión de futuras recomendaciones

---

### 6. 📈 Dashboard e Informes

#### Dashboard Principal
- **Widgets incluidos**:
  - KPI: Consumo total del mes
  - Gráfico: Consumo diario (últimos 30 días)
  - Top 5: Dispositivos con mayor consumo
  - Alerta: Desviación respecto a mes anterior
  - Recomendaciones principales

#### Gráficos Disponibles
- **Línea**: Evolución temporal de consumo
- **Barras**: Comparativa entre dispositivos
- **Pie**: Distribución de consumo por tipo
- **Área**: Consumo acumulativo

#### Exportar Informes
- **Formatos**: PDF, CSV, JSON
- **Contenido**:
  - Resumen ejecutivo
  - Gráficos
  - Histórico detallado
  - Recomendaciones
- **Periodicidad**: Mensual, trimestral, anual

---

## 🌐 Endpoints Principales

### Autenticación

```
POST   /api/auth/register              Registrar usuario
POST   /api/auth/login                 Iniciar sesión
POST   /api/auth/refresh               Renovar token
POST   /api/auth/logout                Cerrar sesión
```

### Usuarios

```
GET    /api/users/profile              Obtener perfil
PUT    /api/users/profile              Actualizar perfil
POST   /api/users/password              Cambiar contraseña
```

### Electrodomésticos

```
GET    /api/appliances                 Listar dispositivos
POST   /api/appliances                 Crear dispositivo
GET    /api/appliances/:id             Obtener detalles
PUT    /api/appliances/:id             Actualizar dispositivo
DELETE /api/appliances/:id             Eliminar dispositivo
```

### Consumo

```
GET    /api/consumption                Obtener histórico
POST   /api/consumption                Registrar consumo
GET    /api/consumption/summary        Resumen mensual
GET    /api/consumption/:id            Consumo por dispositivo
```

### Recomendaciones

```
GET    /api/recommendations            Obtener recomendaciones
PUT    /api/recommendations/:id        Marcar como aplicada
DELETE /api/recommendations/:id        Ignorar recomendación
```

### Informes

```
GET    /api/reports/monthly            Informe mensual
GET    /api/reports/custom             Informe personalizado
```

---

## 📋 Modelos de Datos

### Usuario

```json
{
  "id": "uuid",
  "email": "usuario@example.com",
  "password_hash": "bcrypt_hash",
  "full_name": "Juan Pérez",
  "created_at": "2026-01-01T00:00:00Z",
  "updated_at": "2026-06-04T00:00:00Z",
  "settings": {
    "language": "es",
    "timezone": "America/Buenos_Aires",
    "currency": "ARS"
  }
}
```

### Electrodoméstico

```json
{
  "id": "uuid",
  "user_id": "uuid",
  "name": "Aire Acondicionado Livingroom",
  "type": "air_conditioning",
  "power_watts": 3500,
  "brand": "Samsung",
  "model": "2026",
  "location": "Livingroom",
  "active": true,
  "created_at": "2026-01-15T00:00:00Z",
  "notes": "Unidad principal"
}
```

### Consumo

```json
{
  "id": "uuid",
  "appliance_id": "uuid",
  "date": "2026-06-04",
  "hours_used": 8,
  "kwh_consumed": 28.0,
  "notes": "Día caluroso",
  "created_at": "2026-06-04T00:00:00Z"
}
```

---

## 🔄 Flujos de Negocio Principales

### Flujo 1: Nuevo Usuario

```
1. Registrarse (nombre, email, contraseña)
   ↓
2. Verificar email
   ↓
3. Iniciar sesión
   ↓
4. Tutorial onboarding
   ↓
5. Crear primer electrodoméstico
   ↓
6. Ver dashboard vacío (sin histórico)
```

### Flujo 2: Análisis Mensual

```
1. Sistema recopila datos de consumo diario
   ↓
2. Calcular totales mensuales automáticamente
   ↓
3. Generar recomendaciones basadas en patrones
   ↓
4. Alertar al usuario si consumo > promedio
   ↓
5. Mostrar comparativa mes anterior
```

### Flujo 3: Optimización de Consumo

```
1. Usuario revisa recomendaciones
   ↓
2. Aplica cambios (reduce horas de uso, etc)
   ↓
3. Sistema registra nuevo consumo
   ↓
4. Calcular impacto (ahorro en kWh y costo)
   ↓
5. Felicitar al usuario por progreso
```

---

## 🔐 Seguridad y Validaciones

### Validaciones de Entrada

- **Email**: RFC 5322 compliant
- **Contraseña**: Mín. 8 caracteres, al menos 1 número y 1 mayúscula
- **Potencia**: 1-10000 watts
- **Horas de uso**: 0-24 horas/día
- **Fechas**: Formato ISO 8601

### Autorizaciones

- Los usuarios solo acceden a sus propios datos
- No hay acceso cruzado entre cuentas
- Tokens JWT con expiración

---

## 📚 Documentación OpenAPI

La especificación completa está disponible en:

- **Archivo YAML**: `/docs/api/swagger.yaml`
- **Interfaz interactiva**: `http://localhost:4000/api-docs` (en desarrollo)

Puedes probar todos los endpoints directamente desde Swagger.

---

¿Necesitas más detalles? Consulta el [repositorio](https://github.com/Sagamo-max/DeploySistemaEnergetico) o abre un issue.
