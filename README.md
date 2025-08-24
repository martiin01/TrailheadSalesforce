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


# Developer Beginner

## Fórmulas

Resumen: Fórmulas
Los campos de fórmula son una herramienta en Salesforce que te permite calcular y mostrar datos en un registro sin necesidad de almacenarlos. Son útiles para:

Calcular valores: Dividir campos, restar fechas, etc.

Mostrar datos de otros registros: Obtener el número de cuenta de un contacto.

Crear enlaces clicables: Convertir un campo en un enlace.

Cómo crearlos
Para crear un campo de fórmula, ve al Gestor de objetos, selecciona el objeto, haz clic en Campos y relaciones y elige Fórmula. El editor de fórmulas te permite usar campos, operadores y funciones.

Puntos clave
Usa el editor avanzado.

El botón Verificar sintaxis es crucial para detectar errores.

Los errores comunes incluyen paréntesis faltantes, tipos de datos incorrectos y nombres de campos mal escritos.

Los campos de fórmula son muy versátiles y se pueden usar en informes y vistas de lista.

Resumen: Campos de resumen acumulado (Roll-up Summary)
Un campo de resumen acumulado es una herramienta de Salesforce que calcula valores de un grupo de registros relacionados (detail) y muestra el resultado en un registro principal (master). Su principal diferencia con un campo de fórmula es que opera sobre múltiples registros en lugar de uno solo.

Cómo crearlo
Para implementar este campo, el objeto principal y el secundario deben estar unidos por una relación master-detail.

Navega al objeto principal: Ve a Setup > Gestor de objetos y selecciona el objeto que está en el lado "maestro".

Crea el campo: En Campos y relaciones, haz clic en Nuevo y elige Roll-up Summary.

Configura el resumen:

Objeto a resumir: Elige el objeto secundario (ej. Oportunidades).

Tipo de resumen: Selecciona el cálculo deseado:

COUNT: Cuenta registros.

SUM: Suma los valores de un campo.

MIN: Muestra el valor más bajo.

MAX: Muestra el valor más alto.

Campo a agregar: Elige el campo del objeto secundario que se usará en el cálculo (ej. el Monto de las oportunidades).

Guarda: Completa el proceso y el campo se creará automáticamente en el registro principal.




# SECURE YOUR CRM 
## 👥 Gestión de Usuarios en Salesforce

## 🎯 Objetivos de Aprendizaje
- Comprender qué es una cuenta de usuario y qué información contiene.  
- Añadir uno o varios usuarios.  
- Congelar (**Freeze**) o desactivar (**Deactivate**) usuarios.  

---

## 🔑 ¿Qué es un Usuario?
- Persona que inicia sesión en Salesforce.  
- Tipos de usuarios:  
  - Internos: empleados (comerciales, managers, IT...).  
  - Externos: clientes, prospectos y partners (Experience Cloud).  
- Cada usuario necesita una **cuenta de usuario**, que define acceso a funciones y registros.  

### Información básica de una cuenta:
- Username (único, formato email).  
- Email.  
- Nombre y Apellido.  
- Alias y Nickname.  
- Licencia.  
- Perfil.  
- Rol (opcional).  

👉 Se gestionan en: **Setup → Quick Find → Users → Users**.  

---

## 📌 Conceptos Clave
- **Username**: formato email único (no tiene que ser un email real).  
- **Email**: puede repetirse en diferentes organizaciones.  
- **Licencia de Usuario**: determina acceso a funcionalidades. Ejemplo:  
  - *Salesforce License*: acceso completo.  
  - *Chatter Free*: solo Chatter, sin datos.  
- **Perfiles**: definen configuración base (apps, pestañas, login hours, IPs).  
  - Recomendado: usar *Minimum Access – Salesforce* + **Permission Sets**.  
- **Permission Sets / Groups**: añaden permisos extra a usuarios.  

| Configuración / Permisos         | Perfil | Permission Set |
|----------------------------------|--------|----------------|
| Apps, pestañas, layouts por defecto | ✔️     | ❌ |
| Login hours / IP ranges          | ✔️     | ❌ |
| Permisos de objetos y campos     | ❌     | ✔️ |
| Permisos personalizados          | ❌     | ✔️ |
| Acceso a Apex / Visualforce      | ❌     | ✔️ |

- **Roles**: controlan visibilidad de datos en la jerarquía. (Opcional).  
- **Alias**: abreviación del nombre del usuario (ej: jdoe).  

---

## 🛠️ Añadir Usuarios
1. Ir a **Setup → Quick Find → Users → Users**.  
2. Clic en **New User** (1 usuario) o **Add Multiple Users** (hasta 10).  
3. Completar datos: nombre, email, username (único, formato email).  
4. Seleccionar:  
   - **User License**.  
   - **Profile**.  
   - (Opcional) Rol.  
5. Marcar **Generate password and notify user immediately**.  
6. Guardar con **Save**.  

⚠️ Los usuarios deben cambiar su contraseña en el primer login.  

---

## ❄️ Congelar un Usuario (Freeze)
- Bloquea acceso temporal.  
- **No libera la licencia**.  

**Ruta:**  
`Setup → Users → Seleccionar Usuario → Freeze`  

---

## 🔒 Desactivar un Usuario
- Bloquea acceso y **libera la licencia**.  
- No se pueden borrar usuarios (para no perder registros).  

**Ruta:**  
`Setup → Users → Edit → desmarcar "Active" → Save`  

---

## 👀 Ver Acceso de un Usuario
Con **User Access Summary** puedes revisar permisos:  
1. `Setup → Users → Seleccionar Usuario → View Summary`  
2. Revisar pestañas: permisos, grupos, colas.  
3. Clic en **Access Granted By** para ver qué asignación da ese permiso.  

---

## 📌 Diferencia Freeze vs Deactivate
- **Freeze** → usuario bloqueado temporalmente, licencia sigue ocupada.  
- **Deactivate** → usuario bloqueado y licencia liberada.  

## 🔐 Control de Acceso de Usuarios en Salesforce

## 🎯 Objetivos de Aprendizaje
- Describir los diferentes niveles de control de acceso a los datos en Salesforce.  
- Crear **Permission Sets** y **Permission Set Groups**.  
- Configurar los **Organization-Wide Defaults (OWD)** para compartir registros.  

---

## 🛡️ Introducción a la Seguridad de Datos
Salesforce permite controlar lo que los usuarios pueden **ver, crear, editar o eliminar** mediante configuraciones a distintos niveles:  
- Organización.  
- Objetos.  
- Campos.  
- Registros.  

Combinando estos niveles se otorga el acceso justo a cada usuario, sin necesidad de asignar permisos uno por uno.  

---

## 📊 Niveles de Acceso a Datos

1. **Organización**
   - Lista de usuarios autorizados.  
   - Políticas de contraseñas.  
   - Restricción por horarios o ubicaciones de login.  

2. **Objetos**
   - Determina si los usuarios pueden ver, crear, editar o eliminar registros de un objeto.  
   - Se recomienda configurarlo con **Permission Sets** o **Permission Set Groups**.  

3. **Campos**
   - Control de visibilidad/edición de campos dentro de un objeto.  
   - Ejemplo: campo *salario* visible solo para managers.  
   - Configurable en **Permission Sets**.  

4. **Registros**
   - Control de acceso a nivel de registros individuales.  
   - Basado en:  
     - **OWD (Organization-Wide Defaults)**.  
     - Jerarquía de roles.  
     - Sharing rules.  
     - Manual sharing.  

---

## 🧩 Permission Sets
- Colecciones de permisos para ampliar acceso **sin modificar perfiles**.  
- Permiten acceso a objetos, campos, pestañas y funciones.  
- Reutilizables: evitan crear decenas de perfiles distintos.  
- Recomendación: usar **Minimum Access – Salesforce** + asignar **Permission Sets** según necesidad.  

### 🚀 Crear un Permission Set
1. `Setup → Quick Find → Permission Sets → New`.  
2. Ingresar *Label* y *Descripción*.  
3. (Opcional) Seleccionar licencias a las que aplica.  
4. Guardar con **Save**.  
5. Configurar permisos:  
   - **Object Settings → [Objeto] → Edit** → asignar permisos de objeto y campos.  
   - **App Permissions / System Permissions → Edit** → asignar permisos de usuario.  
6. Guardar y asignar a usuarios.  

---

## 📦 Permission Set Groups
- Agrupan varios **Permission Sets**.  
- Se asignan a usuarios en bloque → permisos combinados.  
- Permiten **mutear permisos** dentro del grupo.  
- Un mismo Permission Set puede estar en varios grupos.  

### 🚀 Crear un Permission Set Group
1. `Setup → Quick Find → Permission Set Groups → New Permission Set Group`.  
2. Ingresar *Label* y *Descripción*. Guardar.  
3. En **Permission Sets in Group → Add Permission Set** → seleccionar los que correspondan.  
4. (Opcional) Mutear permisos:  
   - **Muting Permission Set in Group → New → Save**.  
   - Editar y marcar en columna *Muted* los permisos a bloquear.  
5. Asignar a usuarios:  
   - **Manage Assignments → Add Assignments** → seleccionar usuarios.  
   - (Opcional) Definir fecha de expiración.  

---

## 🌍 Organization-Wide Defaults (OWD)
Definen el **nivel base de acceso a registros** que no son propios.  

### Opciones de Acceso:
| Modelo                  | Descripción |
|--------------------------|-------------|
| **Private**             | Solo el propietario y roles superiores pueden ver/editar. |
| **Public Read Only**    | Todos pueden ver y reportar, pero solo propietario/roles superiores editan. |
| **Public Read/Write**   | Todos pueden ver, editar y reportar. |
| **Controlled by Parent**| El acceso depende del registro padre. |

👉 Si el OWD es **Private** o **Public Read Only**, se puede **ampliar acceso** con jerarquías, reglas de compartición o sharing manual.  
⚠️ Nunca se puede **restringir más** de lo que define el OWD.  

### 🚀 Configurar OWD
1. `Setup → Quick Find → Sharing Settings`.  
2. En **Organization-Wide Defaults → Edit**.  
3. Para cada objeto, seleccionar nivel de acceso en **Default Internal Access**.  
4. Activar **Grant Access Using Hierarchies** para dar acceso automático a roles superiores (en objetos custom, si no es Controlled by Parent).  
5. Guardar.  

---

## 📌 Resumen Rápido
- **Niveles de seguridad:** Organización → Objetos → Campos → Registros.  
- **Permission Sets:** amplían permisos a usuarios sin tocar perfiles.  
- **Permission Set Groups:** agrupan varios Permission Sets (con opción de mutear permisos).  
- **OWD:** establecen acceso base a registros (Private, Public Read Only, Public Read/Write, Controlled by Parent).  

---
