# 🐾 Sistema de Turnos — Veterinaria

Aplicación web para la **gestión de turnos online** de una veterinaria, desarrollada como trabajo para la materia **Taller de Ingeniería de Software**.

Permite a los clientes registrarse, iniciar sesión y reservar turnos de veterinaria o estética para sus mascotas, eligiendo profesional, fecha y horario disponible. Los administradores cuentan con un panel de gestión de turnos y usuarios.

---

## 🚀 Funcionalidades

### Usuario cliente
- Registro e inicio de sesión
- Reserva de turnos seleccionando servicio, tipo, profesional, fecha y horario
- Visualización y cancelación de sus propios turnos
- Validación de disponibilidad de horarios en tiempo real

### Administrador
- Panel de administración exclusivo
- Visualización de todos los turnos por fecha
- Gestión de usuarios registrados

---

## 🏗️ Arquitectura

El proyecto es una **Single Page Application (SPA)** sin backend, que utiliza `localStorage` para persistir los datos en el navegador.

```
├── index.html              # Única página HTML — contiene todas las vistas
├── src/
│   ├── app.js              # Capa de UI: formularios, eventos, renderizado
│   └── core/
│       └── reservas.js     # Módulo core: lógica de negocio, validaciones, datos
├── tests/
│   └── reservas.test.js    # Tests unitarios con Jest
└── styles.css              # Estilos del sitio
```

---

## 🧠 Módulo core — `reservas.js`

Encapsula toda la lógica de negocio como un objeto JavaScript con las siguientes responsabilidades:

**Gestión de usuarios**
- `registrarUsuario()` — registro con validaciones de email, teléfono y contraseña
- `iniciarSesion()` — autenticación por email y password
- `cerrarSesion()` — limpieza de sesión activa
- `estaLogueado()` — verificación de sesión actual

**Gestión de turnos**
- `crearTurno()` — creación con validación de cédula, fecha, hora y disponibilidad
- `obtenerTurnosPorUsuario()` — turnos del usuario logueado
- `obtenerTurnosPorFecha()` — turnos del día para el panel admin
- `obtenerHorariosDisponibles()` — horarios libres filtrando los ya reservados

**Validaciones**
- `validarEmail()` — formato con regex
- `validarPassword()` — mínimo 6 caracteres
- `validarTelefono()` — solo números, mínimo 8 dígitos
- `validarCedula()` — solo números, 7 u 8 dígitos
- `validarFecha()` — no pasada, no fin de semana, máximo 2 meses a futuro
- `validarHora()` — dentro del rango de atención (09:00 a 17:30)

**Persistencia**
- `cargarDesdeStorage()` / `guardarEnStorage()` — sincronización con `localStorage`

---

## 🧪 Testing

El proyecto incluye **tests unitarios** con **Jest** para el módulo core:

```
tests/
└── reservas.test.js
```

Casos cubiertos:
- Validación de emails válidos e inválidos
- Validación de contraseñas y teléfonos
- Generación de horarios (18 slots de 09:00 a 17:30)
- Rechazo de fechas pasadas, fines de semana y fechas a más de 2 meses

Para correr los tests:
```bash
npm test
```

---

## 🛠️ Tecnologías

- **HTML5 / CSS3** — estructura y estilos
- **JavaScript (ES5/ES6)** — lógica del sitio sin frameworks
- **localStorage** — persistencia de datos en el cliente
- **Jest** — testing unitario
- **Patrón:** SPA con router de vistas manual

---

## 👨‍💻 Autor

- [SebaaFischel](https://github.com/SebaaFischel)
