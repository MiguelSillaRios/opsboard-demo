# OpsBoard — Demo de gestión de tareas operativas

Prototipo funcional de una aplicación para gestión de tareas en equipos operativos (logística, transporte, almacén). Diseñado como alternativa moderna a las hojas de Excel compartidas que muchos equipos siguen usando para coordinar el día a día.

**[→ Probar la demo en vivo](https://opsboard-demo.netlify.app/)** **

---

## El problema

Muchos equipos operativos siguen gestionando sus tareas diarias en Excel:

- Asignaciones rígidas (el famoso "binomio fijo": Persona A o Persona B, no hay otra opción)
- Sin trazabilidad real de quién ha hecho qué y cuándo
- Sin KPIs que permitan al manager identificar cuellos de botella o cargas desiguales
- Sin gestión de ausencias (vacaciones, bajas) más allá de "cambiarlo a mano"
- Sin visibilidad para el equipo: cada operario ve solo "su" Excel

OpsBoard es una propuesta de cómo se ve esto cuando lo construyes pensando en las personas que lo van a usar.

## Funcionalidades

### Para el manager
- **Planificador horario** con asignación libre por drag & drop (sin binomios fijos)
- **Gestión de ausencias por rangos** (vacaciones, bajas, permisos)
- **Reasignaciones masivas**: mueve todas las tareas de una persona a otra (o varias) durante un rango de fechas, con filtros por días de la semana
- **Creación de tareas puntuales** en caliente
- **KPIs**: % OK, % KO, % cierres sospechosos (<2 min), duración media, evolución mensual, ranking por operativo, ranking por tarea (minutos por tarea)
- **Vista TV** para proyectar en pantalla de oficina

### Para el operativo
- **Mis tareas del día** con botones grandes Iniciar / Finalizar y cuenta atrás hasta hora límite
- **Vista general (TV)** del estado de todo el equipo

### Reglas de cómputo
- **OK**: tarea iniciada y finalizada antes de la hora teórica
- **KO**: finalizada fuera de plazo o no iniciada al cierre del día
- **Sospechosa**: cerrada en menos de 2 minutos desde el inicio (posible cierre exprés sin trabajo real)
- Tareas asignadas a binomios computan en KPIs para todos los integrantes

## Stack técnico

Demo construida intencionadamente como **un único `index.html`** sin dependencias de servidor:

- HTML + CSS + JavaScript vanilla
- [Chart.js](https://www.chartjs.org/) para gráficos
- localStorage del navegador para persistencia local de las acciones del usuario
- JSON embebido con histórico simulado de 6 meses (~3.500 ejecuciones)

Esto permite que la demo funcione abriendo un único archivo, sin instalación, sin backend y sin base de datos. Ideal para validar la idea antes de pasar a producción.

## Cómo se escalaría a producción

| Capa | Demo actual | Versión productiva |
|---|---|---|
| Frontend | HTML + JS vanilla | Mismo, o React/Vue si se prefiere |
| Backend | Sin backend | Python (FastAPI / Flask) con API REST |
| Persistencia | localStorage + JSON | SQL / SharePoint Lists / Dataverse |
| Autenticación | Selector simulado | Microsoft Entra ID / OAuth |
| Tiempo real | No | WebSockets / polling |
| Despliegue | Netlify (estático) | Azure App Service / on-premise |

La lógica de negocio del prototipo (cálculo de estados, reasignaciones, descomposición de binomios para KPIs, gestión de ausencias por rangos) está aislada en JavaScript y es directamente trasladable a cualquier backend.

## Datos

El histórico que ves al abrir la app es **completamente simulado**:

- 6 meses de datos sintéticos
- 8 operativos ficticios (Carlos, Ana, David, Laura, Miguel, Elena, Pablo, Marta)
- Cada operativo tiene un perfil de rendimiento distinto, así los rankings tienen variabilidad realista
- ~80% OK, ~15% KO, ~5% sospechosas — distribución típica de un equipo real funcionando bien

## Cómo probar

1. Abre la demo
2. Arriba a la derecha hay un selector de usuario. Por defecto eres "Manager" (ves todo).
3. Cambia a Carlos, Ana, David... para ver la **vista de operativo** (solo "Mis tareas" y "Vista general")
4. Como manager, prueba a:
   - Cambiar de día con los botones ◀/▶ del planificador
   - Crear una tarea puntual con "+ Nueva tarea"
   - Marcar a alguien de vacaciones desde el botón "Ausencias"
   - Crear una regla de reasignación masiva desde "Reasignaciones"
   - Revisar los KPIs y la vista TV

## Contexto

Construido como demostración pública. El diseño se inspira en patrones reales de equipos de logística pero los datos, nombres y tareas son ficticios.

## Autor

Miguel Silla Ríos · [LinkedIn](https://www.linkedin.com/in/miguelsillarios/) · [GitHub](https://github.com/MiguelSillaRios)

Data Scientist en logística. Interesado en construir herramientas que reemplacen los Excel compartidos por interfaces que las personas realmente usen.

## Licencia

MIT
