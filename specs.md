# Especificación funcional y técnica - Prototipo HTML del panel de administración de AgentHub

## 1) Objetivo del entregable

Construir un prototipo frontend estático (sin backend ni API) del panel de administración interno de AgentHub, pensado como referencia de producto y base de implementación futura.

Este documento define qué construir, cómo debe comportarse y qué reglas de UI/UX seguir para que otro desarrollador (humano o agente de código IA) pueda implementarlo desde cero sin ambigüedades.

## 2) Alcance

Incluido en alcance:

- Una interfaz de administración con navegación lateral persistente.
- Barra superior con toggle global de tema claro/oscuro.
- Seis secciones de contenido:
	- Dashboard.
	- Gestión de usuarios.
	- Gestión de agentes.
	- Skills.
	- Contrataciones de agentes.
	- Log de errores.
- Componentes interactivos en frontend puro:
	- Dropdowns de acciones por fila/tarjeta.
	- Modales con backdrop.
	- Expand/collapse de skills por agente con transición suave.
- Datos 100% hardcodeados para demo.

Fuera de alcance:

- Integración con APIs, autenticación real, persistencia o base de datos.
- Filtros avanzados, paginación real o exportación de datos.
- Gestión real de permisos/roles (solo representación visual).

## 3) Stack y restricciones de implementación

- HTML5 semántico.
- Tailwind CSS vía CDN de navegador.
- JavaScript vanilla para interacciones.
- Sin frameworks (React/Vue/etc.).
- Sin librerías externas adicionales para modales/dropdowns.
- Diseño responsive (desktop first, usable en mobile).
- Modo oscuro implementado con utilidades dark: de Tailwind mediante clase dark en el elemento root.

## 4) Arquitectura de layout

### 4.1 Estructura general

- Contenedor raíz de pantalla completa (min-h-screen).
- Sidebar izquierda fija/persistente con branding y menú de 6 secciones.
- Área principal a la derecha con:
	- Topbar fija o sticky.
	- Contenido dinámico de la sección activa.

### 4.2 Sidebar

- Debe permanecer visible en desktop.
- En mobile puede colapsarse en drawer, pero debe seguir siendo persistente en comportamiento (accesible en toda sección).
- Ítems de navegación:
	- Dashboard
	- Gestión de usuarios
	- Gestión de agentes
	- Skills
	- Contrataciones de agentes
	- Log de errores
- El ítem activo debe tener estilo destacado (fondo, borde o acento de color).

### 4.3 Topbar

- Título de sección activa.
- Toggle de tema claro/oscuro (switch o botón con estado).
- Al cambiar tema, toda la interfaz debe actualizarse visualmente (fondos, texto, bordes, badges, modales).

## 5) Guía visual y sistema de diseño

### 5.1 Estilo general

- Apariencia profesional tipo SaaS B2B.
- Jerarquía tipográfica clara para títulos, subtítulos, labels de tabla y datos.
- Espaciado consistente en múltiplos de 4 (Tailwind spacing scale).
- Superficies en tarjetas con bordes suaves y sombra ligera.

### 5.2 Color y estados

- Definir paleta utilizable en claro y oscuro.
- Estados mínimos:
	- Éxito (activo / resuelto).
	- Advertencia (inactivo / atención).
	- Error (fallando / crítico).
	- Neutro (informativo).
- Badges de severidad en log de errores deben ser distinguibles por color y contraste.

### 5.3 Responsive

- Desktop: layout con sidebar + contenido.
- Tablet/mobile: tablas con scroll horizontal o compactación; mantener legibilidad.
- Modales adaptables a viewport reducido (max-height con scroll interno si hace falta).

## 6) Modelo de navegación e interacción

### 6.1 Cambio de sección

- Navegación por clic en sidebar.
- Solo una sección visible a la vez en el área principal.
- Se puede implementar con:
	- Render condicional por JS, o
	- Secciones en el DOM con hidden/block.

### 6.2 Dropdowns de acciones

- Cada fila/tarjeta que lo requiera tendrá botón de acciones (icono tipo "⋮").
- El menú debe abrir/cerrar por clic.
- Debe cerrarse al hacer clic fuera.
- Solo un dropdown abierto al mismo tiempo (regla recomendada para evitar ruido visual).

### 6.3 Modales

- Tipos de modal requeridos:
	- Detalle de usuario.
	- Configuración de agente (prompt de sistema).
	- Detalle de skill.
	- Detalle de contratación.
	- Detalle de error (stack trace).
- Todos los modales deben:
	- Usar overlay/backdrop.
	- Cerrar con botón explícito.
	- Cerrar al clic en backdrop.
	- Bloquear interacción del fondo mientras están abiertos.

### 6.4 Expand/collapse de skills de agente

- Skills ocultas por defecto.
- Control expandible por cada agente.
- Animación/transición suave al abrir/cerrar.

## 7) Requisitos por sección

### 7.1 Dashboard

Componentes obligatorios:

- Cuatro tarjetas de métricas visibles:
	- Ingresos totales generados (mes actual).
	- Pérdida total por descuentos y cupones.
	- Número de agentes activos.
	- Número de agentes fallando.
- Área de marcador de posición para gráfico de actividad semanal debajo de las tarjetas.

Contenido de demo sugerido:

- Mostrar valores numéricos claros, formato de moneda y variación opcional (ej. +12%).
- Placeholder de gráfico con etiqueta "Actividad semanal" y zona visual delimitada.

### 7.2 Gestión de usuarios

Componentes obligatorios:

- Tabla con columnas:
	- Nombre
	- Email
	- Plan
	- Estado
	- Acciones
- Dropdown por fila con opciones:
	- Ver detalle
	- Eliminar
- Modal "Ver detalle" con registro completo del usuario.
- Cierre de modal por botón y por clic en backdrop.

Datos mínimos hardcodeados:

- Al menos 6 usuarios con combinación de planes y estados variados.

### 7.3 Gestión de agentes

Componentes obligatorios:

- Listado de agentes con:
	- Nombre del agente
	- Propietario
	- Estado (activo/inactivo/fallando)
	- Skills colapsadas por defecto
	- Acciones
- Control expandible para revelar skills con transición suave.
- Dropdown por agente con opciones:
	- Configurar
	- Eliminar
- Modal "Configurar" que muestra el prompt de sistema del agente.

Datos mínimos hardcodeados:

- Al menos 6 agentes con estados mixtos y 2-5 skills por agente.

### 7.4 Skills

Componentes obligatorios:

- Bloque descriptivo dentro de la sección explicando qué es una "skill" en AgentHub.
- Catálogo/listado de skills con:
	- Nombre
	- Descripción breve
	- Indicador de cuántos agentes la usan
	- Acciones
- Dropdown por skill con opciones:
	- Ver detalle
	- Eliminar

Datos mínimos hardcodeados:

- Al menos 8 skills diferentes con uso heterogéneo.

### 7.5 Contrataciones de agentes

Componentes obligatorios:

- Tabla con columnas:
	- Cliente
	- Agente alquilado
	- Skills contratadas
	- Fechas del contrato
	- Importe total pagado
	- Acciones
- Dropdown por fila con "Ver detalle" (y opcionalmente otras acciones).
- Modal de detalle con:
	- Resumen del contrato
	- Lista desglosada de skills contratadas
	- Precio individual por skill
	- Total final

Datos mínimos hardcodeados:

- Al menos 6 contratos (mezcla de activos y finalizados).

### 7.6 Log de errores

Componentes obligatorios:

- Registro de errores con columnas/campos:
	- Timestamp
	- Nombre del agente
	- Tipo de error
	- Descripción breve
	- Severidad visual (badge)
	- Acciones
- Dropdown por entrada con opciones:
	- Ver detalle
	- Marcar como resuelto
- Modal "Ver detalle" mostrando traza completa del error.

Reglas de visualización:

- Badges de severidad por color (ej. crítico=rojo, warning=ámbar, info=azul).
- Debe percibirse claramente la diferencia entre tipos de error.

Datos mínimos hardcodeados:

- Al menos 10 registros con tipos y severidades variadas.

## 8) Datos hardcodeados - especificación mínima

Definir estructuras JavaScript locales (arrays de objetos) para:

- metrics
- users
- agents
- skillsCatalog
- contracts
- errorLogs

Cada objeto debe incluir los campos necesarios para renderizar vistas, badges, dropdowns y modales sin dependencia externa.

## 9) Requisitos funcionales transversales

- Todas las acciones visuales deben ser clicables y demostrar comportamiento esperado (aunque no persistan cambios reales).
- Botones "Eliminar" y "Marcar como resuelto" pueden ejecutar acciones de demo (ej. alert o actualización en memoria local de sesión), pero deben tener respuesta visible.
- Cualquier modal debe poblarse con datos de la fila/tarjeta seleccionada.
- Debe evitarse solapamiento defectuoso de dropdowns y modales (gestión de z-index coherente).

## 10) Accesibilidad básica

- Contraste suficiente de texto/fondo en ambos temas.
- Elementos interactivos con estado focus visible.
- Botones y controles con labels comprensibles.
- Escape puede implementarse opcionalmente para cerrar modales, recomendado.

## 11) Criterios de aceptación (Definition of Done)

Se considera completado cuando:

- Existen las 6 secciones accesibles desde sidebar persistente.
- El toggle claro/oscuro impacta toda la UI usando dark:.
- Dashboard muestra las 4 métricas y placeholder de gráfico semanal.
- Gestión de usuarios tiene tabla, dropdown por fila y modal de detalle con cierre por botón y backdrop.
- Gestión de agentes muestra skills colapsadas por defecto, expansión con transición y modal de configuración.
- Skills incluye explicación contextual, listado con indicador de uso y dropdown con acciones.
- Contrataciones muestra tabla completa y modal con desglose de skills y precios individuales.
- Log de errores muestra badges por severidad, dropdown de acciones y modal con traza completa.
- Todos los datos son hardcodeados y el prototipo funciona sin backend.
- Interfaz usable en desktop y mobile.

## 12) Entregables esperados para la siguiente fase (implementación)

- index.html con layout y secciones.
- styles opcionales (si se añade archivo CSS complementario).
- script.js opcional para lógica interactiva (o script embebido en HTML).

Nota: esta fase actual solo define la especificación. La implementación HTML/CSS/JS será el siguiente paso.

