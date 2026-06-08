# SPECS - AgentHub Admin Panel (Prototipo HTML)

## 1) Descripcion breve del producto

AgentHub es una plataforma para administrar agentes de IA y sus capacidades (skills), monitorear su operacion y gestionar contrataciones.

El usuario administrador de este panel es un operador interno de producto/operaciones que necesita:
- revisar metricas del negocio,
- gestionar usuarios y agentes,
- inspeccionar skills,
- consultar contratos,
- y analizar errores operativos.

## 2) Stack tecnologico y restricciones

- HTML5 semantico.
- Tailwind CSS via CDN.
- JavaScript vanilla (sin TypeScript obligatorio).
- Sin frameworks (React, Vue, Angular, Svelte, etc.).
- Sin backend ni llamadas a API.
- Sin base de datos ni persistencia; todos los datos hardcodeados en JS.
- Modo oscuro usando clase `dark` en `html` o contenedor raiz.

## 3) Especificaciones por seccion (6 vistas)

Regla global: cada requerimiento debe definir componente, contenido y comportamiento visual/interactivo.

### 3.1 Dashboard

1. Mostrar 4 tarjetas de metricas en grilla responsive 2x2 en desktop y 1x4 en mobile: ingresos del mes, perdida por descuentos, agentes activos, agentes fallando.
2. Cada tarjeta debe incluir icono, etiqueta, valor hardcodeado y color de acento distinto por tipo de metrica; la tarjeta activa al hover eleva sombra y desplaza 1-2px.
3. Debajo de las tarjetas, incluir un bloque de ancho completo con borde discontinuo titulado "Actividad semanal" como placeholder de grafico.
4. El bloque de actividad debe conservar proporcion minima visible (alto minimo) en mobile para evitar colapso visual.

### 3.2 Gestion de usuarios

1. Renderizar tabla con columnas: Nombre, Email, Plan, Estado, Acciones; minimo 6 filas hardcodeadas.
2. En Acciones, incluir dropdown por fila con al menos "Ver detalle" y "Eliminar"; al abrir un dropdown se cierran los demas.
3. "Ver detalle" debe abrir modal con datos completos del usuario seleccionado (nombre, email, plan, estado, fecha de alta).
4. El modal debe cerrar por boton, por click en backdrop y por tecla Escape.

### 3.3 Gestion de agentes

1. Renderizar lista o tabla de minimo 6 agentes con: nombre, propietario, estado, cantidad de skills y acciones.
2. Cada agente debe tener panel colapsable de skills (cerrado por defecto) con transicion suave en altura/opacidad.
3. El dropdown de acciones por agente debe incluir "Configurar" y "Eliminar".
4. "Configurar" abre modal que muestra el prompt de sistema hardcodeado del agente y un boton de cierre.

### 3.4 Skills

1. Incluir un bloque introductorio explicando que una skill es una capacidad reutilizable que amplía lo que un agente puede hacer.
2. Mostrar catalogo con minimo 8 skills; cada item incluye nombre, descripcion corta y contador de agentes que la usan.
3. Cada skill debe tener dropdown con acciones "Ver detalle" y "Eliminar".
4. "Ver detalle" abre modal con descripcion extendida, entradas esperadas y salida esperada de la skill.

### 3.5 Contrataciones de agentes

1. Mostrar tabla con minimo 6 contratos y columnas: Cliente, Agente, Skills contratadas, Fechas, Importe total, Acciones.
2. En cada fila, agregar dropdown con "Ver detalle".
3. "Ver detalle" abre modal con resumen del contrato, lista de skills incluidas y precio individual por skill.
4. El modal debe mostrar total final calculado (hardcodeado o suma en cliente) y estado del contrato (activo/finalizado).

### 3.6 Log de errores

1. Mostrar listado de minimo 10 errores con: timestamp, agente, tipo, descripcion breve, severidad y acciones.
2. La severidad debe verse con badge de color consistente: critico (rojo), warning (ambar), info (azul), resuelto (verde).
3. En Acciones, incluir dropdown con "Ver detalle" y "Marcar como resuelto".
4. "Ver detalle" abre modal con stack trace completo; "Marcar como resuelto" actualiza visualmente el badge del item.

## 4) Inventario de componentes reutilizables

- Sidebar persistente de navegacion.
- Topbar con titulo dinamico y toggle de modo oscuro.
- Tarjeta de metrica.
- Tabla responsive con scroll horizontal en viewport pequeno.
- Badge de estado/severidad.
- Dropdown de acciones con cierre por click fuera.
- Modal con backdrop y foco visible.
- Panel colapsable (accordion) para skills de agente.
- Botones primario/secundario/destructivo.

## 5) Criterios de aceptacion (verificables)

1. Existen 6 secciones navegables desde sidebar y solo una visible a la vez.
2. El toggle de modo oscuro cambia toda la UI (fondos, textos, bordes, tarjetas, tablas y modales).
3. Cada seccion cumple al menos 3 especificaciones concretas de esta SPECS.
4. Comportamiento interactivo - dropdown: abre por click, cierra por click fuera y solo uno puede estar abierto a la vez.
5. Comportamiento interactivo - modal: abre con accion contextual, cierra por boton, backdrop y Escape.
6. Comportamiento interactivo - colapsable: skills de agentes inician cerradas y se expanden/colapsan con transicion suave.
7. Comportamiento interactivo - modo oscuro: el estado del tema persiste durante la sesion (ej. en `localStorage`).
8. Todo el contenido se renderiza con datos hardcodeados locales sin backend.
9. La interfaz es usable en desktop y mobile (sin solapamientos criticos ni contenido inaccesible).

## 6) Nota de implementacion

Esta SPECS es la fuente de verdad del prototipo. La implementacion HTML debe seguir este documento en estructura, componentes e interacciones sin pedir aclaraciones adicionales.
