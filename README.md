# Trailhead Admin Beginner — Resumen de estudio 📚

Resumen práctico para repasar y afianzar conceptos clave de administración en Salesforce. Tiempo estimado del trail: ⏱️ ~8 h.


## Salesforce Platform Basics 🧩
- Arquitectura y ecosistema: org multi‑tenant, metadatos como base. Primero declarativo, código cuando sea necesario.
- Vocabulario: objetos, registros, campos; permisos y seguridad a varios niveles.
- Setup (Configuración): busca opciones con Búsqueda rápida; crea objetos/campos en Gestor de objetos.
- AppExchange: instala apps/componentes verificados para ampliar sin programar (revisa permisos post‑instalación).
- Trailhead Playground: entorno seguro para retos; usa “Launch” y restablece si fuera necesario.
- Enfoque por casos: modela procesos (ventas, servicio, marketing) con objetos, automatización y seguridad.


## Data Modeling 🏗️
- Objetos estándar vs personalizados: estándar (Cuenta, Contacto, Oportunidad); personalizados para necesidades propias.
- Campos: tipos adecuados (picklist, fórmula, lookup, checkbox, etc.). Documenta con descripciones.
- Relaciones:
  - Lookup: flexible; sin herencia de propiedad/seguridad; el hijo puede existir sin padre.
  - Master‑Detail: hereda propiedad y seguridad; borrado en cascada; permite roll‑up summary en el master.
  - Junction object: dos master‑detail para muchos‑a‑muchos.
- Tipos de registro y diseños de página: segmentan experiencia por procesos/perfiles.
- Schema Builder: vista visual para crear/entender el modelo; usa Auto‑Layout para ordenar.

💡 Ejemplo (Relaciones y roll‑up) 
- Necesidad: contar inscripciones por curso y ocultar inscripciones si el usuario no ve el curso.
- Modelo: `Curso__c` (Master) — `Inscripcion__c` (Detail).
- Ventaja: en `Curso__c` crea un campo Roll‑Up Summary (COUNT) de `Inscripcion__c`. Seguridad y borrado en cascada se heredan. ✅


## Data Management 🧮
- Importar datos:
  - Asistente de importación: UI en Configuración; ideal hasta ~50k; objetos comunes.
  - Data Loader: cargas masivas (>50k), update/upsert, External IDs, y objetos no soportados por el asistente.
- Orden típico de carga: Usuarios → Cuentas → Contactos → Oportunidades → Hijos dependientes.
- Consejos: CSV en UTF‑8, limpia espacios y formatos; prueba con lote pequeño primero.
- Exportar/backup: Exportación de datos (semanal/mensual) o Data Loader para análisis/copias.

💡 Ejemplo (Upsert con External ID en Data Loader)
- Objetivo: crear/actualizar cuentas sin depender del Salesforce Id.
- Pasos: añade `ExternalId__c` en `Account`; prepara CSV con ese identificador; usa Upsert mapeando `ExternalId__c`.
- CSV mínimo:
```
ExternalId__c,Name,Phone
C-0001,Acme Corp,+34 900 000 001
C-0002,Globex,+34 900 000 002
```
- Resultado: si `ExternalId__c` existe → update; si no → insert. 🔄


## Lightning Experience Customization 🛠️
- Apps Lightning: pestañas, branding y navegación; decide qué ve cada perfil.
- List Views: filtros AND/OR, gráficos rápidos, edición en línea, vista Kanban para pipelines.
- Compact Layouts: define campos destacados del encabezado de registros.
- Record Pages:
  - Lightning App Builder: estructura y componentes por app/perfil/tipo de registro.
  - Page Layouts: campos, secciones, listas relacionadas, acciones y botones.
- Acceso rápido: icono de engranaje → “Editar página” (App Builder); diseños en Gestor de objetos.
- Botones, enlaces y acciones:
  - List button, Detail page link, Detail page button.
  - Acciones rápidas: globales vs de objeto; crear/actualizar registros o lanzar flujos.


## User Engagement (In‑App Guidance) 💡
- Prompts: ayudas contextuales (Floating, Targeted, Docked) para descubrir funciones.
- Walkthroughs: serie de prompts que guían procesos clave paso a paso.
- Targeting y control: segmenta por app, perfil, página y frecuencia; programa vigencia; analiza vistas/clicks para iterar.


## Reports & Dashboards 📊
- Reportes:
  - Tipos: Tabular, Summary, Matrix, Joined.
  - Filtros: estándar, relativos (hoy/este mes), lógica AND/OR y Cross Filters (incluir/excluir hijos).
  - Agrupaciones y cálculos: totales, subtotales, row‑level formulas y buckets.
- Dashboards:
  - Componentes: gráficos, tablas, medidores; cada uno con un reporte origen.
  - Dinámicos: ejecutan “como el usuario actual” respetando visibilidad; controla acceso con carpetas.
- Buenas prácticas: nombres claros, filtros de dashboard y pocos KPIs accionables.

💡 Ejemplo (Análisis de pipeline)
- Row‑level formula: `Weighted_Amount__c = Amount * Probability / 100` para ver pipeline ponderado.
- Cross Filter: Cuentas WITHOUT Oportunidades para detectar cuentas sin actividad comercial. 🔍


## Decisiones rápidas 🧭
- Lookup vs Master‑Detail: ¿necesitas roll‑ups, herencia de seguridad o borrado en cascada? → Master‑Detail. ¿Independencia? → Lookup.
- Asistente vs Data Loader: bajo volumen/objetos soportados → Asistente; alto volumen, upsert, programable → Data Loader.
- App Builder vs Page Layout: estructura/visibilidad de componentes → App Builder; campos/listas relacionadas/acciones → Page Layout.
- Reporte vs Dashboard: análisis detallado/ad hoc → Reporte; visión ejecutiva en una pantalla → Dashboard.


## Consejos y buenas prácticas ✅
- Nombra y describe campos/objetos; ayuda a admins futuros y a reportes.
- Usa validaciones para calidad de datos; picklists y reglas de negocio claras.
- Prueba en un Playground/Sandbox y en lotes pequeños antes de cargas masivas.
- Documenta decisiones (por qué Lookup vs Master‑Detail, convenciones de External IDs, etc.).


## Recursos oficiales 🔗
- Trailhead: Admin Beginner → https://trailhead.salesforce.com/users/strailhead/trailmixes/admin-beginner

—
Pequeños ejemplos y emojis añadidos para facilitar el repaso. 📝