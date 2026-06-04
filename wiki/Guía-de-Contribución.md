# 🤝 Guía de Contribución

¡Gracias por tu interés en contribuir a EnergyHome! Esta guía te explica cómo puedes ayudar a mejorar el proyecto.

## 📖 Índice

- [Códigos de Conducta](#-código-de-conducta)
- [Cómo Contribuir](#-cómo-contribuir)
- [Flujo de Trabajo](#-flujo-de-trabajo)
- [Estándares de Código](#-estándares-de-código)
- [Pruebas](#-pruebas)
- [Documentación](#-documentación)
- [Pull Requests](#-pull-requests)
- [Reportar Bugs](#-reportar-bugs)
- [Sugerir Mejoras](#-sugerir-mejoras)

---

## 👥 Código de Conducta

Nos comprometemos a proporcionar un ambiente inclusivo y respetuoso. Esperamos que todos los contribuyentes:

- Respeten a otros contribuyentes
- Cuestionen ideas, no personas
- Busquen el consenso en las decisiones
- Reconozcan y celebren la diversidad
- Sean abiertos y considerados en crítica constructiva

Cualquier comportamiento inapropiado puede resultar en exclusión del proyecto.

---

## 🚀 Cómo Contribuir

Hay muchas formas de contribuir a EnergyHome:

### 1. 🐛 Reportar Bugs
Encuentra y reporta problemas que encuentres durante el uso.

### 2. 💡 Sugerir Mejoras
Propón nuevas características o mejoras a las existentes.

### 3. 📝 Mejorar Documentación
Ayuda a escribir, actualizar o traducir la documentación.

### 4. 💻 Escribir Código
Implementa nuevas características o soluciona bugs existentes.

### 5. 🧪 Escribir Pruebas
Aumenta la cobertura de tests y mejora la calidad.

### 6. 🎨 Mejorar UI/UX
Sugiere y implementa mejoras de diseño e interfaz.

---

## 🔄 Flujo de Trabajo

### Para Principiantes

```
1. Fork del repositorio
   ↓
2. Clonar tu fork localmente
   ↓
3. Crear rama con nombre descriptivo
   ↓
4. Hacer cambios
   ↓
5. Escribir tests (si aplica)
   ↓
6. Actualizar documentación
   ↓
7. Commit con mensaje claro
   ↓
8. Push a tu fork
   ↓
9. Crear Pull Request
   ↓
10. Responder a reviews
```

### Paso a Paso

#### 1️⃣ Fork el Repositorio

En GitHub, haz clic en el botón "Fork" en la esquina superior derecha.

#### 2️⃣ Clonar tu Fork

```bash
git clone https://github.com/TU_USUARIO/DeploySistemaEnergetico.git
cd DeploySistemaEnergetico
```

#### 3️⃣ Agregar Remote Upstream

```bash
git remote add upstream https://github.com/Sagamo-max/DeploySistemaEnergetico.git
```

#### 4️⃣ Crear una Rama

```bash
# Actualizar la rama develop local
git fetch upstream
git checkout develop
git rebase upstream/develop

# Crear rama para tu cambio
git checkout -b feature/descripcion-del-cambio
```

**Convención de nombres:**
- `feature/nueva-funcionalidad` - Para nuevas características
- `fix/descripcion-del-bug` - Para corrección de bugs
- `docs/descripcion` - Para cambios de documentación
- `refactor/descripcion` - Para refactorización
- `test/descripcion` - Para tests

#### 5️⃣ Hacer tus Cambios

Edita los archivos necesarios. Asegúrate de:
- Seguir los estándares de código
- Escribir código limpio y legible
- Agregar comentarios cuando sea necesario

#### 6️⃣ Escribir Pruebas

```bash
# Backend
npm run test --workspace backend

# Frontend
npm run test --workspace frontend
```

#### 7️⃣ Actualizar Documentación

Si tu cambio afecta la funcionalidad, actualiza:
- `README.md`
- Archivos relevantes en `wiki/`
- Swagger (si es un endpoint)

#### 8️⃣ Commit con Mensaje Claro

```bash
git add .
git commit -m "feat: agregar validación de email en registro"
```

**Formato de commit:**
```
<tipo>(<scope>): <descripción>

<cuerpo opcional>

<pie opcional>
```

**Tipos válidos:**
- `feat`: Nueva característica
- `fix`: Corrección de bug
- `docs`: Cambios en documentación
- `style`: Cambios de formato (sin lógica)
- `refactor`: Refactorización de código
- `test`: Agregar o actualizar tests
- `chore`: Cambios en configuración

**Ejemplos:**
```bash
git commit -m "feat(auth): agregar recuperación de contraseña"
git commit -m "fix(api): corregir error 500 en endpoint de consumo"
git commit -m "docs: actualizar guía de instalación para Docker"
```

#### 9️⃣ Push a tu Fork

```bash
git push origin feature/descripcion-del-cambio
```

#### 🔟 Crear Pull Request

1. Ve a tu fork en GitHub
2. Haz clic en "Compare & pull request"
3. Rellena la plantilla de PR (ver abajo)
4. Haz clic en "Create pull request"

---

## 📐 Estándares de Código

### JavaScript/TypeScript

```javascript
// ✅ Bueno
const calculateConsumption = (watts, hours) => {
  return (watts * hours * 30) / 1000;
};

// ❌ Evitar
function calc(w, h) {
  return w * h * 30 / 1000;
}
```

**Reglas:**
- Usar `const` por defecto, `let` si es necesario
- Nombres descriptivos en inglés
- Máximo 80-100 caracteres por línea
- Usar arrow functions para callbacks
- Comentar lógica compleja

### React

```jsx
// ✅ Bueno
const ConsumptionChart = ({ data, isLoading }) => {
  if (isLoading) return <LoadingSpinner />;
  
  return (
    <div className="chart-container">
      <Chart data={data} />
    </div>
  );
};

// ❌ Evitar
const Chart = (props) => {
  return <div>{props.data.map(d => <p>{d}</p>)}</div>;
};
```

**Reglas:**
- Componentes como functional components
- Props con destructuring
- Manejo de loading y error states
- Usar custom hooks para lógica reutilizable

### Backend (Express)

```javascript
// ✅ Bueno
router.post('/appliances', authenticateToken, async (req, res) => {
  try {
    const { name, power_watts } = req.body;
    
    if (!name || !power_watts) {
      return res.status(400).json({ error: 'Missing required fields' });
    }
    
    const appliance = await Appliance.create(req.user.id, name, power_watts);
    res.status(201).json(appliance);
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: 'Internal server error' });
  }
});

// ❌ Evitar
router.post('/appliances', (req, res) => {
  Appliance.create(req.body).then(a => res.json(a));
});
```

**Reglas:**
- Usar async/await en lugar de callbacks
- Validar entrada en cada endpoint
- Retornar códigos HTTP apropiados
- Manejar errores explícitamente
- Loguear errores para debugging

### CSS/Styling

```css
/* ✅ Bueno */
.consumption-card {
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 20px;
  border-radius: 8px;
  background-color: var(--color-surface);
}

/* ❌ Evitar */
.card {
  margin: 10px;
  padding: 10px 10px;
  border: 1px solid #ccc;
}
```

**Reglas:**
- Usar variables CSS para colores y tamaños
- Nombres descriptivos en snake-case
- Respetar el sistema de diseño
- Mobile-first approach

---

## 🧪 Pruebas

### Backend (Jest)

```javascript
describe('Appliance Service', () => {
  describe('calculateConsumption', () => {
    it('should calculate consumption correctly', () => {
      const result = calculateConsumption(1000, 8);
      expect(result).toBe(240); // (1000 * 8 * 30) / 1000
    });

    it('should return 0 for 0 watts', () => {
      const result = calculateConsumption(0, 8);
      expect(result).toBe(0);
    });
  });
});
```

### Frontend (Jest/React Testing Library)

```javascript
import { render, screen } from '@testing-library/react';
import ConsumptionChart from './ConsumptionChart';

describe('ConsumptionChart', () => {
  it('renders chart with data', () => {
    const data = [{ date: '2026-01-01', kwh: 10 }];
    render(<ConsumptionChart data={data} />);
    
    expect(screen.getByTestId('chart')).toBeInTheDocument();
  });

  it('shows loading spinner while loading', () => {
    render(<ConsumptionChart isLoading={true} />);
    
    expect(screen.getByRole('status')).toBeInTheDocument();
  });
});
```

**Requisitos:**
- Mínimo 80% de cobertura de código
- Tests unitarios para funciones críticas
- Tests de integración para flows principales
- Tests E2E para casos de uso críticos

---

## 📚 Documentación

### Actualizar README.md

Si tu cambio añade nueva funcionalidad:

```markdown
## New Feature

Description of what it does.

### Usage

```javascript
example code
```

### Configuration

Any needed config or environment variables.
```

### Agregar a Wiki

Para cambios significativos, actualiza la wiki correspondiente:
- Documentación de Características
- Guía de Instalación
- etc.

### Swagger/OpenAPI

Si agregas un endpoint, documéntalo en `docs/api/swagger.yaml`:

```yaml
/api/appliances:
  post:
    summary: Create appliance
    tags:
      - Appliances
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            properties:
              name:
                type: string
              power_watts:
                type: integer
    responses:
      201:
        description: Appliance created
      400:
        description: Bad request
```

---

## 📋 Pull Requests

### Plantilla de PR

```markdown
## Descripción

Explica qué cambios hace este PR y por qué.

## Tipo de Cambio

- [ ] Bug fix
- [ ] Nueva característica
- [ ] Breaking change
- [ ] Cambios de documentación

## Cómo se probó

Describe cómo probaste tus cambios:

```
Pasos de prueba:
1. ...
2. ...
```

## Checklist

- [ ] Mi código sigue los estándares de código del proyecto
- [ ] He actualizado la documentación
- [ ] He agregado tests para nuevas características
- [ ] Todos los tests pasan localmente
- [ ] No hay warnings en la consola

## Screenshots (si aplica)

Adjunta screenshots de cambios en UI.
```

### Durante el Review

- Respeta el feedback
- Haz cambios en la misma rama
- Usa `git push --force-with-lease` si necesitas reescribir historia
- Responde preguntas del reviewer

### Después de la Aprobación

El maintainer hará merge cuando todas las condiciones se cumplan:
- ✅ Todos los tests pasan
- ✅ Mínimo 1 aprobación
- ✅ Rama actualizada con main
- ✅ Sin conflictos

---

## 🐛 Reportar Bugs

### Antes de reportar

1. Verifica que el bug aún exista
2. Busca en issues si ya fue reportado
3. Revisa la documentación
4. Intenta reproducirlo en desarrollo

### Cómo reportar

Ve a [Issues](https://github.com/Sagamo-max/DeploySistemaEnergetico/issues) y haz clic en "New issue".

**Información requerida:**
- Título descriptivo
- Descripción clara del problema
- Pasos para reproducir
- Comportamiento esperado
- Comportamiento actual
- Entorno (OS, navegador, versión Node.js, etc.)
- Logs o screenshots

**Ejemplo:**

```markdown
## Título
La gráfica de consumo no se actualiza al agregar nuevo dispositivo

## Descripción
Cuando creo un nuevo electrodoméstico desde el dashboard, 
la gráfica de consumo no refleja los datos del nuevo dispositivo 
hasta recargar la página.

## Pasos para reproducir
1. Iniciar sesión
2. Ir a Dashboard
3. Crear nuevo dispositivo
4. Observar la gráfica

## Esperado
La gráfica debe actualizarse automáticamente

## Actual
La gráfica se queda igual hasta F5

## Entorno
- OS: macOS 13.5
- Navegador: Chrome 115
- Node.js: v18.17.0
```

---

## 💡 Sugerir Mejoras

### Tipos de Sugerencias

- **Nuevas características**: Funcionalidad completamente nueva
- **Mejoras**: Cambios a funcionalidad existente
- **Cambios de UX**: Mejoras a interfaz
- **Performance**: Optimizaciones

### Cómo sugerir

Ve a [Discussions](https://github.com/Sagamo-max/DeploySistemaEnergetico/discussions) o abre un issue con el label `enhancement`.

**Incluye:**
- Descripción clara de la idea
- Caso de uso
- Posible implementación (opcional)
- Mockups o ejemplos (si aplica)

---

## 🔄 Mantener tu Fork Actualizado

```bash
# Traer cambios del upstream
git fetch upstream

# Rebase tu rama de desarrollo
git rebase upstream/develop

# Push a tu fork
git push origin develop
```

---

## 📞 Obtener Ayuda

- **Preguntas**: Abre una Discusssion
- **Bugs**: Abre un Issue
- **Ideas**: Abre una Discusssion
- **Chat**: Comenta en PRs relevantes

---

## 🎉 Gracias

¡Gracias por contribuir a EnergyHome! Tu ayuda hace que el proyecto sea mejor para todos.

Algunas de las mejores contribuciones:
- 🐛 Reportar bugs
- 📝 Mejorar documentación
- 🧪 Escribir tests
- 🎨 Mejorar diseño
- 💻 Implementar características

---

## 📞 Licencia

Al contribuir, aceptas que tu código sea publicado bajo la misma licencia que el proyecto.

---

**¡Feliz contribuyendo! 🚀**
