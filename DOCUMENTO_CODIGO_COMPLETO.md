# DOCUMENTO CON TODO EL CODIGO - Webapp Automechanika Shanghai 2025
Proyecto: Seguimiento Lizarte | Version V12
Generado: 2026-02-06 12:17
Total: index.html (~5775) + datos.json (~1505) + GUIA (~401) + deploy.yml (~57) = mas de 7700 lineas

---

## 1. .github/workflows/deploy.yml

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write  # ⚠️ ESTE ES EL PERMISO QUE FALTABA

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup Node.js (si es necesario)
        uses: actions/setup-node@v4
        with:
          node-version: '20'
      
      # Aquí irían tus pasos de build si los tienes
      - name: Build
        run: echo "Build completado"
        # Ejemplo: npm install && npm run build

  report-build-status:
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Report build status
        run: echo "Build status reportado"

  deploy:
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup Pages
        uses: actions/configure-pages@v4
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'  # Ajusta esto según tu estructura (ej: './dist' si tienes build)
      
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

## 2. GUIA_USO_APLICACION.md

```markdown
# Guia de Uso - Sistema de Seguimiento Automechanika Shanghai 2025

## 🎯 Introducción

Esta aplicación web ha sido diseñada para gestionar y hacer seguimiento de todos los contactos y reuniones realizadas durante la feria **Automechanika Shanghai 2025** (19 Nov - 6 Dic). Permite organizar la información de empresas, reuniones programadas, oportunidades de negocio y mantener un control completo del estado de seguimiento de cada contacto.

---

## 🚀 Pantalla Inicial (Splash Screen)

Al abrir la aplicación, verás una pantalla de bienvenida que muestra:

- **🏢 Empresas Priorizadas Contactadas**: Total de empresas registradas en el sistema
- **🤝 Reuniones Estratégicas**: Número de reuniones programadas
- **📷 Registros Visuales**: Total de fotos subidas
- **⭐ Oportunidades Innovación**: Empresas asignadas al departamento de Innovación

**Nota**: Esta pantalla se muestra automáticamente al cargar la aplicación. Haz clic en "🚀 ACCEDER AL SISTEMA" para continuar.

---

## 📊 Dashboard Principal

### Tarjetas de Estadísticas

En la parte superior de la pantalla principal encontrarás 5 tarjetas con estadísticas en tiempo real:

1. **Total**: Número total de empresas (reuniones + información adicional)
2. **Pendientes**: Empresas que aún no han sido contactadas
3. **Contactados**: Empresas con las que ya se ha establecido contacto
4. **En Proceso**: Empresas con negociaciones o seguimiento activo
5. **Finalizados**: Empresas con seguimiento completado

**💡 Importante**: Estos números se actualizan automáticamente cuando añades, modificas o cambias el estado de las empresas.

---

## 📑 Pestañas Principales

La aplicación está organizada en tres pestañas:

### 🤝 Reuniones
Contiene todas las **reuniones programadas** durante la feria. Cada reunión incluye:
- Nombre de la empresa
- Persona de contacto
- Producto/servicio de interés
- Hora y stand de la reunión
- Comentarios y notas
- Fotos de la reunión
- Sistema de seguimiento completo

**Contador**: El número entre paréntesis `(X)` muestra cuántas reuniones hay registradas.

### 📋 Info Adicional
Contiene **empresas de interés** que no tienen reunión programada pero son relevantes para el seguimiento. Incluye:
- Nombre de la empresa
- Producto/servicio
- Notas generales
- Oportunidad de negocio (descripción detallada)
- Fotos
- Sistema de seguimiento completo

**Contador**: El número entre paréntesis `(X)` muestra cuántas empresas adicionales hay registradas.

### ⚙️ Configuración
Permite personalizar:
- Título de la aplicación
- Subtítulo
- Notas generales sobre la feria

---

## 🏷️ Sistema de Clasificación

### Departamentos

Cada empresa puede estar asignada a uno de dos departamentos:

- **🔵 Lizarte**: Empresas relacionadas con el negocio principal de Lizarte
- **⭐ Innovación**: Empresas relacionadas con proyectos de innovación y nuevas oportunidades

El departamento se muestra como una **etiqueta (badge)** junto al nombre de la empresa.

### Prioridades

Cada empresa tiene un nivel de prioridad que puedes ajustar haciendo clic en los botones numéricos:

- **🔴 0 - Muy Importante**: Máxima prioridad, requiere atención inmediata
- **🟢 1 - Alta**: Alta prioridad, seguimiento prioritario
- **🟡 2 - Media**: Prioridad media, seguimiento normal
- **🟠 3 - Baja**: Baja prioridad, seguimiento ocasional

**Visualización**: El botón correspondiente a la prioridad actual se muestra resaltado con color.

---

## 📋 Sistema de Seguimiento

Cada empresa (tanto en Reuniones como en Info Adicional) tiene una sección de **Seguimiento** que permite gestionar el estado del contacto:

### Estados

Puedes marcar cada empresa con uno de estos estados:

- **⚪ Pendiente**: Aún no se ha contactado con la empresa
- **🟡 Contactado**: Ya se ha establecido contacto inicial
- **🔵 En Proceso**: Hay negociaciones o seguimiento activo en curso
- **🟢 Finalizado**: El seguimiento de esta empresa está completado

**Importante**: El estado seleccionado se refleja automáticamente en las estadísticas del dashboard.

### Información de Seguimiento

Para cada empresa puedes registrar:

- **👤 Responsable**: Persona del equipo de Lizarte asignada al seguimiento
- **📧 Email**: Dirección de correo del responsable (para enviar recordatorios)
- **📅 Fecha de Seguimiento**: Próxima fecha programada para seguimiento
- **📝 Próxima Acción**: Descripción de la siguiente acción a realizar
- **✅ Acciones**: Lista de acciones pendientes o realizadas (puedes añadir múltiples)

**Funcionalidades**:
- **➕ Añadir Acción**: Añade una nueva acción a la lista
- **✏️ Editar**: Haz clic en cualquier acción para editarla
- **🗑️ Eliminar**: Elimina una acción de la lista
- **📧 Enviar Email**: Abre tu cliente de correo con un mensaje preconfigurado para el responsable

---

## 🔍 Filtros y Búsqueda

En la parte superior, justo debajo de las pestañas, encontrarás un panel de filtros:

### 🔍 Buscar
Escribe cualquier texto para buscar en:
- Nombre de empresa
- Producto/servicio

### 🏢 Departamento
Filtra por:
- Todos
- 🔵 Lizarte
- ⭐ Innovación

### 👤 Responsable
Filtra por la persona asignada al seguimiento. La lista se genera automáticamente con los responsables que ya están asignados.

### 📊 Estado
Filtra por el estado de seguimiento:
- Todos
- Pendiente
- Contactado
- En Proceso
- Finalizado

### ⭐ Prioridad
Filtra por nivel de prioridad:
- Todas
- 🔴 0 - Muy Importante
- 🟢 1 - Alta
- 🟡 2 - Media
- 🟠 3 - Baja

**💡 Tip**: Puedes combinar múltiples filtros para encontrar exactamente lo que buscas. Por ejemplo: "Empresas de Innovación, prioridad Alta, estado En Proceso".

---

## ➕ Añadir Nueva Empresa

Haz clic en el botón **"➕ Añadir Nueva Empresa"** (arriba a la derecha).

Se abrirá un menú donde puedes elegir:
- **🤝 Añadir Reunión**: Para empresas con reunión programada
- **📋 Añadir Info Adicional**: Para empresas de interés sin reunión programada

### Al añadir una Reunión, se te pedirá:
- Nombre de la empresa
- Persona de contacto
- Producto/servicio
- Hora de la reunión
- Stand (opcional)
- Departamento (Lizarte o Innovación)
- Prioridad (0-3)

### Al añadir Info Adicional, se te pedirá:
- Nombre de la empresa
- Producto/servicio
- Departamento (Lizarte o Innovación)
- Prioridad (0-3)

**Nota**: Todos los demás campos (notas, seguimiento, fotos, etc.) se pueden completar después de crear la empresa.

---

## ✏️ Editar Información

### Campos de Texto
- **Clic en cualquier campo** y escribe para modificar
- Los cambios se guardan automáticamente al salir del campo
- Los campos de texto largo (Comentarios, Notas, Oportunidad) se ajustan automáticamente a su contenido

### Campos Especiales

**Prioridad**: Haz clic en los botones numéricos (0, 1, 2, 3) en la esquina superior derecha de cada tarjeta de empresa.

**Departamento**: Selecciona en el menú desplegable dentro de la información básica.

**Estado de Seguimiento**: Selecciona el botón de radio correspondiente en la sección de Seguimiento.

---

## 📷 Gestión de Fotos

### Añadir Fotos
1. Haz clic en **"📷 Añadir Fotos"** en la sección de fotos de cada empresa
2. Selecciona una o varias imágenes desde tu dispositivo
3. Las fotos se mostrarán como miniaturas

### Ver Fotos
- Haz clic en cualquier miniatura para verla en tamaño completo
- Se abrirá un modal (ventana emergente) con la imagen ampliada
- Haz clic fuera del modal o en la X para cerrar

### Eliminar Fotos
- Haz clic en el botón **"×"** en la esquina superior derecha de cada miniatura
- Se pedirá confirmación antes de eliminar

---

## 📎 Gestión de Documentos

Cada empresa puede tener documentos asociados:

### Añadir Documento como Enlace
1. Haz clic en **"🔗 Añadir Enlace"**
2. Introduce la URL del documento
3. Asigna un nombre descriptivo

### Añadir Documento como Archivo
1. Haz clic en **"📄 Añadir Archivo"**
2. Selecciona un archivo desde tu dispositivo (PDF, Word, Excel)
3. El archivo se guardará en formato base64

### Ver/Eliminar Documentos
- Haz clic en el nombre del documento para abrirlo
- Haz clic en **"🗑️"** para eliminar un documento

---

## 🗑️ Eliminar Empresa

1. Haz clic en el botón **"🗑️"** en la esquina superior derecha de la tarjeta de la empresa
2. Confirma la eliminación
3. La empresa se eliminará de la vista

**⚠️ Importante**: 
- La eliminación es permanente en tu sesión actual
- Para que la eliminación sea definitiva, debes **exportar los datos** (ver sección Exportación)
- Las empresas eliminadas no aparecerán en el JSON exportado

---

## 📤 Exportar Datos

### ¿Cuándo exportar?
Exporta los datos cuando:
- Has añadido nuevas empresas
- Has modificado información importante
- Has eliminado empresas
- Quieres compartir los datos actualizados con el equipo

### Cómo exportar
1. Haz clic en el botón flotante **"📤 EXPORTAR"** (esquina inferior derecha)
2. El sistema generará un archivo `datos.json` con todos los datos actualizados
3. El archivo se descargará automáticamente

### ¿Qué incluye la exportación?
- Todas las empresas (reuniones + adicional)
- Todas las modificaciones realizadas
- Sistema de seguimiento completo
- Fotos (en formato base64)
- Documentos
- **NO incluye** empresas que hayas eliminado

### Después de exportar
1. Ve a GitHub (o tu repositorio)
2. Sube el archivo `datos.json` descargado
3. Reemplaza el archivo anterior
4. Haz commit con el mensaje: "Datos actualizados"
5. Comparte el enlace con tu equipo

**💡 Importante**: Solo cuando subas el archivo a GitHub, los cambios serán visibles para todos los miembros del equipo.

---

## 💾 Guardado Automático

La aplicación guarda automáticamente todos los cambios en el **almacenamiento local del navegador** (localStorage). Esto significa que:

- ✅ Tus cambios se guardan inmediatamente
- ✅ Si recargas la página, tus cambios siguen ahí
- ✅ No necesitas guardar manualmente (excepto para exportar)

**⚠️ Nota**: El almacenamiento local es específico de cada navegador y dispositivo. Si cambias de navegador o dispositivo, necesitarás exportar e importar los datos.

---

## 🎨 Características Visuales

### Campos de Texto Largo
Los campos de texto largo (Comentarios, Notas, Oportunidad) se ajustan automáticamente a su contenido. Esto significa que:
- No necesitas hacer scroll dentro del campo
- Todo el texto es visible sin necesidad de expandir manualmente
- El campo crece automáticamente mientras escribes

### Badges y Etiquetas
- **Badge de Departamento**: Aparece junto al nombre de la empresa (🔵 Lizarte o ⭐ Innovación)
- **Badge de Prioridad**: Se muestra en la sección de seguimiento de Info Adicional

### Colores y Estados
- Los colores de los botones de prioridad cambian según el nivel seleccionado
- Los estados de seguimiento tienen colores distintivos (blanco, amarillo, azul, verde)

---

## ❓ Preguntas Frecuentes

### ¿Puedo usar la aplicación sin conexión a internet?
Sí, la aplicación funciona completamente sin conexión. Solo necesitas internet para:
- Cargar la aplicación por primera vez
- Subir el archivo exportado a GitHub

### ¿Qué pasa si cierro el navegador?
Todos tus cambios están guardados en el almacenamiento local. Al volver a abrir la aplicación, verás todos tus datos.

### ¿Cómo comparto los datos con mi equipo?
1. Exporta los datos (botón 📤 EXPORTAR)
2. Sube el archivo `datos.json` a GitHub
3. Comparte el enlace de la aplicación con tu equipo
4. Todos verán los datos actualizados

### ¿Puedo recuperar una empresa eliminada?
Si acabas de eliminar una empresa y aún no has exportado, puedes:
1. No exportar los datos
2. Recargar la página (los datos se cargarán desde el JSON original)
3. La empresa volverá a aparecer

Si ya exportaste, la empresa estará eliminada permanentemente del JSON.

### ¿Cómo sé qué empresas he modificado?
Todas las empresas que veas en la aplicación reflejan el estado actual, incluyendo todas tus modificaciones. No hay una lista separada de "empresas modificadas".

### ¿Puedo añadir más de una foto?
Sí, puedes añadir múltiples fotos a cada empresa. Simplemente selecciona varias imágenes cuando uses "Añadir Fotos".

### ¿Los cambios se guardan automáticamente?
Sí, todos los cambios se guardan automáticamente en el almacenamiento local. Solo necesitas exportar cuando quieras compartir los datos con el equipo.

---

## 🆘 Solución de Problemas

### Los contadores no se actualizan
- Recarga la página (F5)
- Los contadores deberían actualizarse automáticamente

### No veo mis cambios después de recargar
- Verifica que estés usando el mismo navegador
- Los datos se guardan en el almacenamiento local del navegador específico

### El botón de exportar no funciona
- Verifica que tengas permisos para descargar archivos en tu navegador
- Intenta con otro navegador si el problema persiste

### Las fotos no se cargan
- Verifica que las fotos estén en un formato compatible (JPG, PNG)
- Asegúrate de que el tamaño del archivo no sea excesivamente grande

---

## 📞 Contacto y Soporte

Para dudas o problemas técnicos, contacta con:
**Krum Kovachev** - Desarrollador del sistema

**Versión**: V12 by Krum Kovachev

---

## 📝 Notas Finales

- Esta aplicación está diseñada específicamente para **Automechanika Shanghai 2025**
- Todos los datos son privados y se almacenan localmente
- Exporta regularmente para mantener una copia de seguridad
- Comparte los datos actualizados con el equipo mediante GitHub

---

**¡Gracias por usar el Sistema de Seguimiento Automechanika Shanghai 2025!** 🚀

```

## 3. datos.json

```json{
  "reuniones": [
    {
      "company": "ALTEZZA",
      "person": "Gustavo/Gloria",
      "product": "Grupo hidráulico, conectores DAES, Husillos DAES",
      "time": "14:45",
      "stand": "Hall 2.1 A71",
      "comments": "<b>Grupos hidráulicos</b> – Plan de validación\nLa próxima semana recibiremos cinco grupos hidráulicos para someterlos a pruebas de validación. Realizaremos dos tipos de test: ensayo de durabilidad de 1.500 horas en banco de verificación y prueba de resistencia de 3.000 km en vehículo real.\nEl plazo de aprobación es crítico: si damos el OK antes de Navidad, podrán enviarnos las unidades con rapidez. En caso contrario, el envío se retrasaría hasta después de Año Nuevo, con inicio de fabricación en marzo y un plazo de producción de aproximadamente un mes, más el tiempo de transporte marítimo.\n\nReunión con Gloria – <b>Cremalleras de husillo</b> para DAES y componentes(Conectores)\nHablé con Gloria sobre las cremalleras de husillo destinadas a sistemas de dirección asistida eléctrica (DAES). Le comenté que las últimas ofertas que hemos recibido rondan los 100 € por unidad, aunque en realidad algunas cotizaciones han sido superiores. Le trasladé que un precio objetivo interesante para nosotros sería de unos <b>50 € por unidad</b>. Su respuesta fue positiva:<b> no lo ve imposible de conseguir pero en un tiempo más largo.</b>\nNos recomienda que <b>Javier Baztán</b> y yo mantengamos una reunión con ella para solicitar varias referencias y obtener cotizaciones detalladas.\nAdemás, Gloria nos ofreció columnas EPS nuevas. Al preguntarle por las referencias disponibles, mencionó Honda CR-V, que de momento no resultan interesantes para nuestra línea de producto. También nos mostró documentación <b>sobre conectores y recambios</b> <b>compatibles </b>con sistemas DAES.",
      "id": 1763364468847,
      "fotos": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Homologar nuevos grupos hidráulicos",
          "Comprobar de nuevo si Honda CR-V sería interesante comprar DAES nuevas",
          "Pedir información de conectores y recambios para DAES "
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 1,
      "fotos_extra": [],
      "respuestas": [
        {
          "texto": "Se han montado 3 unidades, todas con un consumo elevado, aprox de 75A-80A vs 50A. \nSe va a montar una pieza en el banco de verificación \nSe va a montar una pieza en el vehículo para testear ",
          "formato": {
            "negrita": false,
            "lista": false
          }
        }
      ],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "CHABGHUI GROUP",
      "person": "Jason Bai",
      "product": "Varios",
      "time": "16:18",
      "stand": "Hall 6.1 F01",
      "comments": "También tienen DAE nueva para Ford F-150 pickup, una referencia que podría resultar interesante dado el volumen de este modelo en ciertos mercados.\nAdemás, disponen de distintos <b>componentes sueltos para sistemas de dirección</b>, como sensores de ángulo y clock springs (muelles de reloj o contactores rotatorios del airbag).\nPendiente revisar el email para consultar el catálogo completo y valorar qué referencias pueden encajar con nuestra línea de producto.",
      "id": 1763378341743,
      "fotos": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Posible proveedor de anillos de airbag"
        ],
        "estado": "pendiente",
        "email": "jbastan@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 3,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "LT Drive Shaft",
      "person": "Cactus",
      "product": "Drive Shaft",
      "time": "18:12",
      "stand": "Hall 1.1 C24",
      "comments": "Empresa con la que coincidimos en Paris, poco más que añadir. ",
      "id": 1763719943011,
      "fotos": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "finalizado"
      },
      "departamento": "Lizarte",
      "prioridad": 3,
      "fotos_extra": [],
      "respuestas": [
        {
          "texto": "",
          "formato": {
            "negrita": false,
            "lista": false
          }
        }
      ],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "Bomba Retrofitting",
      "person": "Vanessa Li; liwei@zjquanxing.com (Hablar con Leo y Kathy)",
      "product": "Bomba universal",
      "time": "08:12",
      "stand": "Hall1.1 A10",
      "comments": "He realizado una visita a la empresa que fabrica la <b>bomba universal para retrofitting</b>. Me han llevado directamente a las instalaciones de Quanxing, donde he podido ver el proceso productivo de primera mano. Durante el recorrido, Leo me ha revelado información muy relevante que cambia completamente nuestra estrategia de aprovisionamiento: la empresa Bourge, con quien habíamos estado en contacto hasta ahora, no es fabricante. Es simplemente una comercializadora que revende el producto de Quanxing. No han sido sinceros con nosotros al presentarse como algo que no son.\nEsta revelación es importante porque significa que hemos estado negociando con un intermediario que añade su margen sin aportar valor real.<b> El fabricante auténtico de la bomba es Quanxing,</b> y ahora tenemos contacto directo con ellos.\nDecisión tomada:\nA partir de ahora, vamos a tratar directamente con Kathy y Leo en Quanxing para desarrollar el proyecto, eliminando intermediarios. Esto nos permitirá:\n\nMejores precios al eliminar el margen del comercializador.\nComunicación directa con quien realmente fabrica el producto.\nMayor capacidad de personalización y desarrollo conjunto.\nResolución de problemas técnicos de forma más ágil.\n\nObjetivo del proyecto:\nEl proyecto con Quanxing tiene un enfoque muy específico que nos diferencia del mercado y aporta un valor estratégico enorme:\n\n<b>Recibir la bomba sin software precargado:</b> Queremos que la bomba llegue \"en blanco\" para que desde Lizarte podamos cargar nuestro propio software. Esto es clave porque nos permite adaptar la bomba a cualquier aplicación de forma flexible, sin depender del fabricante para cada configuración diferente. Nosotros controlamos el software, nosotros controlamos el producto final.\n<b>Diseño de soportes personalizados: </b>Además de la bomba, trabajaremos en el diseño de soportes adaptados para facilitar la instalación en distintos vehículos. Esto convierte el producto en una solución de retrofitting completa, no solo un componente suelto. El cliente recibe bomba + soporte + software configurado = instalación sencilla y rápida.\n\nOportunidad de negocio identificada:\nEsta es una de las visitas más estratégicas identificadas en la feria, con potencial de impacto a largo plazo:\n\nProducto propio diferenciado: Al cargar nuestro propio software y diseñar soportes personalizados, el producto final es 100% Lizarte. No es una bomba genérica que cualquier competidor puede comprar, es una solución desarrollada por nosotros que solo nosotros podemos ofrecer. Esto nos posiciona como especialistas, no como simples revendedores.\nFlexibilidad de aplicación: Una bomba universal que podemos adaptar vía software a múltiples vehículos reduce enormemente la necesidad de stock de referencias diferentes. Con un mismo hardware físico podemos cubrir muchas aplicaciones simplemente cambiando la configuración de software. Esto simplifica la logística y reduce el capital inmovilizado en stock.\nSolución de retrofitting completa: El mercado del retrofitting busca soluciones fáciles de instalar. Si ofrecemos bomba + soporte + software configurado, el taller solo tiene que montar y conectar. Esto es un argumento de venta potente frente a competidores que solo venden la bomba y dejan al taller resolver la instalación.\nMárgenes mejorados: Al eliminar a Bourge como intermediario y tratar directamente con el fabricante, nuestros márgenes mejoran automáticamente. Además, el valor añadido del software y los soportes personalizados justifica un precio de venta superior.\nControl del conocimiento: El software lo desarrollamos y cargamos nosotros. Esto significa que el conocimiento técnico queda en Lizarte, no en el proveedor. Es una barrera de entrada para competidores que quieran copiar nuestra solución.\nEscalabilidad: Una vez desarrollado el sistema (software + soportes para los vehículos más comunes), escalar a nuevas aplicaciones es relativamente sencillo. Cada nuevo soporte diseñado amplía nuestro catálogo sin necesidad de desarrollar un producto completamente nuevo.\n\nDatos del contacto:\n\nFabricante real: Quanxing\nContactos directos: Kathy y Leo\nIntermediario descartado: Bourge (comercializadora, no fabricante)",
      "id": 1763896381600,
      "fotos": [],
      "seguimiento": {
        "responsable": "Calidad",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Primera acción; la bomba pequeña puede funcionar con 12V",
          "Segunda acción; qué necesitan para mandarnos una bomba sin software para que nosotros carguemos el nuestro?",
          "Establecer comunicación formal con Kathy y Leo como nuestros interlocutores directos. Definir especificaciones técnicas para recibir la bomba sin software. Iniciar el desarrollo del software propio internamente. Comenzar el diseño de soportes para las aplicaciones más demandadas del mercado. Solicitar muestras de bomba sin software para iniciar pruebas de integración. Cortar relación comercial con Bourge de forma profesional."
        ],
        "estado": "contactado",
        "email": "jhualde@lizarte.com"
      },
      "departamento": "Innovación",
      "prioridad": 3,
      "fotos_extra": [],
      "respuestas": [
        {
          "texto": "Hay dos modelos de tamaño, una que tiene la base mayor que otra. La bomba de mayor tamaño, la hay en 12V y 24V, la que nos interesa es la de 12V. Pero la más apropiada es la del tamaño pequeño. En la fabrica me confirmaron que hay de 12V pero ahora me dicen que hay que desarrollarla y que son 50K$. También pido precios a Shirley (bomba tamaño grande), precio unidad 590$, por 100 uds a 560$ y 1200 uds a 430$. Solicito una muestra gratuita. \nTambién voy a pedir precio a Cathy de Quanxing. ",
          "formato": {
            "negrita": false,
            "lista": false
          }
        }
      ],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "CIPE Breaking Systems Technology",
      "person": "Fiona Lu; sales02@ckgautoparts.com",
      "product": "EPB",
      "time": "11:29",
      "stand": "Hall 6.1 E02",
      "comments": "Fabricante chino especializado en componentes de <b>sistemas de freno hidráulico: pinzas, servofrenos y bombas de freno.</b> Suministran a OEMs como Ford y Nissan. Disponen de capacidad de I+D y fabricación avanzada para componentes de freno de disco y tambor, con enfoque en calidad y tecnología. Integran sistemas ABS y controles electrónicos en sus desarrollos.",
      "id": 1763954957878,
      "fotos": [],
      "seguimiento": {
        "responsable": "Comercial",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "pendiente",
        "email": ""
      },
      "departamento": "Innovación",
      "prioridad": 1,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "Taizhou EBS Auto Parts Co., Ltd.",
      "person": "Stefen Dong; ebs@ebsbrake.com",
      "product": "EPB y pinzas de freno",
      "time": "11:34",
      "stand": "Hall 3 E56",
      "comments": "Empresa que ofrece <b>frenos de estacionamiento eléctricos (EPB) y pinzas de freno, tanto mecánicas como electrónicas.</b> Trabajan con referencias para Volkswagen y BMW, marcas de alto volumen en el parque europeo.\nLos sistemas EPB están cada vez más presentes en vehículos modernos, lo que genera una demanda creciente de recambios. Posicionarse en este mercado ahora puede suponer una ventaja competitiva a medio plazo.",
      "id": 1763955286688,
      "fotos": [],
      "seguimiento": {
        "responsable": "Comercial",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Solicitar catálogo con referencias y precios. Valorar si encaja como nueva línea de producto complementaria al catálogo actual."
        ],
        "estado": "pendiente",
        "email": "krum@lizarte.com"
      },
      "departamento": "Innovación",
      "prioridad": 1,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "UKAT",
      "person": "Molly",
      "product": "No especifica en el email",
      "time": "12:13",
      "stand": "Hall 7.1 E76",
      "comments": "Proveedor de propshaft(cardan), primera opción de proveedor hasta que llego Stone. ",
      "id": 1763957620217,
      "fotos": [],
      "seguimiento": {
        "responsable": "",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "finalizado"
      },
      "departamento": "Lizarte",
      "prioridad": 3,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "EBI Bearing",
      "person": "John Zhao; johnzhao@ebi-bearings.com",
      "product": "Rodamientos",
      "time": "12:15",
      "stand": "Hall 1.1 D33",
      "comments": "Interesante opción para comprar <b>rodamientos </b>directamente en China y reducir costes de aprovisionamiento. El producto expuesto en el stand me ha causado buena impresión, con un acabado y calidad aparentemente aceptables para nuestras aplicaciones.\nComprar rodamientos en origen podría suponer un ahorro significativo en un componente de consumo recurrente que actualmente adquirimos a proveedores locales o europeos con márgenes añadidos.",
      "id": 1763957712020,
      "fotos": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Siguiente paso: solicitar muestras de las referencias top que estamos comprando actualmente para poder compararlas con nuestros proveedores habituales.",
          "Muy importante que Calidad de el OK tras las verificaciones pertinentes. "
        ],
        "estado": "contactado",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 0,
      "fotos_extra": [],
      "respuestas": [
        {
          "texto": "A la espera de que Compras mande el nuestro TopVentas, para que el proveedor nos envié muestras para Calidad y comprobar la calidad de los rodamientos. \nEn caso de dudas, quizás puedo hablar con SKT(Tudela), para saber cómo homologar los rodamientos. ",
          "formato": {
            "negrita": false,
            "lista": false
          }
        }
      ],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "AIERFU",
      "person": "Dane",
      "product": "Direcciones",
      "time": "19:32",
      "stand": "Hall 6.1 F55",
      "comments": "Me he reunido con Dane, quien quiere convertirse en nuestro proveedor principal. Le he comentado que primero necesita hablar con Javier respecto a los targets de precio, y que Calidad debe validar las piezas. Si todo está OK, lo valoraremos.\nYa nos han enviado dos cremalleras de DAES para pruebas.\nValoración: Es muy interesante homologar <b>cremalleras para DAES.</b> Aunque actualmente el precio por unidad puede ser alto por ser un producto nuevo en el mercado, en cuanto los precios bajen será estratégico para Lizarte tener este componente ya homologado y un proveedor validado.",
      "id": 1763983993823,
      "fotos": [
        "fotos/reunion_aierfu_foto1.jpg"
      ],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Pedir muestra de NCR 06965600 Passat y Tiguan; B8 importante ",
          "Hablar con Dane para preguntar quién solicito las muestras, son para BMW pero salta la parte del usillo en el cremallera o es así?",
          "Revisar catalogo del proveedor",
          "Contactar con Dane: Preguntar si tienen medios y cómo hacen para medir la holgura entre el husillo y sin fin. (Mostrar interés\"\"\")"
        ],
        "estado": "pendiente",
        "email": "krum@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 0,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "YLCNC",
      "person": "Kairi Ban; gongxue2@yuliancn.com",
      "product": "Conectores LizOn",
      "time": "10:00",
      "stand": "Hall 4.1 C56",
      "comments": "Proveedor de <b>conectores </b>de todo tipo. Como se puede observar en la foto, disponen de una amplia gama de referencias. Podrían servir tanto <b>para la línea general como para LizOn.</b>\nValorar como alternativa a Shungbang para diversificar proveedores o mejorar condiciones.",
      "id": 1764122436398,
      "fotos": [
        "fotos/reunion_ylcnc_foto2.jpg",
        "fotos/reunion_ylcnc_foto1.jpg"
      ],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Mandar los productos que estamos ahora comprando a China para ver si tienen stock, precio y nuevos productos."
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 3,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "- Cangzhou Fubang",
      "person": "-Lucy",
      "product": "Conectores LizOn",
      "time": "10:17",
      "stand": "Hall 4.1 H119",
      "comments": "Proveedor de <b>conectores </b>de todo tipo. Como se puede observar en la foto, disponen de una amplia gama de referencias. Podrían servir tanto <b>para la línea general como para LizOn.</b>\nValorar como alternativa a Shungbang para diversificar proveedores o mejorar condiciones. Ojo tiene el mismo tamaño que ShungBang, proveedor actual. Puede parecer stand pequeño pero tiene potencial.",
      "id": 1764123486251,
      "fotos": [
        "fotos/reunion___cangzhou_fubang_foto2.jpg",
        "fotos/reunion___cangzhou_fubang_foto1.jpg"
      ],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Mandar los productos que estamos ahora comprando a China para ver si tienen stock, precio y nuevos productos."
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 3,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "YANGYU",
      "person": "Vida Hong; vida@rayangyu.com",
      "product": "EGR Valve",
      "time": "10:31",
      "stand": "Hall 4.1 E43",
      "comments": "Proveedor de <b>EGR </b>– <b>Marca reconocida en Europa</b>\nEmpresa que dispone de muchas referencias de válvulas EGR en su catálogo, lo que indica una buena cobertura de aplicaciones para el mercado europeo. Un detalle interesante es que nos conocen como marca reconocida en Europa, lo cual habla bien de la reputación que Lizarte ha construido en el sector. Sin embargo, curiosamente, hasta ahora no habían contactado con nosotros a pesar de conocernos.\nEl proveedor tiene buena pinta para válvulas EGR, tanto por la variedad de referencias como por la impresión general transmitida durante la feria. El hecho de que conozcan el mercado europeo y nuestra posición en él es un punto a favor, ya que facilita el entendimiento mutuo de las necesidades y estándares de calidad requeridos.\n\nValoración: Merece la pena explorar la posibilidad de colaboración. <b>Podría convertirse en un proveedor alternativo o complementario para nuestra línea de EGR.</b>",
      "id": 1764124295568,
      "fotos": [
        "fotos/reunion_yangyu_foto1.jpg",
        "fotos/reunion_yangyu_foto2.jpg",
        "fotos/reunion_yangyu_foto3.jpg"
      ],
      "seguimiento": {
        "responsable": "Innovación",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Solicitar catálogo completo y más información sobre su gama de producto. Identificar qué referencias coinciden con las que actualmente comercializamos o podríamos incorporar, y pedir precios para comparar con los proveedores actuales y compartir con Richard."
        ],
        "estado": "pendiente",
        "email": "krum@lizarte.com"
      },
      "departamento": "Innovación",
      "prioridad": 0,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "Matteo Vehicle Parts Factory",
      "person": "Marco (General Manager); 2826664554@qq.com",
      "product": "Relen",
      "time": "10:44",
      "stand": "Hall 4.1 B61",
      "comments": "Empresa especializada en <b>relés </b>de todo tipo y para distintos amperajes. Disponen de una gama amplia que podría cubrir nuestras necesidades de componentes eléctricos en diferentes aplicaciones, tanto <b>para la línea general de Lizarte como para LizOn.</b>\nTener un proveedor directo de relés en China podría reducir costes respecto a los intermediarios actuales y asegurar disponibilidad de un componente que usamos de forma recurrente.",
      "id": 1764125076721,
      "fotos": [
        "fotos/reunion_matteo_vehicle_parts_factory_foto1.jpg",
        "fotos/reunion_matteo_vehicle_parts_factory_foto2.jpg"
      ],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Contactar con ellos para consultar si disponen del relé que actualmente compramos a Altezza y solicitar precio directo. De esta forma, podríamos evitar intermediarios y mejorar costes."
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 3,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "KITPAMT",
      "person": "Ms. Anna; anayang1311@gmail.com",
      "product": "DAES Y COMPONENTES DEAS",
      "time": "11:31",
      "stand": "Hall 5.1 D111",
      "comments": "<div>anayang1311@gmail.com</div><div><br></div>Este proveedor me ha parecido muy interesante por la variedad de componentes que ofrecen:\n\n<b>Rodamientos de aguja\nRodamientos normales y de gran tamaño\nCarcasas\nTapas de conectores\nCorreas\nCables\n</b>\nTambién tienen posicionadores, aunque son diferentes a los que usamos habitualmente. Disponen de <b>sensor de piñón</b> para 06964000, lo cual podría ser relevante para nuestra línea.",
      "id": 1764127927936,
      "fotos": [
        "fotos/reunion_kitpamt_foto1.jpg",
        "fotos/reunion_kitpamt_foto3.jpg",
        "fotos/reunion_kitpamt_foto2.jpg"
      ],
      "seguimiento": {
        "responsable": "Calidad",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Pedir catálogo poner en copia a JH,JB,JB",
          "Muy interesante para componentes de Encory, también tienen cremalleras con husillos.",
          ""
        ],
        "estado": "contactado",
        "email": "jhualde@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 0,
      "fotos_extra": [],
      "respuestas": [
        {
          "texto": "Hemos comprobado el sensor de la 06964000 y funciona correctamente, solicito precio. El turco nos los ofrece a 40€ y el proveedor a 11$. ",
          "formato": {
            "negrita": false,
            "lista": false
          }
        }
      ],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "QUANBANG",
      "person": "Con Liu",
      "product": "Direcciones y Terminales",
      "time": "12:00",
      "stand": "Hall 5.1 F99",
      "comments": "Empresa que comercializa direcciones hidráulicas completas. Sin embargo, lo más destacable de este proveedor es que también <b>venden terminales </b>como componente separado, algo que no todos los proveedores ofrecen y que podría resultar interesante para nuestras necesidades de recambio y reparación.\n",
      "id": 1764129667486,
      "fotos": [
        "fotos/reunion_quanbang_foto1.jpg"
      ],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Solicitar el catálogo de terminales. Una vez recibido, compartir con Javier Baztán para revisar las referencias disponibles, valorar si encajan con nuestras aplicaciones y solicitar precios para comparar con los proveedores actuales.\n",
          "Valorar la opción de comprar terminales en chiva vs Proceso Actual."
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 0,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "YUGFROST",
      "person": "David Gontmakher( Manager)",
      "product": "Aires acondicionados para camiones",
      "time": "12:08",
      "stand": "Hall 5.1 K64",
      "comments": "Son dos compañías en una, con presencia tanto en Rusia como en China, lo que les da capacidad de fabricación y distribución en distintos mercados. Se dedican a fabricar sistemas de aire acondicionado para camiones, diseñados específicamente para su uso en parada: cuando el camionero está descansando, puede mantener el aire encendido sin necesidad de tener el motor en marcha, lo cual supone un ahorro de combustible y mayor confort para el conductor.\nEl sistema incorpora una protección automática inteligente que apaga el equipo cuando la batería baja del 30%, evitando así que el camión se quede sin carga suficiente para arrancar. Un detalle técnico bien pensado que evita problemas al usuario final.\nOfrecen la posibilidad de personalizar los productos con nuestra caja y marca, de forma que podríamos comercializarlos directamente bajo el nombre Lizarte sin necesidad de desarrollar producto propio. Podría ser una línea interesante para diversificar el catálogo y entrar en el segmento de vehículo industrial.\nNota: Durante la feria se veían muchos stands ofreciendo productos similares, lo que indica que hay demanda y potencial de mercado real. Valorar la idea como posible nuevo producto a comercializar.",
      "id": 1764130099961,
      "fotos": [
        "fotos/reunion_yugfrost_foto2.jpg",
        "fotos/reunion_yugfrost_foto1.jpg"
      ],
      "seguimiento": {
        "responsable": "Dirección",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Valorar la idea como posible producto a comercializar. Había muchos stands en la feria ofreciendo productos similares, lo que indica que hay demanda y potencial de mercado. Merece la pena estudiarlo con más detalle.",
          "ThermoKing análizar Krum"
        ],
        "estado": "pendiente",
        "email": "krum@lizarte.com"
      },
      "departamento": "Innovación",
      "prioridad": 1,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "FOBAUTOPARTS",
      "person": "Jack Tao y Jared Chen; jack@fobautoparts.com & sales04@fobautoparts.com",
      "product": "Direcciones",
      "time": "12:42",
      "stand": "Hall 6.1 F100",
      "comments": "Empresa comercializadora – <b>Servicios de agrupación e inspección</b>\nSe trata de una empresa comercializadora, no de un fabricante directo. Ofrecen varios servicios interesantes:\n\nAgrupación de pedidos: Pueden consolidar material de distintos proveedores en un único envío.\nInspección previa al envío: Revisan el producto antes de mandarlo y nos pueden enviar fotos como evidencia de que todo está en orden.\n\nEn cuanto a productos, comentan que las bombas las compran a Quanxing, pero las direcciones las fabrican ellos mismos. También ofrecen transmisiones, que según dicen las adquieren a GSP. La diferencia es que GSP no permite poner nuestra marca en el producto, pero ellos sí podrían hacerlo.\nAdemás, pueden darnos referencias de otras empresas o incluso acompañarnos a visitarlas para verificar las instalaciones de los fabricantes.\n\nPuede parecer interesante plantearlos como una empresa que nos haga de intermediario de confianza en China: <b>agrupación de material, control de calidad e inspección antes del envío. Podría simplificarnos la gestión logística y darnos mayor seguridad en los pedidos(SERVICIO).</b> (Esta idea se comentó hace varios años, ahora mismo no se si es prioritario).",
      "id": 1764132222182,
      "fotos": [
        "fotos/reunion_fobautoparts_foto1.jpg",
        "fotos/reunion_fobautoparts_foto3.jpg",
        "fotos/reunion_fobautoparts_foto2.jpg"
      ],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Pedir catálogo de otros productos que comercializan, como por ejemplo bombas de gasolina (las que van desde el depósito hacia el motor), para valorar la opción de incluirlas en nuestro catálogo."
        ],
        "estado": "pendiente",
        "email": "krum@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 3,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "CHANGHI",
      "person": "Jason Bai",
      "product": "DAES",
      "time": "13:39",
      "stand": "Hall 6.1 F01",
      "comments": "Problemas para recuperar la información. ",
      "id": 1764135592052,
      "fotos": [],
      "seguimiento": {
        "responsable": "",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "pendiente"
      },
      "departamento": "Lizarte",
      "prioridad": 1,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "WINNER AUTOPARTS",
      "person": "Eve Xu; evexu@winner-parts.com",
      "product": "EGR",
      "time": "14:19",
      "stand": "Hall 2.1 A96",
      "comments": "Sin duda, la <b>mejor empresa que he visto en la feria para válvulas EGR.</b> Destacan notablemente por tener equipos de verificación expuestos directamente en el stand, lo que demuestra un enfoque serio y profesional en el control de calidad de sus productos. No es habitual ver este nivel de transparencia en los fabricantes.\nAdemás de las válvulas EGR, <b>también disponen de productos relacionados con sistemas AdBlue</b>, lo cual amplía su catálogo hacia el tratamiento de emisiones en vehículos diésel modernos. Podría ser interesante valorar esta línea también.\n\nIdea a valorar: Durante la conversación <b>hemos comentado la posibilidad de adquirir uno de sus equipos de verificación para realizar test internos de calidad en Lizarte.</b> Contar con esta capacidad nos permitiría validar el producto recibido de cualquier proveedor y asegurar el nivel de calidad antes de su comercialización, reduciendo así el riesgo de reclamaciones y mejorando la confianza en el producto final.",
      "id": 1764137943163,
      "fotos": [
        "fotos/reunion_winner_autoparts_foto3.jpg",
        "fotos/reunion_winner_autoparts_foto1.jpg",
        "fotos/reunion_winner_autoparts_foto2.jpg"
      ],
      "seguimiento": {
        "responsable": "Comercial",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Contactar para pedir catálogo de las referencias que tienen de EGR y AdBlue."
        ],
        "estado": "pendiente",
        "email": "krum@lizarte.com"
      },
      "departamento": "Innovación",
      "prioridad": 0,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "SEINECA",
      "person": "Luis Yu; service3@seineca.com",
      "product": "CV JOINT",
      "time": "16:24",
      "stand": "Hall 3 K60",
      "comments": "Es una empresa fundada en 2010 y fabrican directamente, no son comercializadores. Esto es un punto a favor en cuanto a control de calidad y trazabilidad del producto.\nPendiente recibir por email:\n\nListado de referencias fast mover en Europa con sus códigos OEM correspondientes.\n<br>",
      "id": 1764145484162,
      "fotos": [
        "fotos/reunion_seineca_foto1.jpg"
      ],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Pedir ambos catálogos de los dos productos."
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 3,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "CHIBOSS",
      "person": "Levi & Hancy; levi@chiboss.cn & Hancy@chiboss.cn",
      "product": "Correas EPS",
      "time": "09:45",
      "stand": "Hall 3.1 H123",
      "comments": "Empresa especializada en la fabricación de correas de todo tipo, incluyendo las que necesitamos para nuestras aplicaciones actuales. Además, disponen de versiones más finas que podrían ser útiles para otras referencias donde el espacio o las especificaciones técnicas requieran un perfil más reducido. Esta variedad de gama demuestra capacidad de fabricación flexible.\n\nHa sido <b>uno de los mejores stands que he visto en toda la feria</b>, tanto por la presentación del producto como por la atención recibida y la profesionalidad mostrada. Da confianza como potencial proveedor.\n\nContacto: Hancy@chiboss.cn",
      "id": 1764207955485,
      "fotos": [
        "fotos/reunion_chiboss_foto2.jpg",
        "fotos/reunion_chiboss_foto1.jpg"
      ],
      "seguimiento": {
        "responsable": "Calidad",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Pedir referencias de Encory y precios para valorar vs proveedor actual",
          "Se ha mandado email con las medidas para solicitar muestras. Verificar las dimensiones y Javier B. pedir muestras"
        ],
        "estado": "contactado",
        "email": "jbobadilla@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 0,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "ZFYLCD",
      "person": "Karol y lilei; jtyl13633187801@163.com",
      "product": "Cardans",
      "time": "10:07",
      "stand": "Hall 1.1 E01",
      "comments": "Empresa que vende <b>cardans </b>y que tiene buena pinta a primera vista. Las piezas expuestas en el stand se ven bien acabadas, con un nivel de calidad aparente más que aceptable. Es cierto que lógicamente habrán llevado el mejor producto posible para la feria, pero aun así la impresión general es positiva y merece la pena explorar una posible colaboración.\nUn punto importante es que comentan trabajar con vehículos del parque europeo, lo cual es especialmente relevante para nuestro mercado y nos asegura que sus referencias podrían encajar directamente con las aplicaciones que manejamos. No siempre los proveedores chinos tienen cobertura de vehículos europeos, por lo que esto es un valor añadido.\n\nAcción: Pendiente recibir catálogo con las referencias disponibles. Revisar cobertura de vehículos y valorar si encaja con nuestra línea de producto para posibles compras o diversificación de proveedores.",
      "id": 1764209275780,
      "fotos": [
        "fotos/reunion_zfylcd_foto2.jpg",
        "fotos/reunion_zfylcd_foto1.jpg"
      ],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Solicitar catálogo con las referencias disponibles. Revisar cobertura de vehículos y valorar si encaja con nuestra línea de producto para posibles compras o diversificación de proveedores."
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 3,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "WUXI BELT",
      "person": "Hanna; wxjudy@wuxibelt.cn",
      "product": "Correas para DAES",
      "time": "10:14",
      "stand": "Hall 1.1",
      "comments": "Otro proveedor de <b>correas </b>identificado durante la feria. Supone una alternativa adicional para diversificar las opciones de suministro en este tipo de componente, algo importante para no depender de un único proveedor y poder negociar mejores condiciones.\n<b>Tener varias opciones de proveedores de correas nos permite comparar calidad, precio y plazos de entrega, además de contar con un plan B en caso de problemas de suministro con el proveedor principal. Dado que nuestra demanda es baja, mejor solo tener dos proveedores o pedir precio a dos empresas. </b>",
      "id": 1764209654681,
      "fotos": [
        "fotos/reunion_wuxi_belt_foto1.jpg",
        "fotos/reunion_wuxi_belt_foto2.jpg"
      ],
      "seguimiento": {
        "responsable": "Calidad",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Solicitar correas de Encory para comparar calidad y precio con otros proveedores contactados en la feria.",
          "Pedidas las medidas a I+D para contactar con el proveedor"
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "prioridad": 1,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "company": "TENDA TEC",
      "person": "Jim Lee; jim@tendaparts.com",
      "product": "EGR",
      "time": "10:26",
      "stand": "Hall 1.1",
      "comments": "Empresa que vende <b>válvulas EGR</b>. Me ha gustado mucho su stand, transmitía una imagen muy profesional y cuidada, lo que ya de entrada genera buena impresión sobre la seriedad de la empresa.\nDurante la conversación, <b>comentan que suministran directamente a Bosch y me han mostrado fotos como prueba de esta colaboración.</b> Además, me han indicado que en el propio stand de Bosch durante la feria estaba expuesto su producto. Para verificarlo, he visitado el stand de Bosch y efectivamente, aparentemente se trata del mismo producto que ofrece este proveedor.\n\nEsto da mucha confianza: si trabajan con Bosch, el nivel de exigencia y control de calidad al que están sometidos debe ser muy alto. Bosch no trabaja con cualquier proveedor, por lo que esta relación comercial actúa como un aval importante de su capacidad productiva y calidad de producto. Disponen además de <b>muchas referencias en su catálogo</b>, lo que indica una buena cobertura de aplicaciones.\n\nValoración: <b>Proveedor a tener muy en cuenta para válvulas EGR</b>. La relación con Bosch es un respaldo significativo que reduce el riesgo de problemas de calidad.",
      "id": 1764210396599,
      "fotos": [
        "fotos/reunion_tenda_tec_foto2.jpg",
        "fotos/reunion_tenda_tec_foto1.jpg"
      ],
      "seguimiento": {
        "responsable": "Comercial",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Acción: Pedir catálogo completo con todas las referencias y solicitar específicamente el listado de referencias que suministran a Bosch."
        ],
        "estado": "pendiente",
        "email": "krum@lizarte.com"
      },
      "departamento": "Innovación",
      "prioridad": 0,
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "1765886037129",
      "company": "MVA SPARES",
      "person": "Boryana Kolev; boryanakolev@gmail.com",
      "product": "Refabricación LizOn",
      "time": "",
      "stand": "",
      "comments": "<b>Empresa gestionada por búlgaros con sede en Sudáfrica.</b> Les conocí de forma casual en la feria mientras ellos también buscaban productos y proveedores, igual que yo. Me presenté y les expliqué a qué nos dedicamos en Lizarte. Desde el primer momento mostraron gran interés en la sección de LizOn, especialmente en todo lo relacionado con mecatrónica.\n<b>Su objetivo es comenzar a hacer remanufacturado de mecatrónica en su empresa,</b> pero actualmente tienen pocos conocimientos técnicos en este ámbito. Se encuentran en una fase inicial donde necesitan tanto producto como formación y equipamiento. Esta situación abre varias oportunidades de negocio interesantes para nosotros:\n<b>Posibles líneas de colaboración:</b>\n\n<b>Venta de producto LizOn</b>: Están interesados en adquirir producto terminado para comercializar en su mercado. Ojo: el retorno del casco podría ser un problema logístico importante debido a la distancia con Sudáfrica. Habría que valorar si compensa económicamente o si se plantea un modelo sin retorno con ajuste de precio.\n<b>Venta de SmartCan</b>: Opción más sencilla desde el punto de vista logístico, ya que no requiere gestionar el retorno de cascos. Podría ser la vía más práctica para iniciar la relación comercial.\n\n<b>Formación en reman:</b> Posibilidad de venderles formación técnica en remanufacturado de mecatrónica. Esta podría ser una vía de ingresos muy interesante y además abriría la puerta a futuras ventas de equipamiento, herramientas y producto. Formarles crea dependencia positiva con Lizarte como referente técnico.\n\nContacto interesante para desarrollar negocio en el mercado africano, una zona donde actualmente no tenemos presencia directa. <b>Explorar qué línea de colaboración encaja mejor</b> según sus necesidades reales y nuestra capacidad logística. Mantener el contacto activo.",
      "departamento": "Innovación",
      "prioridad": 0,
      "fotos": [],
      "fotos_extra": [],
      "seguimiento": {
        "responsable": "Dirección",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Primera toma de contacto, ya hecha. ",
          "Explorar qué posibilidades reales hay de trabajar con ellos. Contactar para conocer mejor sus necesidades concretas, capacidad de inversión y volumen potencial. A partir de ahí, definir cuál de las líneas de colaboración tiene más sentido iniciar: producto terminado, SmartCan o formación. Mantener el contacto activo y no dejar enfriar la relación."
        ],
        "estado": "contactado",
        "email": "oscar@lizarte.com"
      },
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "1765892785333",
      "company": "YBZC BEARING ",
      "person": "Mingzhu Li",
      "product": "Rodamientos para Bombas y Direcciones",
      "time": "",
      "stand": "",
      "comments": "Empresa especializada en la <b>fabricación de rodamientos de todo tipo,</b> con una amplia gama de referencias y tamaños. Durante la visita al stand, he identificado rodamientos específicos para bombas, direcciones y otros de mayor diámetro que también podrían encajar con nuestras necesidades.\nEste proveedor resulta especialmente interesante porque abre la posibilidad de homologar y comprar rodamientos directamente en China para reducir costes, algo que hasta ahora nunca hemos hecho en Lizarte. Actualmente dependemos de proveedores locales o europeos para este componente, por lo que explorar la opción china podría suponer un ahorro significativo en un producto de alto consumo.\n\nLógicamente, antes de dar el paso sería necesario realizar un <b>proceso de homologación</b> riguroso para asegurar que la calidad cumple con nuestros estándares, pero si las muestras superan las pruebas, podría convertirse en una fuente de aprovisionamiento muy competitiva.\n\nContacto; 2592274187@qq.com",
      "departamento": "Lizarte",
      "prioridad": 1,
      "fotos": [],
      "fotos_extra": [],
      "seguimiento": {
        "responsable": "Calidad",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Solicitar muestras de las referencias de rodamientos que más consumimos actualmente (bombas, direcciones y los de mayor diámetro identificados). Realizar pruebas de homologación internas y, si la calidad lo permite, valorar el cambio de proveedor o al menos incorporarlo como alternativa para reducir costes."
        ],
        "estado": "pendiente",
        "email": "jhualde@lizarte.com"
      },
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    }
  ],
  "adicional": [
    {
      "id": "add_1",
      "empresa": "N.F.YO",
      "producto": "Ruedas y neumáticos",
      "notas": "NFYO – Oportunidad de diversificación con <b>neumáticos</b>\n\nHe visitado el stand de NFYO y tras una conversación con Lucy, me ha revelado información muy interesante: han comprado recientemente una empresa dedicada a la fabricación de neumáticos, lo que amplía significativamente su portfolio de productos.\nLe he comentado que estamos interesados en diversificar con nuevas líneas de negocio y le he preguntado si habría opción de valorar la idea de comercializar neumáticos a través de Lizarte. Su respuesta ha sido positiva: sí estarían interesados. Además, me ha comentado que podríamos tener la exclusiva de ventas, aunque necesito confirmar si sería exclusiva para España o para toda Europa. Creo recordar que mencionó Europa, pero no estoy al 100% seguro, por lo que es un punto a aclarar en el siguiente contacto.\n\n<b>Ofrecen neumáticos</b> para diferentes tipos de vehículos<b>: coches, motos y tractores</b>. Este último segmento resulta especialmente atractivo, ya que en España las ruedas de tractores son extremadamente caras. Si conseguimos ofrecer un producto de calidad aceptable a un precio competitivo, podría haber un nicho de mercado muy interesante en el sector agrícola.\n\nValoración: Oportunidad de diversificación importante que podría abrir una nueva línea de negocio completamente diferente a lo que hacemos actualmente. La exclusividad de ventas (si se confirma para Europa) sería un valor añadido enorme.",
      "oportunidad": "Exclusividad territorial – Si se confirma la exclusiva para España o Europa, tendríamos el mercado cerrado para nosotros con ese producto. Eso es una ventaja competitiva muy potente.\n\nNeumáticos de tractor – Nicho de alto margen – Esta es probablemente la más interesante. Si en España las ruedas de tractor son extremadamente caras, hay un hueco claro para entrar con un producto de precio competitivo. El sector agrícola necesita neumáticos de forma recurrente y el agricultor busca reducir costes. Podríamos ofrecer una alternativa más económica sin sacrificar demasiado en calidad.\n\nDiversificación de líneas de producto – Salir del sector tradicional de Lizarte (dirección, bombas, etc.) y entrar en neumáticos abre un mercado completamente nuevo con clientes potencialmente diferentes.\n\nAcceso directo a fabricante – NFYO ha comprado la fábrica, por lo que no hay intermediarios. Eso permite negociar mejores precios y márgenes.\n\nResumen: La oportunidad más clara es atacar el nicho de neumáticos de tractor en España, donde el precio actual del mercado es muy alto y hay margen para entrar con una oferta más competitiva, especialmente si contamos con exclusividad.",
      "prioridad": 1,
      "seguimiento": {
        "responsable": "Innovación",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Contactar con Lucy para confirmar el alcance territorial de la exclusiva (España o Europa), solicitar catálogo de neumáticos con referencias y precios, y valorar internamente si esta línea de negocio encaja con la estrategia de Lizarte. Especial atención a las ruedas de tractor por el potencial de margen en el mercado español."
        ],
        "estado": "pendiente",
        "email": "krum@lizarte.com"
      },
      "departamento": "Innovación",
      "fotos": [],
      "fotos_extra": [],
      "respuestas": [
        {
          "texto": "Óscar, se aleja de nuestro cliente. Tendríamos que decirnos si proveer a alguna marca famosa de tractores.  ",
          "formato": {
            "negrita": false,
            "lista": false
          }
        }
      ],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_2",
      "empresa": "YARN ",
      "producto": "Cabezas de inyectores Diesel",
      "notas": "Contacto; kathy@yarncm.com\n\nProveedor de inyectores diésel – <b>Cabezas de inyector</b>\n\nEmpresa especializada en inyectores diésel que también comercializa cabezas de inyector como componente separado. Este es un punto especialmente relevante, ya que las cabezas de inyector son un producto que actualmente necesitamos en Lizarte y no siempre es fácil encontrar proveedores que las ofrezcan de forma independiente.\n\nSe trata de un producto muy interesante. En España, el precio de mercado de las cabezas de inyector es alto, lo que abre una oportunidad clara para mejorar márgenes si conseguimos un proveedor competitivo en origen. Al ser un componente específico y no un producto de gran volumen generalista, hay menos competencia y más margen de maniobra en la comercialización.",
      "oportunidad": "El mercado español tiene precios elevados en este producto, por lo que si conseguimos aprovisionarnos directamente de este fabricante a buen precio, podemos:\n\nCubrir nuestra propia necesidad interna a menor coste.\nComercializar las cabezas de inyector en el mercado español con un margen atractivo, aprovechando que la competencia vende caro.\nPosicionarnos como alternativa competitiva en un nicho donde pocos operadores están entrando con producto de origen chino.",
      "prioridad": 3,
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "JB, tenemos casquero que verifica las cabezas y nos mando solo material bueno. "
        ],
        "estado": "contactado",
        "email": "jbaztan@lziarte.com"
      },
      "departamento": "Lizarte",
      "fotos": [],
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_3",
      "empresa": "Máquinas equilibrado",
      "producto": "Máquinas de equilibrado y cambio de ruedas",
      "notas": "Contacto; Chen Li; sales1@trainsway.com\n\nDurante la feria he visto varias empresas que ofrecen <b>máquinas de equilibrado y cambio de ruedas.</b> Es un producto que tiene muy buena salida en el mercado europeo, especialmente en talleres mecánicos que necesitan renovar o ampliar su equipamiento sin realizar grandes inversiones.\nEl contexto de mercado es favorable: las máquinas alemanas, que tradicionalmente dominan el sector, son muy caras y no todos los talleres pueden permitírselas, especialmente los más pequeños o los que están empezando. Por otro lado, las máquinas chinas han mejorado mucho en calidad y funcionan bien para el uso diario de un taller estándar, todo ello a un precio significativamente más competitivo.\n Esta diferencia de precio sin una pérdida notable de prestaciones es lo que está impulsando la demanda.",
      "oportunidad": "Existe un hueco claro en el mercado para ofrecer máquinas de equilibrado y cambio de ruedas de origen chino a talleres europeos que buscan una alternativa económica(al igual que los elevadores, como el que tenemos nosotros) a las marcas alemanas premium. Los talleres pequeños y medianos son especialmente sensibles al precio y estarían dispuestos a comprar maquinaria china si alguien de confianza se la ofrece con garantía y servicio postventa.\nLizarte, con su red de contactos en el sector del recambio y su reputación como marca reconocida en Europa, podría:\n\nComercializar estas máquinas como complemento a su catálogo actual, ampliando la oferta hacia equipamiento de taller.\nOfrecer un pack completo: máquinas + servicio técnico + garantía, lo que generaría confianza en el comprador.\nAprovechar la relación con talleres que ya compran productos Lizarte para hacer venta cruzada de este equipamiento.\n\nAl haber visto varias empresas con este producto en la feria, hay margen para comparar proveedores y elegir el que mejor relación calidad-precio-servicio ofrezca.",
      "prioridad": 2,
      "seguimiento": {
        "responsable": "Innovación",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "pendiente",
        "email": "krum@lizarte.com"
      },
      "departamento": "Innovación",
      "fotos": [],
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_4",
      "empresa": "GL Link, Shenzhen Jinyang Electronic Technology",
      "producto": "Conectores, cables y componentes eléctricos",
      "notas": "Contacto; yuyanyiya@126.com\n\nEmpresa que ofrece <b>conectores, cables y componentes eléctricos de todo tipo</b>. Dentro de su gama, destacan e<b>specialmente los accesorios para cables y conectores OBD</b>, un producto muy específico que no siempre es fácil encontrar con variedad de referencias y a buen precio.\nEste tipo de producto tiene una doble vertiente de interés:\n<b><font color=\"#1dd396\">Para comercialización:</font></b>\nExiste un mercado para accesorios OBD, aunque probablemente sea un mercado pequeño y de nicho. Los compradores potenciales serían talleres especializados en diagnosis, empresas de equipamiento de taller y profesionales que trabajan con herramientas de diagnóstico. No sería un producto de gran volumen, pero podría ser un complemento interesante al catálogo si los márgenes son buenos.\n<b><font color=\"#15e5a0\">Para uso interno (más interesante):</font></b>\nProbablemente el mayor valor de este proveedor esté en cubrir nuestras propias necesidades internas. En Lizarte y especialmente en LizOn, trabajamos con componentes eléctricos, conectores y cables de forma habitual. Tener un proveedor fiable y competitivo en precio para este tipo de material podría reducir costes de aprovisionamiento y asegurarnos disponibilidad de componentes que a veces son difíciles de conseguir.",
      "oportunidad": "La oportunidad principal aquí no está tanto en la comercialización externa (mercado limitado), sino en el ahorro de costes interno. Si conseguimos aprovisionarnos de conectores, cables y accesorios OBD directamente de este proveedor a precios competitivos, podemos:\n\nReducir el coste de los componentes que usamos en producción y reparación.\nTener un proveedor alternativo para materiales que actualmente compramos a otros, mejorando nuestra capacidad de negociación.\nDisponer de stock de componentes eléctricos difíciles de encontrar en el mercado local.\n\nPoner a Pablo en copia.",
      "prioridad": 2,
      "seguimiento": {
        "responsable": "Calidad",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "Email con fotos componentes eléctricos necesarios",
        "fechaSeguimiento": "",
        "acciones": [
          "Revisar el catálogo en detalle cuando lo recibamos y cruzarlo con nuestras necesidades internas actuales (tanto en Lizarte como en LizOn). Identificar qué referencias consumimos habitualmente y solicitar precios para comparar con los proveedores actuales. Si la comercialización tiene sentido, valorarlo como segunda opción."
        ],
        "estado": "pendiente",
        "email": "jhualde@lizarte.com"
      },
      "departamento": "Lizarte",
      "fotos": [],
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_5",
      "empresa": "C.K.T (http://www.ktf.cn) ; Tornillos para Encory",
      "producto": "Tornillos calidad 10.9/12.9, proveedor de VW",
      "notas": "Empresa fabricante de <b>tornillos de alta calidad con diferentes grados de resistencia: 8.8, 10.9 y 12.9.</b> Un punto muy relevante es que <b>fabrican directamente para Volkswagen</b>, lo cual, si se confirma, es un aval de calidad y fiabilidad enorme. VW tiene unos estándares de exigencia muy altos para sus proveedores, por lo que trabajar con ellos implica haber superado auditorías y controles de calidad rigurosos. Esto da mucha seguridad.\nDurante la conversación he detectado una oportunidad muy interesante: <b>existe la posibilidad de comprar tornillos de calidad 12.9 (la más alta) al precio de los 10.9</b>. Si esto se confirma, estaríamos obteniendo un producto de mayor resistencia y prestaciones por el mismo coste que actualmente pagamos por una calidad inferior. En aplicaciones de automoción, donde los tornillos están sometidos a esfuerzos importantes, esto supone una mejora técnica directa sin impacto en el coste.\nDatos del proveedor:\n\nEmpresa: C.K.T.\nWeb: http://www.ktf.cn\nContacto: David\nEmail: david.liu@ktf.cn",
      "oportunidad": "Esta es una oportunidad de alto valor por varios motivos:\n\nMejora de calidad sin coste adicional: Si podemos comprar tornillos 12.9 al precio de 10.9, estamos mejorando la calidad de nuestro producto final sin incrementar costes. Esto nos diferencia de la competencia y reduce el riesgo de fallos en los componentes que fabricamos o remanufacturamos.\n\nReducción de costes: Si actualmente compramos tornillos 10.9 a un proveedor europeo, es muy probable que C.K.T. pueda ofrecernos mejor precio incluso en la misma calidad. El ahorro podría ser significativo en un componente de consumo recurrente.\n\nProveedor avalado por OEM: El hecho de que trabajen para Volkswagen elimina gran parte de la incertidumbre sobre la calidad. No estamos apostando por un fabricante desconocido, sino por uno que ya ha pasado los filtros de un OEM de primer nivel.\n\nTornillería específica para automoción: No es un fabricante genérico, sino especializado en tornillos para el sector de automoción. Esto garantiza que conocen las especificaciones y requisitos del sector.",
      "prioridad": 0,
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Contactar con David lo antes posible para solicitar catálogo completo, listado de referencias que fabrican para VW, y precios para las calidades 10.9 y 12.9. Confirmar la posibilidad de obtener 12.9 al precio de 10.9. Cruzar con nuestras necesidades internas de tornillería y valorar homologación urgente si los números cuadran.",
          "Mikel Malón, está en conversación con él, para determinar la calidad de los tornillos. ",
          "Contactar de nuevo con David Liu "
        ],
        "estado": "proceso",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "fotos": [],
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_6",
      "empresa": "Herramientas Premium",
      "producto": "Puntas, herramientas, pistolas",
      "notas": "Sin duda, <b>el mejor stand de herramientas que he visto en toda la feria. JTC AUTO TOOLS</b> destaca claramente por encima del resto tanto en la presentación de sus productos como en la amplitud de su gama. La imagen profesional del stand transmite seriedad y la variedad de herramientas expuestas demuestra que tienen un catálogo muy completo para el sector de automoción. Un punto importante que he identificado durante la visita es la posibilidad de<b> utilizar este proveedor para comprar herramientas que en nuestro día a día tienen un desgaste excesivo.</b> En cualquier entorno de producción o taller, hay herramientas que se deterioran rápidamente por el uso intensivo y que necesitamos reponer con frecuencia. Si conseguimos un proveedor de calidad aceptable a buen precio, podemos reducir significativamente el coste de reposición de estas herramientas de alto consumo .Datos del proveedor:\n\nEmpresa: JTC AUTO TOOLS\nWeb: jtc.com.tw (Taiwán)\nContacto: Antony Lin\nEmail: antony@jtc.com.tw",
      "oportunidad": "Oportunidad de negocio identificada:\n\nReducción de costes en herramientas de alto desgaste: Actualmente, las herramientas que se desgastan rápidamente suponen un coste recurrente importante. Si conseguimos aprovisionarnos de un fabricante asiático de calidad a mejor precio, el ahorro acumulado a lo largo del año puede ser considerable. No hablamos de comprar herramientas baratas de mala calidad, sino de encontrar un equilibrio óptimo entre durabilidad y precio.\n\nProveedor de origen taiwanés: A diferencia de muchos fabricantes chinos, JTC es de Taiwán, donde la industria de herramientas tiene muy buena reputación por su calidad. Esto reduce el riesgo de problemas de calidad que a veces se asocian con productos de origen chino.\nPosible comercialización: Dado que es el mejor stand de herramientas de la feria, podría valorarse también la opción de comercializar algunas de sus herramientas a través de Lizarte, especialmente herramientas específicas para automoción que encajen con nuestro público objetivo (talleres, profesionales del sector). Sería una línea complementaria al recambio.\n\nEquipamiento interno: Más allá del consumible de desgaste, también podríamos valorar la compra de herramientas de mayor calidad para equipar nuestras instalaciones, mejorando la eficiencia del trabajo en producción.",
      "prioridad": 1,
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Solicitar catálogo completo a Antony Lin. Internamente, elaborar un listado de las herramientas que más consumimos por desgaste y las que necesitamos reponer con frecuencia. Cruzar ese listado con el catálogo de JTC para pedir precios específicos. Valorar también si hay herramientas interesantes para comercialización o para mejorar el equipamiento de nuestras instalaciones."
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "fotos": [],
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_7",
      "empresa": "Direct Sillones - Silvia G",
      "producto": "Direcciones",
      "notas": "Empresa que comercializa direcciones completas y que podría servir como alternativa a los proveedores actuales. Lo que más destaca de este contacto no es solo el producto en sí, sino una ventaja operativa muy importante: la persona de <b>contacto habla perfectamente castellano</b>. Este detalle, que puede parecer menor, es en realidad un plus enorme a la hora de trabajar con proveedores en China. \nLa barrera idiomática es uno de los principales problemas que surgen en las relaciones comerciales con Asia: malentendidos en especificaciones técnicas, confusiones en pedidos, errores en documentación, problemas a la hora de gestionar incidencias o reclamaciones... Todo esto se complica cuando la comunicación se hace en un inglés limitado por ambas partes o a través de traductores automáticos.\nContar con un interlocutor que hable nuestro idioma de forma fluida facilita enormemente las negociaciones, las gestiones técnicas del día a día y la resolución de cualquier problema que pueda surgir. La comunicación directa y sin barreras genera confianza y reduce errores.",
      "oportunidad": "Proveedor alternativo de direcciones: Siempre es estratégico tener alternativas a los proveedores actuales para no depender de una única fuente. Esto nos da capacidad de negociación y seguridad ante posibles problemas de suministro. Si este proveedor ofrece producto de calidad comparable a buen precio, podría entrar en nuestra cartera de proveedores.\n\nReducción de errores y costes ocultos: Trabajar con alguien que habla castellano reduce drásticamente los errores derivados de malentendidos. Estos errores tienen un coste real: pedidos incorrectos, devoluciones, retrasos, producto que no cumple especificaciones... Un proveedor con el que podamos comunicarnos sin fricciones puede acabar siendo más rentable aunque su precio no sea el más bajo del mercado.\n\nAgilidad en la gestión: Las consultas técnicas, modificaciones de pedido, gestión de incidencias y cualquier negociación se pueden resolver de forma más rápida y eficaz cuando no hay barrera idiomática. Esto ahorra tiempo y recursos internos.\nRelación comercial más sólida: La comunicación fluida permite construir una relación de confianza más fácilmente, lo que a largo plazo puede traducirse en mejores condiciones, mayor flexibilidad y un trato preferente.\n\nValoración: Tener muy en cuenta como proveedor alternativo de direcciones. Aunque el producto deba pasar igualmente un proceso de homologación y comparación de precios, la ventaja del idioma es un factor diferencial que no debemos subestimar.",
      "prioridad": 3,
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          " Solicitar catálogo de direcciones con referencias y precios. Comparar con los proveedores actuales(YAS) en términos de calidad, cobertura de referencias y precio. Si el producto es competitivo, valorar incorporarlo como segunda fuente de suministro aprovechando la facilidad de comunicación."
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "fotos": [],
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_8",
      "empresa": "NBM",
      "producto": "Correas para BMW/Encory",
      "notas": "Empresa dedicada a la<b> fabricación de correas</b> con una característica que la diferencia de otros proveedores vistos en la feria: no solo disponen de referencias estándar de catálogo, sino que también tienen capacidad para desarrollar correas nuevas según especificaciones concretas. Esto es especialmente interesante si en algún momento necesitamos algo a medida, ya sea por dimensiones especiales, materiales específicos o aplicaciones particulares que no cubren los productos estándar del mercado.\nAdemás de las correas, también <b>disponen de columnas EPS nuevas en su catálogo.</b> Sin embargo, de momento su gama <b>está enfocada principalmente al mercado USA</b>, por lo que las referencias actuales podrían no coincidir directamente con las aplicaciones del parque europeo. Aun así, si tienen capacidad de desarrollo para correas, es probable que también puedan adaptar o desarrollar referencias de columnas EPS para el mercado europeo si hay volumen suficiente que lo justifique.\nDatos del proveedor:\n\nContacto: Kozy\nEmail: nbmbelt-kozy@mstjd.com",
      "oportunidad": "Oportunidad de negocio identificada:\n\nCorreas a medida: La capacidad de fabricar correas según especificaciones nos abre una puerta que pocos proveedores ofrecen. Si en alguna aplicación tenemos problemas para encontrar una correa estándar que encaje perfectamente, o si queremos optimizar el rendimiento de algún producto con una correa específica, este proveedor podría desarrollarla para nosotros. Esto nos da flexibilidad técnica que con otros proveedores no tendríamos.\n\nProveedor alternativo de correas estándar: Además de la capacidad de desarrollo, también pueden suministrar correas estándar. Esto les convierte en otra opción más para diversificar proveedores en este componente y comparar precios con los demás contactos de correas identificados en la feria.\n\nColumnas EPS – Oportunidad a medio plazo: Aunque su catálogo de EPS esté enfocado a USA, merece la pena explorar si tienen referencias que coincidan con vehículos europeos (algunos modelos son globales) o si estarían dispuestos a desarrollar referencias para nuestro mercado. Si la calidad es buena y el precio competitivo, podría ser una fuente interesante de columnas EPS nuevas, un producto con demanda creciente.\n\nPartner de desarrollo: Un proveedor con capacidad de desarrollo técnico puede convertirse en un partner estratégico a largo plazo, no solo como suministrador de producto, sino como colaborador en proyectos de mejora o nuevos desarrollos. Este tipo de relaciones aportan valor más allá del simple aprovisionamiento.",
      "prioridad": 1,
      "seguimiento": {
        "responsable": "Dirección",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "pendiente",
        "email": "oscar@lziarte.com"
      },
      "departamento": "Lizarte",
      "fotos": [],
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_9",
      "empresa": "YAS - Bruce Lee & Bella",
      "producto": "Direcciones (PROYECTO CLAVE)",
      "notas": "He mantenido una reunión importante con Bruce Lee y Bella. El proyecto inicial que teníamos en mente, basado en la creación de un almacén conjunto, no les interesa. Bruce Lee, comentó que es algo nuevo para él y no lo visualiza. Sin embargo, han puesto sobre la mesa una propuesta alternativa que resulta muy interesante desde el punto de vista estratégico y comercial.\nPropuesta del proveedor:\n\nEnvío de gran volumen de material: <b>Nos mandarían un stock importante de producto, tanto referencias ya homologadas como referencias nuevas no homologadas. OJO, REF EUROPEAS \n</b>\n<b>Ampliación del plazo de pago:</b> Ofrecen condiciones de pago extendidas, lo que reduce significativamente la necesidad de inversión inicial y el riesgo financiero por nuestra parte. Eso sí, necesitan saber una estimación de tiempo necesario para vender el producto, importante este punto. \n<b>Lizarte se encarga de la comercialización:</b> Nosotros nos ocuparíamos de vender el producto en Europa, aprovechando nuestra red comercial, reputación y conocimiento del mercado.\n\n<b>Venta bajo marca LIZARTE</b>: Todo el producto se comercializaría con nuestra marca, no con la suya. Esto mantiene nuestra imagen de marca y la confianza del cliente final en Lizarte.\n\n¿Por qué es tan interesante esta propuesta?\nEste modelo de colaboración tiene un valor estratégico enorme por varios motivos:\n\nBajo riesgo financiero: El proveedor asume el riesgo de enviarnos stock y nos da plazo de pago ampliado. Esto significa que Lizarte no tiene que hacer una inversión inicial grande. Básicamente, vendemos primero y pagamos después. El flujo de caja juega a nuestro favor.\n\n<b>Ampliación masiva de catálogo:</b> Podríamos ampliar significativamente el catálogo de direcciones, algo que de otra forma requeriría una inversión enorme en stock y homologaciones. Tener más referencias significa poder atender más demanda y captar clientes que ahora van a la competencia porque no tenemos su referencia.\n\nSolución al problema del casco en mercados lejanos: Este modelo es especialmente interesante para vender en países donde el retorno del casco es un problema logístico (como vimos con el contacto de Sudáfrica). Si vendemos producto nuevo bajo marca Lizarte, no hay casco que gestionar. Abre la puerta a mercados que hasta ahora eran complicados para nosotros.\n\nMarca propia: Al vender con marca LIZARTE, no perdemos identidad ni posicionamiento. El cliente sigue asociando el producto con nosotros, lo que refuerza nuestra presencia en el mercado y nos diferencia de competidores que venden marcas blancas genéricas.\n\nReferencias no homologadas = oportunidad: El hecho de que incluyan referencias no homologadas para el mercado europeo significa que podemos acceder a producto nuevo antes que la competencia. Si homologamos esas referencias, ganamos ventaja competitiva.",
      "oportunidad": "Oportunidad de negocio identificada:\nEsta es una de las oportunidades más importantes detectadas en la feria. Estamos hablando de un proyecto estratégico que podría transformar nuestra posición en el mercado de direcciones:\n\nCrecimiento acelerado: Podemos crecer en catálogo y volumen de ventas sin la inversión proporcional que normalmente requeriría.\n\nEntrada en nuevos mercados: Los países donde el retorno de casco era un freno ahora se convierten en mercados accesibles.\n\nCompetitividad: Más referencias + marca propia + precios competitivos = mayor capacidad de competir con los grandes competidores del mercado.\n\nModelo replicable: Si funciona con direcciones, podría plantearse un modelo similar con otros productos en el futuro. Ej; Defu. \n\nRiesgos a considerar:\n\nDependencia de un único proveedor para un volumen grande de producto.\n\nNecesidad de validar la calidad de las referencias no homologadas antes de comercializarlas.\n\nGestión del stock: aunque el riesgo financiero es menor, hay que ser capaces de mover el producto. Y estimar un plazo de venta, ya que ese será el plazo de pago. Ej, si decimos que seremos capaces de vender el producto en 6 meses, eso significa, que en 6 meses tendremos que realizar el pago y si no hemos vendido todo el material. será un riesgo. ",
      "prioridad": 0,
      "seguimiento": {
        "responsable": "Dirección",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "Informar volumen anual de direcciones vendidas para calcular plazo de pago",
        "fechaSeguimiento": "",
        "acciones": [
          "Analizar la propuesta en detalle internamente. Definir qué volumen de referencias estaríamos dispuestos a asumir en una primera fase. Solicitar listado completo de referencias disponibles (homologadas y no homologadas) con precios. Evaluar la calidad del producto con muestras antes de comprometernos. Negociar condiciones concretas de plazo de pago y posibles devoluciones de producto no vendido. Presentar la propuesta a dirección como proyecto estratégico de ampliación de catálogo de direcciones.",
          "¿Capacidad de devolver algo si nos sobra?"
        ],
        "estado": "pendiente",
        "email": "oscar@lizarte.com"
      },
      "departamento": "Innovación",
      "fotos": [],
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_10",
      "empresa": "7+ (seven plus tools)",
      "producto": "Herramientas ",
      "notas": "Proveedor de<b> pistolas de impacto portátiles</b> – Herramientas de montaje\nEmpresa que ofrece pistolas de impacto portátiles, un <b>tipo de herramienta cada vez más demandada por producción y necesaria para Encory/BMW</b>. Lo más interesante de este producto es que permite trabajar con un <b>par de apriete controlado</b>, algo fundamental para garantizar la calidad del montaje en componentes de automoción donde el apriete incorrecto puede provocar fallos graves.\nEn nuestro proceso de montaje actual, contar con herramientas que aseguren un par de apriete preciso y repetible es clave para mantener la calidad del producto final. Las pistolas de impacto portátiles con control de par eliminan la variabilidad del apriete manual y reducen el riesgo de errores humanos, ya sea por apriete insuficiente (que puede provocar holguras y vibraciones) o por apriete excesivo (que puede dañar roscas o componentes).\n<b>El hecho de que sean portátiles añade versatilidad: </b>pueden utilizarse en diferentes puestos de trabajo sin necesidad de instalaciones fijas, lo que facilita la organización de la producción y permite adaptarse a diferentes necesidades.\n\nContacto; info@sevenplustools.com",
      "oportunidad": "Mejora de calidad en producción: Incorporar pistolas de impacto con par controlado en nuestros procesos de montaje eleva el nivel de calidad y consistencia del producto. Cada tornillo, cada unión, queda apretada exactamente con el par especificado. Esto reduce reclamaciones por fallos de montaje y refuerza la fiabilidad del producto Lizarte.\nReducción de errores y reprocesos: El control de par evita tanto el apriete insuficiente como el excesivo. Menos errores de montaje significa menos tiempo perdido en reprocesos y menos coste por producto defectuoso.\nTrazabilidad y control: Algunas pistolas de impacto modernas permiten registrar los datos de apriete, lo que añade trazabilidad al proceso productivo. Esto puede ser un argumento de calidad frente a clientes exigentes o en auditorías.",
      "prioridad": 0,
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Krum contacta de momento no hay respuesta."
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "departamento": "Lizarte",
      "fotos": [],
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_11",
      "empresa": "Galería OneNote - Tarjetas y Fotos",
      "producto": "Tarjetas de visita, productos, stands",
      "notas": "47 fotos extraídas de la app by KKK. Incluye tarjetas de visita de contactos, fotos de productos, stands visitados y material de referencia..<div><b>Meter las fotos a la IA a ver que me puede ofrecer.</b></div>",
      "oportunidad": "Archivo visual de referencia de la feria",
      "prioridad": 1,
      "fotos": [
        "fotos/onenote_imagen-000.png",
        "fotos/onenote_imagen-001.png",
        "fotos/onenote_imagen-002.png",
        "fotos/onenote_imagen-003.png",
        "fotos/onenote_imagen-004.png",
        "fotos/onenote_imagen-005.png",
        "fotos/onenote_imagen-006.png",
        "fotos/onenote_imagen-007.png",
        "fotos/onenote_imagen-008.png",
        "fotos/onenote_imagen-009.png",
        "fotos/onenote_imagen-010.png",
        "fotos/onenote_imagen-011.png",
        "fotos/onenote_imagen-012.png",
        "fotos/onenote_imagen-013.png",
        "fotos/onenote_imagen-014.png",
        "fotos/onenote_imagen-015.png",
        "fotos/onenote_imagen-016.png",
        "fotos/onenote_imagen-017.png",
        "fotos/onenote_imagen-018.png",
        "fotos/onenote_imagen-019.png",
        "fotos/onenote_imagen-020.png",
        "fotos/onenote_imagen-021.png",
        "fotos/onenote_imagen-022.png",
        "fotos/onenote_imagen-023.png",
        "fotos/onenote_imagen-024.png",
        "fotos/onenote_imagen-025.png",
        "fotos/onenote_imagen-026.png",
        "fotos/onenote_imagen-027.png",
        "fotos/onenote_imagen-028.png",
        "fotos/onenote_imagen-029.png",
        "fotos/onenote_imagen-030.png",
        "fotos/onenote_imagen-031.png",
        "fotos/onenote_imagen-032.png",
        "fotos/onenote_imagen-033.png",
        "fotos/onenote_imagen-034.png",
        "fotos/onenote_imagen-035.png",
        "fotos/onenote_imagen-036.png",
        "fotos/onenote_imagen-037.png",
        "fotos/onenote_imagen-038.png",
        "fotos/onenote_imagen-039.png",
        "fotos/onenote_imagen-040.png",
        "fotos/onenote_imagen-041.png",
        "fotos/onenote_imagen-042.png",
        "fotos/onenote_imagen-043.png",
        "fotos/onenote_imagen-044.png",
        "fotos/onenote_imagen-045.png",
        "fotos/onenote_imagen-046.png"
      ],
      "seguimiento": {
        "responsable": "",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "pendiente",
        "email": ""
      },
      "departamento": "Lizarte",
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_1765891635308",
      "empresa": "TrakMotive ",
      "producto": "Componentes electrónicos Liz On",
      "notas": "<b>Sean Haung; suang@trakmotive.com </b>\n<b>Ingeniero electrónico en TrakMotive con muchos contactos.</b> <b>Me lo presenta Pablo Menéndez, ya que es una persona que conoce muchas empresas que nos pueden proveer de componentes electrónicos directamente, saltándonos intermediarios, como puede ser Altezza o New Vision. </b>",
      "oportunidad": "Proveedores directos de componentes electrónicos. ",
      "departamento": "Lizarte",
      "prioridad": 0,
      "fotos": [],
      "seguimiento": {
        "responsable": "Innovación",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Krum, primera toma de contacto a través de email y poner a Javier Hualde en copia para decir que componentes son los que necesitamos. \nY, luego procedes a contactar con los proveedores para estableces lazos y comprar muestras. "
        ],
        "estado": "pendiente",
        "email": "krum@lizarte.com"
      },
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_1765891979628",
      "empresa": "BEARINGS KAY; TIANTUO BEARING Co., Ltd",
      "producto": "Rodamientos para Bombas y Direcciones ",
      "notas": "<b>Contacto; FuKay ; bearing789@gmail.com</b>\n<div><b>Rodamientos para Bombas y Direcciones </b></div>",
      "oportunidad": "",
      "departamento": "Lizarte",
      "prioridad": 1,
      "fotos": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Solicitar catálogo para ver referencias, modelos y precios "
        ],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "fotos_extra": [],
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_1765892154124",
      "empresa": "FORTUNE Ningbo Fortune Auto Parts Manufacture",
      "producto": "Guantes de trabajo",
      "notas": "Ofrecen guantes naranjas cómo los que utilizamos ahora. <b><font color=\"#d71d1d\">Plantearnos a vender guantes a otras compañías o hacer compra conjunta para mayor descuento. </font></b>",
      "oportunidad": "Ahora del 50% en la compra de los guantes. Ya tenemos primera oferta y el ahorro es del 50%\nPlantearnos a vender guantes a otras compañías o hacer compra conjunta para mayor descuento. ",
      "departamento": "Lizarte",
      "prioridad": 1,
      "fotos": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Solicitar precio "
        ],
        "estado": "proceso",
        "email": "jbaztan@lizarte.com"
      },
      "fotos_extra": [],
      "respuestas": [
        {
          "texto": "Se ha realizado pedido y llega en Febrero. ",
          "formato": {
            "negrita": false,
            "lista": false
          }
        }
      ],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_1765956616629",
      "empresa": "SANTPRO",
      "producto": "Herramientas, puntas de pistolas.",
      "notas": "Contacto;Sabina; sales04@shengtetools.com\n\nEmpresa que tiene todo tipo de<b> accesorios para herramientas: bocas, llaves, vasos, puntas y demás utillaje de uso diario. Este tipo de producto es exactamente lo que utilizamos de forma continua en producción y que tiene un desgaste y consumo elevado.</b> En cualquier entorno productivo como el nuestro, las herramientas de mano y sus accesorios sufren un deterioro constante por el uso intensivo. Bocas que se redondean, llaves que pierden precisión, vasos que se dañan... Son elementos que hay que reponer con frecuencia y que, aunque individualmente no son caros, en conjunto suponen un coste recurrente significativo a lo largo del año.\n\nHasta ahora, este tipo de material probablemente lo compramos a proveedores locales o distribuidores europeos, con los márgenes que eso implica. Encontrar un fabricante o proveedor en origen que ofrezca este tipo de accesorios a precios competitivos y con calidad suficiente para uso industrial puede suponer un ahorro importante en el gasto de consumibles de producción.",
      "oportunidad": "",
      "departamento": "Lizarte",
      "prioridad": 2,
      "fotos": [],
      "fotos_extra": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_1765956833381",
      "empresa": "LTMS ",
      "producto": "",
      "notas": "Contacto; <b>506015814@qq.com, este tipo de email, inspira poca confianza. </b>\n\nEmpresa que tiene todo tipo de <b>accesorios para herramientas: bocas, llaves, vasos, puntas y demás utillaje de uso diario. Este tipo de producto es exactamente lo que utilizamos de forma continua en producción y que tiene un desgaste y consumo elevado </b>.En cualquier entorno productivo como el nuestro, las herramientas de mano y sus accesorios sufren un deterioro constante por el uso intensivo. Bocas que se redondean, llaves que pierden precisión, vasos que se dañan... Son elementos que hay que reponer con frecuencia y que, aunque individualmente no son caros, en conjunto suponen un coste recurrente significativo a lo largo del año.\n\nHasta ahora, este tipo de material probablemente lo compramos a proveedores locales o distribuidores europeos, con los márgenes que eso implica. Encontrar un fabricante o proveedor en origen que ofrezca este tipo de accesorios a precios competitivos y con calidad suficiente para uso industrial puede suponer un ahorro importante en el gasto de consumibles de producción.",
      "oportunidad": "",
      "departamento": "Lizarte",
      "prioridad": 1,
      "fotos": [],
      "fotos_extra": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_1765956951296",
      "empresa": "Ruain Linguang Plastic Manufacture",
      "producto": "Cables, conectores",
      "notas": "Stand pequeño pero con alta variedad de <b>cableado específico que podría ser útil para LizOn</b>. A veces los stands más pequeños esconden proveedores muy especializados con producto de nicho difícil de encontrar en otros sitios.\nEl cableado es un componente esencial en nuestras aplicaciones de mecatrónica. Contar con un proveedor directo especializado podría asegurar disponibilidad y reducir costes frente a los canales de aprovisionamiento actuales.\n\nContacto: linguang_linkai@163.com",
      "oportunidad": "",
      "departamento": "Lizarte",
      "prioridad": 1,
      "fotos": [],
      "fotos_extra": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_1765957135382",
      "empresa": "CAGREN",
      "producto": "",
      "notas": "Stand pequeño pero con alta variedad de <b>cableado específico que podría ser útil para LizOn.</b> A veces los stands más pequeños esconden proveedores muy especializados con producto de nicho difícil de encontrar en otros sitios.\nEl cableado es un componente esencial en nuestras aplicaciones de mecatrónica. Contar con un proveedor directo especializado podría asegurar disponibilidad y reducir costes frente a los canales de aprovisionamiento actuales.\n\nContacto; george@cagren.com",
      "oportunidad": "",
      "departamento": "Lizarte",
      "prioridad": 2,
      "fotos": [],
      "fotos_extra": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_1765959293995",
      "empresa": "YUHUAN YUANHAO MACHINERY Co.,LTD",
      "producto": "Terminales ",
      "notas": "Empresa que ofrece <b>terminales </b>como componente. Al igual que otro proveedor identificado en la feria, la idea es comprar terminales directamente <b>listos para usar y evitar tener que retrabajar los actuales, lo que supondría un ahorro de tiempo y coste de mano de obra en producción.</b>\nTener varias opciones de proveedores de terminales nos permite comparar calidad y precio, además de asegurar suministro alternativo.<div><br></div><div><b>Importante, que Calidad de el OK para evitar problemas. </b>\n\nContacto: yhsuspension@foxmail.com</div>",
      "oportunidad": "",
      "departamento": "Lizarte",
      "prioridad": 2,
      "fotos": [],
      "fotos_extra": [],
      "seguimiento": {
        "responsable": "Compras",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [],
        "estado": "pendiente",
        "email": "jbaztan@lizarte.com"
      },
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_1765959803163",
      "empresa": "SINOMZ",
      "producto": "LizOn ",
      "notas": "<b>VISITA ESTRATÉGICA A FÁBRICA – SINOMZ</b>\nHe realizado una visita completa a las instalaciones de SINOMZ. La visita ha sido muy reveladora y ha aportado información clave tanto sobre la capacidad del proveedor como sobre las posibilidades de colaboración futura. Es importante destacar que con esta empresa nos conocemos desde hace más de 15 años, lo que establece una base de confianza sólida para cualquier proyecto conjunto.\n\nDATOS DE LA EMPRESA:\n\nNombre: SINOMZ\nFundación: 2004 (más de 20 años de trayectoria)\nPlantilla: 350 trabajadores\nSuperficie actual: 40.000 m²\nEquipo técnico: 25 ingenieros de desarrollo\nEquipo de calidad: 26 personas dedicadas a control de calidad\nInstalaciones: Nuevas, se trasladaron hace varios años a la ubicación actual\n\nEstos números hablan de una empresa consolidada y con estructura seria. No estamos ante un pequeño taller, sino ante un fabricante con capacidad industrial real y equipos dedicados tanto a desarrollo como a calidad. El ratio de personal técnico y de calidad respecto al total de trabajadores es muy saludable.\n\nAPACIDAD PRODUCTIVA Y CRECIMIENTO:\nSituación actual:\n\nCapacidad planificada: 1,2 millones de piezas al año entre bombas y direcciones.\n\nEvolución en los últimos 5 años:\n\nPartían de una capacidad de 450.000 bombas al año.\n<b>En 2025 han alcanzado: 800.000 bombas + 400.000 direcciones anuales.</b>\nEn 2019 comenzaron a desarrollar y fabricar direcciones además de bombas.\n\nEste crecimiento demuestra una empresa en expansión constante que ha sabido diversificar su producto (de solo bombas a bombas + direcciones) y casi duplicar su capacidad productiva en cinco años.\nPlanes de expansión – Nueva fábrica:\n\nEstán construyendo una nueva fábrica de 85.000 m² (más del doble de la actual).\nCapacidad objetivo: 2,2 millones de piezas anuales.\nSe trasladarán a la nueva fábrica porque la actual se les queda pequeña.\nLa fábrica actual la reconvertirán para fabricar otros productos.\n\nEsto indica que SINOMZ tiene planes de crecimiento muy ambiciosos y visión a largo plazo. Quieren consolidarse como un jugador de referencia en el mercado global.\n\nIMPRESIONES DE LA VISITA A PRODUCCIÓN:\nHe podido ver tanto la línea de bombas como la de direcciones. La impresión general es muy positiva:\n\nAlto nivel de automatización: Tanto en bombas como en direcciones, los procesos están muy automatizados. Esto garantiza consistencia en la calidad, capacidad de producción elevada y menor dependencia de errores de mano de obra manual.\nCapacidades grandes: Las instalaciones están preparadas para volúmenes industriales serios. Pueden absorber pedidos grandes sin problemas de capacidad.",
      "oportunidad": "INTERÉS MUTUO EN COLABORACIÓN:\nDurante la reunión ha quedado claro que SINOMZ tiene un interés genuino en trabajar con Lizarte:\n\nAjuste de precios: Han manifestado que pueden ajustar los precios dada la relación de confianza que tenemos, ya que nos conocemos desde hace más de 15 años. Esto es un punto de partida excelente para negociar condiciones ventajosas.\n\nPropuesta de almacén en Europa: Les he explicado nuestra idea de montar un almacén en Europa para agilizar el suministro y reducir plazos de entrega. La respuesta ha sido positiva: les parece bien y quieren que lo hablemos en detalle. Esto podría ser un proyecto conjunto muy interesante.\n\nInterés del propietario en EPS: El propietario de SINOMZ ha mostrado gran interés en la posibilidad de montar una empresa en China dedicada a EPS. Le he explicado la diferencia entre producto remanufacturado y producto nuevo para que entienda nuestro modelo de negocio y dónde podría haber sinergias.\n\nDisponibilidad para reunirse en España: El propietario ha ofrecido venir personalmente a España para discutir todos los temas si fuese necesario. Este gesto demuestra un nivel de compromiso e interés muy alto. No es habitual que el dueño de una empresa de este tamaño se ofrezca a desplazarse para cerrar acuerdos.\n\nOPORTUNIDADES DE NEGOCIO IDENTIFICADAS:\nEsta visita ha puesto sobre la mesa múltiples oportunidades estratégicas:\n\nPrecios competitivos por relación histórica: 15 años de relación nos posicionan como cliente preferente. Podemos negociar condiciones que otros compradores nuevos no conseguirían. Aprovechar esta ventaja para mejorar márgenes.\n\nAlmacén conjunto en Europa: Si SINOMZ está dispuesto a participar en un modelo de almacén en Europa, podríamos tener stock cerca del cliente final con plazos de entrega reducidos. Esto nos haría mucho más competitivos frente a proveedores que sirven directamente desde China con semanas de espera.\n\nSINOMZ quiere entrar en el negocio de EPS pero carece del conocimiento técnico especializado en remanufacturado. Nosotros, por el contrario, tenemos años de experiencia y know-how en reman de mecatrónica y sistemas electrónicos, pero montar una operación de este tipo en China requeriría una inversión enorme en instalaciones, maquinaria, personal y gestión local.\nLa propuesta une lo mejor de ambos mundos:\n\nSINOMZ aporta: Instalaciones, capacidad productiva, maquinaria, mano de obra, conocimiento del mercado chino y gestión local. Ya tienen 40.000 m² (pronto 85.000 m²), 350 trabajadores, 25 ingenieros y procesos altamente automatizados.\nLizarte aporta: Conocimiento técnico en remanufacturado de EPS, experiencia en el mercado europeo, red comercial, marca reconocida y know-how acumulado durante años en LizOn.\n\nRespuesta del propietario:\nEl propietario de SINOMZ ha mostrado gran interés en la propuesta. No solo le parece viable, sino que ha manifestado total disposición a reunirse cuando queramos y donde queramos para tratar el tema en profundidad. Esta actitud demuestra que lo ve como una oportunidad real de negocio, no como una idea más que escuchar por cortesía.\nModelo propuesto – Lizarte & SINOMZ:\nLa idea sería constituir una empresa conjunta (joint venture) dedicada específicamente al remanufacturado de EPS, operando desde China pero con el conocimiento y supervisión técnica de Lizarte. El modelo podría contemplar:\n\nProducción de EPS remanufacturado en China con costes competitivos.\nTransferencia de conocimiento técnico de Lizarte a la operación conjunta.\nComercialización del producto en Europa bajo marca Lizarte y/o en Asia bajo marca conjunta.\nReparto de beneficios según participación acordada. ",
      "departamento": "Innovación",
      "prioridad": 0,
      "fotos": [],
      "fotos_extra": [],
      "seguimiento": {
        "responsable": "Dirección",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Evaluar internamente el interés estratégico de Lizarte en este proyecto y el nivel de compromiso que estamos dispuestos a asumir.",
          "Definir qué modelo de colaboración preferimos (joint venture, licencia de know-how, acuerdo de producción, etc.).",
          "Preparar una propuesta inicial con los términos básicos que querríamos negociar.",
          "Organizar una reunión formal con el propietario de SINOMZ, ya sea en España o en China, para discutir el proyecto en profundidad.",
          "Consultar con asesoría legal especializada en operaciones internacionales y joint ventures en China."
        ],
        "estado": "pendiente",
        "email": "oscar@lizarte.com"
      },
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    },
    {
      "id": "add_1766263234248",
      "empresa": "CHEERHO",
      "producto": "Cascos, PtCom",
      "notas": "He visitado las instalaciones de Cheerho y me ha sorprendido la <b>gran cantidad de cascos de LizOn que tienen disponibles.</b> Esto abre una oportunidad interesante de aprovisionamiento para nuestra línea de remanufacturado.\nProyectos identificados:\n\n<b>1. Compra de cascos para LizOn:</b>\nHe hablado directamente con el dueño para valorar la posibilidad de que nos suministre cascos de LizOn. Tener acceso a un stock grande de cascos en China podría solucionar problemas de disponibilidad y reducir costes de aprovisionamiento de materia prima para reman.\n\n<b>2. Bomba 04550803 – Alternativa al retrofitting:</b>\nVenden la bomba referencia 04550803 por 70$. Esta referencia es especialmente relevante porque actualmente tenemos altos porcentajes de garantías con ella y ya hemos agotado las opciones de mejora en nuestro proceso de retrofitting.",
      "oportunidad": "Comprar esta bomba directamente como pieza nueva en lugar de hacer retrofitting podría:\n\nMejorar significativamente la calidad del producto final.\nReducir las garantías y los costes asociados a reclamaciones.\nSimplificar el proceso productivo al eliminar el retrofitting de esta referencia problemática.\n\nA veces la mejor solución no es seguir intentando mejorar un proceso que no da más de sí, sino cambiar de estrategia y optar por producto nuevo cuando el coste lo justifica.",
      "departamento": "Innovación",
      "prioridad": 0,
      "fotos": [],
      "fotos_extra": [],
      "seguimiento": {
        "responsable": "Innovación",
        "contactado": false,
        "respuestaRecibida": false,
        "proximaAccion": "",
        "fechaSeguimiento": "",
        "acciones": [
          "Pedirles el listado de referencias de cascos LizOn que tienen disponibles.",
          "Enviarles las referencias de cascos que nos interesan para ver coincidencias y precios.",
          "Solicitar dos muestras de la bomba 04550803 para validar calidad y confirmar que resuelve los problemas de garantías que tenemos actualmente."
        ],
        "estado": "proceso",
        "email": "krum@lizarte.com"
      },
      "respuestas": [],
      "conclusionFinal": "",
      "finalizado": false
    }
  ],
  "nuevosCoches": [
    {
      "id": "coche_1766140582013",
      "nombre": "ARCFOX",
      "descripcion": "ARCFOX (极狐) fue fundada en 2017 como la marca de vehículos eléctricos premium del grupo estatal BAIC Group. En 2024 vendió 81,000 unidades, un crecimiento del 170% respecto al año anterior, con ingresos estimados de aproximadamente $1,000 millones USD. Desde 2022 mantiene una alianza estratégica con Huawei para sistemas operativos y conducción autónoma. Su portafolio incluye el Alpha S5 (desde $18,000 USD) y el innovador Kaola, un MPV diseñado para familias. La marca se está expandiendo internacionalmente hacia Europa, Medio Oriente y Latinoamérica. Compite directamente con NIO y Xpeng en el segmento de EVs premium de precio medio-alto. Su principal desafío sigue siendo alcanzar rentabilidad en un mercado extremadamente competitivo."
    },
    {
      "id": "coche_1766152842149",
      "nombre": "BEIJING AUTO (GEIJING)",
      "descripcion": "BEIJING Auto pertenece a BAIC Group, fundado en 1958 como el sexto mayor fabricante de automóviles de China. La marca Beijing fue relanzada en 2020, enfocándose en vehículos de combustión, híbridos y eléctricos para el mercado masivo. El grupo BAIC completo vendió 1.71 millones de vehículos en 2024, con ingresos superiores a $66,700 millones USD. Su portafolio incluye los SUV X7 y X55 (desde $14,900 USD) y la submarca Beijing Off-Road con los icónicos BJ40 y BJ60, todoterrenos inspirados en el clásico jeep militar chino. BAIC opera joint ventures con Mercedes-Benz y Hyundai. Es una marca estatal con fuerte respaldo gubernamental del municipio de Beijing."
    },
    {
      "id": "coche_1766152855991",
      "nombre": "TANK",
      "descripcion": "TANK (坦克) fue lanzada como marca independiente en abril de 2021 por Great Wall Motors (GWM), especializada en SUVs todoterreno \"neo-retro\" premium. En 2024 vendió 231,001 unidades (+42% interanual), representando el 19% de las ventas totales de GWM, con ingresos estimados de $10,000-13,000 millones USD. El Tank 300 es el modelo insignia con más de 280,000 unidades vendidas acumuladas. La gama incluye el Tank 500 de 7 plazas y el premium Tank 700 Hi4-T con motor V6 híbrido (hasta $97,000 USD). Tank ha creado una nueva categoría en China: todoterrenos de nueva energía. Compite contra Yangwang (BYD), Dongfeng Mengshi y Land Rover. Su expansión internacional abarca Australia, México, Arabia Saudita y Sudáfrica.\n"
    },
    {
      "id": "coche_1766152857801",
      "nombre": "AION",
      "descripcion": "AION (埃安) fue establecida en julio de 2017 como GAC New Energy, convirtiéndose en marca independiente en noviembre de 2020 bajo GAC Group. En diciembre de 2023 logró alcanzar 1 millón de vehículos producidos en solo 4 años y 8 meses, el tiempo más rápido de cualquier marca EV mundial. En 2024 vendió 412,943 unidades, aunque experimentó una caída del 14% por la falta de modelos híbridos enchufables. Los modelos principales son el Aion S y Aion Y (desde $12,500 USD), que representan el 85% de las ventas. La submarca premium Hyptec incluye el hiperdeportivo SSR de 1,224 hp ($180,000-235,000 USD). Es la tercera marca BEV más grande globalmente después de Tesla y BYD. Tiene capacidad de producción de 800,000 unidades anuales y se expande a Tailandia, Indonesia y México."
    },
    {
      "id": "coche_1766152859377",
      "nombre": "ONVO",
      "descripcion": "ONVO (乐道) fue revelada oficialmente el 15 de mayo de 2024 y pertenece 100% a NIO Inc., diseñada para competir en el segmento de mercado masivo de $27,800-41,700 USD. El primer modelo, el SUV coupé L60, se lanzó en septiembre de 2024 como rival directo del Tesla Model Y. En sus primeros 100 días entregó 20,761 unidades, superando las 10,000 entregas mensuales en diciembre. El L60 destaca por su precio competitivo: desde $20,800 USD con el sistema BaaS de alquiler de batería, compartiendo la infraestructura de intercambio de baterías de NIO. Ofrece autonomía de hasta 730 km y arquitectura de 900V. El segundo modelo, el SUV de 3 filas L90, llegará en julio de 2025. NIO apunta a 100,000 ventas de ONVO en 2025."
    },
    {
      "id": "coche_1766152904233",
      "nombre": "AVATR",
      "descripcion": "AVATR (阿维塔) fue fundada el 10 de julio de 2018 como joint venture entre Changan y NIO, siendo renombrada en agosto de 2021 tras incorporar a CATL como accionista. La estructura actual incluye a Changan (41%), CATL (14%) y otros inversores, con Huawei como socio tecnológico estratégico. En 2024 vendió 73,606 unidades, un crecimiento del 132%, con ingresos de $500-600 millones USD. Los modelos incluyen el SUV AVATR 11 (desde $41,800 USD) y el sedán AVATR 12 (desde $37,500 USD). Utiliza sistema de conducción autónoma Huawei ADS 3.0 con 3 LiDAR y HarmonyOS 4.0. Planea salir a bolsa en Hong Kong en 2026 con objetivos de 400,000 unidades para 2027 y 1.5 millones para 2035.\n"
    },
    {
      "id": "coche_1766152906523",
      "nombre": "AITO",
      "descripcion": "AITO (问界) fue fundada el 2 de diciembre de 2021 como la primera marca bajo el modelo HIMA (Harmony Intelligent Mobility Alliance) de Huawei, en colaboración con Seres Group. En 2024 se convirtió en la marca líder entre las \"nuevas fuerzas\" EV con aproximadamente 386,300 unidades vendidas. Los ingresos de Seres alcanzaron $20,160 millones USD (+305%), logrando su primera rentabilidad con un beneficio neto de $826 millones USD. El portafolio incluye el M5, M7 (desde $31,900 USD) y el insignia AITO M9 (desde $65,250 USD), que domina el segmento premium con 150,000 unidades vendidas. La tecnología Huawei es el diferenciador clave: HarmonyOS para cabina y ADS 3.0 para conducción autónoma. Es la cuarta empresa de VE rentable globalmente, después de Tesla, BYD y Li Auto."
    },
    {
      "id": "coche_1766152908601",
      "nombre": "STELATO",
      "descripcion": "STELATO (享界) — nota: la ortografía correcta es STELATO, no \"STELANO\" — fue registrada en diciembre de 2023 como la tercera marca bajo el ecosistema HIMA de Huawei, en colaboración con BAIC BluePark. El primer modelo, el sedán ejecutivo S9, se lanzó el 6 de agosto de 2024 con entregas desde septiembre. En sus primeros cuatro meses de ventas logró 7,494 unidades, posicionándose como competidor del Mercedes-Benz EQS y BMW Serie 5. El S9 destaca por su coeficiente aerodinámico de 0.193 Cd (el más bajo entre sedanes ejecutivos), Huawei ADS 3.0, 4 sensores LiDAR y autonomía de hasta 816 km. El precio oscila entre $43,000-62,500 USD. La capacidad de producción inicial es de 120,000 unidades anuales, expandible a 300,000."
    }
  ],
  "ahorros": [
    {
      "id": "ahorro_1766141065695",
      "empresa": "YAS",
      "producto": "06701575",
      "precioActual": "42",
      "precioNuevo": "38",
      "unidadesAno": "1000",
      "ahorroTotal": 3411.999999999999,
      "precioActualEUR": 35.826,
      "precioNuevoEUR": 32.414,
      "tasaCambio": 0.853,
      "moneda": "USD"
    },
    {
      "id": "ahorro_1766141135837",
      "empresa": "YAS",
      "producto": "01629000",
      "precioActual": "80",
      "precioNuevo": "75",
      "unidadesAno": "500",
      "ahorroTotal": 2132.499999999997,
      "moneda": "USD",
      "tasaCambio": 0.853,
      "precioActualEUR": 68.24,
      "precioNuevoEUR": 63.975
    },
    {
      "id": "ahorro_1766141168518",
      "empresa": "YAS",
      "producto": "06701405",
      "precioActual": "33",
      "precioNuevo": "29",
      "unidadesAno": "3000",
      "ahorroTotal": 10236.000000000007,
      "moneda": "USD",
      "tasaCambio": 0.853,
      "precioActualEUR": 28.149,
      "precioNuevoEUR": 24.737
    }
  ]
}```

## 4. index.html (codigo completo)

```html<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <title>Seguimiento Automechanika v2.0 - Lizarte</title>
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 15px;
            color: #2d3748;
        }
        
        .header {
            background: white;
            padding: 20px;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            margin-bottom: 20px;
            text-align: center;
        }
        
        .logo {
            width: 50px;
            height: 50px;
            margin: 0 auto 12px;
            background: linear-gradient(135deg, #c026d3 0%, #9333ea 100%);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 25px;
        }
        
        h1 {
            font-size: 20px;
            color: #2d3748;
            margin-bottom: 5px;
        }
        
        .subtitle {
            color: #718096;
            font-size: 13px;
        }
        
        .version-badge {
            display: inline-block;
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
            padding: 4px 10px;
            border-radius: 12px;
            font-size: 11px;
            margin-top: 8px;
            font-weight: 600;
        }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 12px;
            margin-bottom: 20px;
        }
        
        .stat-card {
            background: white;
            padding: 15px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            text-align: center;
        }
        
        .stat-value {
            font-size: 24px;
            font-weight: 700;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .stat-label {
            font-size: 10px;
            color: #718096;
            margin-top: 5px;
            text-transform: uppercase;
        }
        
        .tabs {
            background: white;
            border-radius: 12px;
            padding: 5px;
            display: flex;
            gap: 5px;
            margin-bottom: 20px;
            overflow-x: auto;
        }
        
        .tab {
            flex: 1;
            min-width: 120px;
            padding: 10px;
            border: none;
            background: transparent;
            border-radius: 8px;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            white-space: nowrap;
        }
        
        .tab.active {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }
        
        .filters {
            background: white;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 20px;
        }
        
        .filter-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 12px;
        }
        
        .filter-item label {
            display: block;
            font-size: 11px;
            font-weight: 600;
            color: #4a5568;
            margin-bottom: 5px;
        }
        
        .filter-item input,
        .filter-item select {
            width: 100%;
            padding: 8px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 13px;
        }
        
        .content-section {
            display: none;
        }
        
        .content-section.active {
            display: block;
        }
        
        .items-container {
            display: grid;
            gap: 15px;
        }
        
        .item-card {
            background: white;
            border-radius: 16px;
            overflow: hidden;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            transition: background-color 0.3s ease;
        }
        
        .item-card.finalizado {
            background: #f0fdf4;
            border: 2px solid #86efac;
        }
        
        .item-header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 15px;
            color: white;
        }
        
        .item-company {
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 8px;
        }
        
        .item-meta {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            font-size: 12px;
            opacity: 0.95;
        }
        
        .item-body {
            padding: 15px;
        }
        
        .fotos-section {
            margin-bottom: 15px;
        }
        
        .fotos-section-title {
            font-size: 14px;
            font-weight: 700;
            margin-bottom: 10px;
            color: #2d3748;
        }
        
        .fotos-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
            gap: 8px;
            margin-bottom: 10px;
        }
        
        .foto-item {
            position: relative;
        }
        
        .foto-thumb {
            width: 100%;
            height: 100px;
            object-fit: cover;
            border-radius: 8px;
            cursor: pointer;
        }
        
        .foto-delete {
            position: absolute;
            top: 4px;
            right: 4px;
            background: #ef4444;
            color: white;
            border: none;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            cursor: pointer;
            font-size: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .add-foto-btn {
            background: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%);
            color: white;
            padding: 8px 12px;
            border: none;
            border-radius: 8px;
            font-size: 12px;
            cursor: pointer;
            margin-top: 8px;
        }
        
        .seguimiento-box {
            background: #f7fafc;
            padding: 15px;
            border-radius: 12px;
            margin-top: 15px;
        }
        
        .seguimiento-title {
            font-size: 14px;
            font-weight: 700;
            margin-bottom: 12px;
            color: #2d3748;
        }
        
        .form-group {
            margin-bottom: 10px;
        }
        
        .form-group label {
            display: block;
            font-size: 11px;
            font-weight: 600;
            color: #64748b;
            margin-bottom: 4px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 6px 10px;
            border: 1.5px solid #e2e8f0;
            border-radius: 6px;
            font-size: 13px;
            font-family: inherit;
            transition: all 0.2s;
        }
        
        .form-group input:focus,
        .form-group select:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #a855f7;
            box-shadow: 0 0 0 3px rgba(168, 85, 247, 0.1);
        }
        
        .form-group textarea {
            min-height: 40px;
            resize: vertical;
            overflow-y: auto;
            max-height: 400px;
        }
        
        .form-row {
            display: grid;
            grid-template-columns: 1fr auto;
            gap: 8px;
            align-items: end;
        }
        
        .btn-notify {
            background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
            color: white;
            padding: 8px 16px;
            border: none;
            border-radius: 8px;
            font-size: 12px;
            cursor: pointer;
            white-space: nowrap;
        }
        
        .estado-selector {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 8px;
            margin-bottom: 12px;
        }
        
        .estado-option {
            position: relative;
        }
        
        .estado-option input[type="radio"] {
            position: absolute;
            opacity: 0;
        }
        
        .estado-option label {
            display: block;
            padding: 10px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 12px;
            font-weight: 600;
        }
        
        .estado-option input:checked + label {
            border-color: #667eea;
            background: #f0f4ff;
            color: #667eea;
        }
        
        .estado-pendiente label { color: #6b7280; }
        .estado-contactado label { color: #f59e0b; }
        .estado-proceso label { color: #3b82f6; }
        .estado-finalizado label { color: #10b981; }
        
        .estado-pendiente input:checked + label { border-color: #6b7280; background: #f3f4f6; color: #6b7280; }
        .estado-contactado input:checked + label { border-color: #f59e0b; background: #fffbeb; color: #f59e0b; }
        .estado-proceso input:checked + label { border-color: #3b82f6; background: #eff6ff; color: #3b82f6; }
        .estado-finalizado input:checked + label { border-color: #10b981; background: #f0fdf4; color: #10b981; }
        
        .acciones-list {
            margin-bottom: 12px;
        }
        
        .accion-item {
            display: grid;
            grid-template-columns: 1fr auto;
            gap: 8px;
            margin-bottom: 8px;
            align-items: start;
        }
        
        .accion-item textarea {
            min-height: 40px;
        }
        
        .btn-delete-accion {
            background: #ef4444;
            color: white;
            border: none;
            border-radius: 6px;
            padding: 8px 12px;
            cursor: pointer;
            font-size: 12px;
            margin-top: 5px;
        }
        
        .btn-add-accion {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
            padding: 8px 12px;
            border: none;
            border-radius: 8px;
            font-size: 12px;
            cursor: pointer;
            width: 100%;
        }
        
        .respuesta-item {
            display: flex;
            flex-direction: column;
            gap: 8px;
            margin-bottom: 12px;
            padding: 12px;
            background: #f9fafb;
            border-radius: 8px;
            border: 1px solid #e5e7eb;
        }
        
        .respuesta-item textarea {
            min-height: 60px;
            resize: vertical;
            font-family: inherit;
            padding: 10px;
            border: 1px solid #d1d5db;
            border-radius: 6px;
            font-size: 13px;
            line-height: 1.5;
        }
        
        .respuesta-controls {
            display: flex;
            gap: 8px;
            align-items: center;
            flex-wrap: wrap;
        }
        
        .btn-formato {
            background: #6366f1;
            color: white;
            border: none;
            border-radius: 6px;
            padding: 6px 12px;
            font-size: 11px;
            cursor: pointer;
            font-weight: 600;
        }
        
        .btn-formato:hover {
            background: #4f46e5;
        }
        
        .btn-formato.active {
            background: #10b981;
        }
        
        .notas-editor {
            outline: none;
        }
        
        .notas-editor:empty:before {
            content: attr(placeholder);
            color: #9ca3af;
            pointer-events: none;
        }
        
        .notas-editor:focus {
            border-color: #6366f1 !important;
            box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
        }
        
        .btn-delete-respuesta {
            background: #ef4444;
            color: white;
            border: none;
            border-radius: 6px;
            padding: 6px 12px;
            cursor: pointer;
            font-size: 12px;
            margin-left: auto;
        }
        
        .btn-add-respuesta {
            background: linear-gradient(135deg, #6366f1 0%, #4f46e5 100%);
            color: white;
            padding: 8px 12px;
            border: none;
            border-radius: 8px;
            font-size: 12px;
            cursor: pointer;
            width: 100%;
            margin-top: 8px;
        }
        
        .conclusion-final-section {
            margin-top: 20px;
            padding: 15px;
            background: #fef3c7;
            border-radius: 8px;
            border: 2px solid #fbbf24;
        }
        
        .conclusion-final-section h3 {
            font-size: 14px;
            font-weight: 700;
            color: #92400e;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .conclusion-final-section textarea {
            width: 100%;
            min-height: 100px;
            resize: vertical;
            font-family: inherit;
            padding: 12px;
            border: 1px solid #fbbf24;
            border-radius: 6px;
            font-size: 13px;
            line-height: 1.5;
            margin-bottom: 10px;
        }
        
        .conclusion-controls {
            display: flex;
            gap: 8px;
            align-items: center;
            flex-wrap: wrap;
        }
        
        .btn-finalizado {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
            border: none;
            border-radius: 8px;
            padding: 10px 20px;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        
        .btn-finalizado:hover {
            background: linear-gradient(135deg, #059669 0%, #047857 100%);
        }
        
        .btn-finalizado.finalizado {
            background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
        }
        
        .btn-finalizado.finalizado:hover {
            background: linear-gradient(135deg, #dc2626 0%, #b91c1c 100%);
        }
        
        .priority-badge {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 6px;
            font-size: 10px;
            font-weight: 600;
        }
        
        /* Prioridad 0: MUY IMPORTANTE - Rosa magenta */
        .priority-0 {
            background: #fce7f3;
            color: #be185d;
        }
        
        /* Prioridad 1: ALTA - Verde */
        .priority-1 {
            background: #dcfce7;
            color: #166534;
        }
        
        /* Prioridad 2: MEDIA - Amarillo */
        .priority-2 {
            background: #fef3c7;
            color: #92400e;
        }
        
        /* Prioridad 3: BAJA - Naranja */
        .priority-3 {
            background: #ffedd5;
            color: #c2410c;
        }
        
        /* Estilos antiguos por compatibilidad */
        .priority-critica {
            background: #fce7f3;
            color: #be185d;
        }
        
        .priority-alta {
            background: #dcfce7;
            color: #166534;
        }
        
        .priority-media {
            background: #fef3c7;
            color: #92400e;
        }
        
        .priority-baja {
            background: #ffedd5;
            color: #c2410c;
        }
        
        .depto-badge {
            display: inline-block;
            padding: 4px 10px;
            border-radius: 6px;
            font-size: 11px;
            font-weight: 600;
            margin-left: 8px;
        }
        
        .depto-innovacion {
            background: linear-gradient(135deg, #ec4899 0%, #db2777 100%);
            color: white;
            box-shadow: 0 2px 8px rgba(236, 72, 153, 0.3);
        }
        
        .depto-lizarte {
            background: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%);
            color: white;
        }
        
        .config-section {
            background: white;
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 15px;
        }
        
        .config-title {
            font-size: 16px;
            font-weight: 700;
            margin-bottom: 15px;
            color: #2d3748;
        }
        
        .config-group {
            margin-bottom: 20px;
        }
        
        .config-group label {
            display: block;
            font-size: 13px;
            font-weight: 600;
            color: #4a5568;
            margin-bottom: 8px;
        }
        
        .config-group input,
        .config-group textarea {
            width: 100%;
            padding: 10px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 14px;
            font-family: inherit;
        }
        
        .config-group textarea {
            min-height: 100px;
            resize: vertical;
        }
        
        .btn-save-config {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
        }
        
        .btn-export {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
            padding: 15px;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            margin-top: 20px;
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.9);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }
        
        .modal.show {
            display: flex;
        }
        
        /* Botón flotante de exportación */
        .btn-float-export {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
            border: none;
            border-radius: 50px;
            padding: 12px 24px;
            font-size: 16px;
            font-weight: 700;
            cursor: pointer;
            box-shadow: 0 4px 20px rgba(16, 185, 129, 0.4);
            z-index: 999;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s;
        }
        
        .btn-float-export:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 30px rgba(16, 185, 129, 0.6);
            background: linear-gradient(135deg, #059669 0%, #047857 100%);
        }
        
        .btn-float-export:active {
            transform: translateY(0);
        }
        
        .modal-content {
            max-width: 90%;
            max-height: 90%;
        }
        
        .modal-close {
            position: absolute;
            top: 20px;
            right: 20px;
            color: white;
            font-size: 35px;
            cursor: pointer;
            background: rgba(0,0,0,0.5);
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .save-indicator {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: #10b981;
            color: white;
            padding: 12px 20px;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 600;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
            opacity: 0;
            transition: opacity 0.3s;
            z-index: 900;
        }
        
        .save-indicator.show {
            opacity: 1;
        }
        
        @media (max-width: 768px) {
            .stats {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .filter-grid {
                grid-template-columns: 1fr;
            }
            
            .fotos-grid {
                grid-template-columns: repeat(3, 1fr);
            }
            
            .estado-selector {
                grid-template-columns: 1fr;
            }
        }
        
        /* ========== SPLASH SCREEN STYLES ========== */
        
        #splashScreen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #0f0f1e 0%, #1a1a2e 50%, #16213e 100%);
            z-index: 10000;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            animation: splashFadeIn 0.5s ease-out;
        }
        
        #splashScreen.fade-out {
            animation: splashFadeOut 1s ease-out forwards;
        }
        
        .splash-bg-map {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 120%;
            height: 120%;
            opacity: 0.15;
            filter: blur(1px);
        }
        
        .splash-particles {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
        }
        
        .particle {
            position: absolute;
            width: 3px;
            height: 3px;
            background: white;
            border-radius: 50%;
            animation: particleFloat 8s infinite;
            opacity: 0;
        }
        
        .splash-content {
            position: relative;
            z-index: 2;
            text-align: center;
            color: white;
            max-width: 800px;
            padding: 10px;
            max-height: 100vh;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
        
        .splash-route {
            margin-bottom: 15px;
            opacity: 0;
            animation: fadeInUp 1s ease-out 0.5s forwards;
        }
        
        .route-point {
            font-size: 12px;
            font-weight: 600;
            margin: 4px 0;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
        }
        
        .route-line {
            width: 2px;
            height: 30px;
            background: linear-gradient(to bottom, #3b82f6, #8b5cf6);
            margin: 3px auto;
            position: relative;
            overflow: hidden;
        }
        
        .route-line::after {
            content: '';
            position: absolute;
            top: -100%;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(to bottom, transparent, white, transparent);
            animation: routeFlow 2s ease-out 0.8s forwards;
        }
        
        .plane-icon {
            font-size: 24px;
            position: absolute;
            top: -15px;
            left: 50%;
            transform: translateX(-50%) rotate(180deg);
            animation: planeMove 2s ease-out 0.8s forwards;
        }
        
        .splash-stats {
            margin: 12px 0;
            opacity: 0;
            animation: fadeInScale 0.8s ease-out 3s forwards;
            width: 100%;
            max-width: 100%;
            display: flex;
            flex-direction: column;
            align-items: stretch;
        }
        
        .stat-item {
            margin: 6px 0;
            padding: 14px 18px;
            background: rgba(59, 130, 246, 0.1);
            border-radius: 12px;
            border: 2px solid rgba(59, 130, 246, 0.3);
            transition: all 0.3s;
            width: 100%;
            box-sizing: border-box;
        }
        
        .stat-item:hover {
            border-color: rgba(59, 130, 246, 0.6);
            transform: scale(1.02);
        }
        
        .stat-number {
            font-size: 36px;
            font-weight: 800;
            background: linear-gradient(135deg, #3b82f6, #8b5cf6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            display: inline-block;
            text-shadow: 0 0 30px rgba(59, 130, 246, 0.5);
            margin-right: 12px;
        }
        
        .stat-number.glow {
            animation: numberGlow 0.5s ease-out;
        }
        
        .stat-label {
            font-size: 11px;
            color: #cbd5e1;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .splash-message {
            margin: 10px 0;
            opacity: 0;
            animation: fadeInUp 1s ease-out 6s forwards;
        }
        
        .splash-title {
            font-size: 24px;
            font-weight: 800;
            margin-bottom: 5px;
            background: linear-gradient(135deg, #60a5fa, #ec4899);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 0 40px rgba(96, 165, 250, 0.3);
        }
        
        .splash-subtitle {
            font-size: 14px;
            color: #cbd5e1;
            margin-bottom: 3px;
            font-weight: 600;
        }
        
        .splash-date {
            font-size: 12px;
            color: #94a3b8;
            margin-bottom: 8px;
        }
        
        .splash-divider {
            width: 200px;
            height: 1px;
            background: linear-gradient(to right, transparent, #3b82f6, transparent);
            margin: 5px auto;
        }
        
        .splash-credit {
            font-size: 10px;
            color: #64748b;
            margin-top: 5px;
        }
        
        .splash-button {
            opacity: 0;
            animation: fadeInScale 0.8s ease-out 9s forwards;
            margin-top: 8px;
        }
        
        .btn-access {
            background: linear-gradient(135deg, #3b82f6 0%, #8b5cf6 100%);
            color: white;
            border: none;
            padding: 12px 35px;
            font-size: 14px;
            font-weight: 700;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 10px 40px rgba(59, 130, 246, 0.4);
            transition: all 0.3s;
            text-transform: uppercase;
            letter-spacing: 1px;
            position: relative;
            overflow: hidden;
        }
        
        .btn-access::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            transform: translate(-50%, -50%);
            transition: width 0.6s, height 0.6s;
        }
        
        .btn-access:hover::before {
            width: 300px;
            height: 300px;
        }
        
        .btn-access:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 60px rgba(59, 130, 246, 0.6);
        }
        
        .btn-access:active {
            transform: scale(0.98);
        }
        
        .splash-close {
            position: absolute;
            top: 30px;
            right: 30px;
            width: 50px;
            height: 50px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            color: white;
            font-size: 24px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s;
            z-index: 10;
        }
        
        .splash-close:hover {
            background: rgba(255, 255, 255, 0.2);
            border-color: rgba(255, 255, 255, 0.5);
            transform: rotate(90deg);
        }
        
        /* ========== ANIMATIONS ========== */
        
        @keyframes splashFadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
        
        @keyframes splashFadeOut {
            to {
                opacity: 0;
                visibility: hidden;
            }
        }
        
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        @keyframes fadeInScale {
            from {
                opacity: 0;
                transform: scale(0.8);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }
        
        @keyframes routeFlow {
            to {
                top: 100%;
            }
        }
        
        @keyframes planeMove {
            to {
                top: 100%;
            }
        }
        
        @keyframes particleFloat {
            0% {
                opacity: 0;
                transform: translateY(100vh) translateX(0);
            }
            10% {
                opacity: 0.6;
            }
            90% {
                opacity: 0.6;
            }
            100% {
                opacity: 0;
                transform: translateY(-100px) translateX(50px);
            }
        }
        
        @keyframes numberGlow {
            0%, 100% {
                text-shadow: 0 0 30px rgba(59, 130, 246, 0.5);
            }
            50% {
                text-shadow: 0 0 60px rgba(59, 130, 246, 1), 0 0 90px rgba(139, 92, 246, 0.8);
            }
        }
        
        @keyframes pulse {
            0%, 100% {
                transform: scale(1);
                opacity: 1;
            }
            50% {
                transform: scale(1.1);
                opacity: 0.8;
            }
        }
    </style>
</head>
<body>
    <!-- ========== SPLASH SCREEN ========== -->
    <div id="splashScreen" style="display: none;">
        <!-- Botón cerrar -->
        <div class="splash-close" onclick="closeSplash()">✕</div>
        
        <!-- Mapa de fondo -->
        <div class="splash-bg-map">
            <svg viewBox="0 0 800 600" xmlns="http://www.w3.org/2000/svg">
                <!-- Mapa simplificado de China con líneas -->
                <path d="M 400 100 L 600 150 L 650 300 L 600 450 L 400 500 L 200 450 L 150 300 L 200 150 Z" 
                      fill="none" 
                      stroke="url(#mapGradient)" 
                      stroke-width="2" 
                      opacity="0.6"/>
                <!-- Cuadrícula -->
                <line x1="0" y1="150" x2="800" y2="150" stroke="rgba(59, 130, 246, 0.2)" stroke-width="1"/>
                <line x1="0" y1="300" x2="800" y2="300" stroke="rgba(59, 130, 246, 0.2)" stroke-width="1"/>
                <line x1="0" y1="450" x2="800" y2="450" stroke="rgba(59, 130, 246, 0.2)" stroke-width="1"/>
                <line x1="200" y1="0" x2="200" y2="600" stroke="rgba(59, 130, 246, 0.2)" stroke-width="1"/>
                <line x1="400" y1="0" x2="400" y2="600" stroke="rgba(59, 130, 246, 0.2)" stroke-width="1"/>
                <line x1="600" y1="0" x2="600" y2="600" stroke="rgba(59, 130, 246, 0.2)" stroke-width="1"/>
                <!-- Definiciones de gradientes -->
                <defs>
                    <linearGradient id="mapGradient" x1="0%" y1="0%" x2="100%" y2="100%">
                        <stop offset="0%" style="stop-color:#3b82f6;stop-opacity:1" />
                        <stop offset="50%" style="stop-color:#8b5cf6;stop-opacity:1" />
                        <stop offset="100%" style="stop-color:#ec4899;stop-opacity:1" />
                    </linearGradient>
                </defs>
            </svg>
        </div>
        
        <!-- Partículas -->
        <div class="splash-particles" id="particlesContainer"></div>
        
        <!-- Contenido principal -->
        <div class="splash-content">
            <!-- FASE 1: Ruta animada (0-3 seg) -->
            <div class="splash-route" id="splashRoute">
                <div class="route-point">📍 PAMPLONA, ESPAÑA</div>
                <div class="route-line" style="position: relative;">
                    <div class="plane-icon">✈️</div>
                </div>
                <div class="route-point">📍 SHANGHAI, CHINA</div>
            </div>
            
            <!-- FASE 2: Estadísticas (3-6 seg) -->
            <div class="splash-stats" id="splashStats" style="width: 100%; max-width: 100%;">
                <div class="stat-item">
                    <span class="stat-number" id="stat1">0</span>
                    <span class="stat-label">🏢 Empresas Priorizadas Contactadas</span>
                </div>
                <div class="stat-item">
                    <span class="stat-number" id="stat2">0</span>
                    <span class="stat-label">🤝 Reuniones Estratégicas</span>
                </div>
                <div class="stat-item">
                    <span class="stat-number" id="stat3">0</span>
                    <span class="stat-label">📷 Registros Visuales</span>
                </div>
                <div class="stat-item">
                    <span class="stat-number" id="stat4">0</span>
                    <span class="stat-label">⭐ Oportunidades Innovación</span>
                </div>
                <div class="stat-item" style="background: rgba(16, 185, 129, 0.15); border: 2px solid rgba(16, 185, 129, 0.3); margin: 6px 0; padding: 14px 18px; width: 100%; box-sizing: border-box;">
                    <span class="stat-number" id="stat5" style="color: #10b981 !important; text-shadow: 0 0 20px rgba(16, 185, 129, 0.5); font-size: 36px; -webkit-text-fill-color: #10b981 !important; background: none !important;">0,00 €</span>
                    <span class="stat-label" style="color: #10b981; font-size: 11px; font-weight: 600;">💰 Ahorro Conseguido Ya</span>
                </div>
            </div>
            
            <!-- FASE 3: Mensaje (6-9 seg) -->
            <div class="splash-message" id="splashMessage">
                <div class="splash-title">MISIÓN COMPLETADA</div>
                <div class="splash-title" style="font-size: 20px; margin-top: 3px;">KRUM KOVACHEV</div>
                <div class="splash-subtitle">AUTOMECHANIKA SHANGHAI 2025</div>
                <div class="splash-date">19 Nov - 6 Dic</div>
                <div class="splash-divider"></div>
                <div class="splash-credit">Lizarte • Sistema de Gestión</div>
            </div>
            
            <!-- FASE 4: Botón (9-12 seg) -->
            <div class="splash-button">
                <button class="btn-access" onclick="closeSplash()">
                    <span style="position: relative; z-index: 1;">🚀 ACCEDER AL SISTEMA</span>
                </button>
                <div class="splash-credit" style="margin-top: 8px; font-size: 10px;">V12 by Krum Kovachev</div>
            </div>
        </div>
    </div>
    
    <!-- Botón flotante de exportación -->
    <button class="btn-float-export" onclick="exportarDatosActualizados(event)" title="Exportar todos los datos actualizados">
        📤 EXPORTAR
    </button>
    
    <!-- Modal para seleccionar dónde añadir empresa -->
    <div id="addEmpresaModal" style="display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 10000; justify-content: center; align-items: center;">
        <div style="background: white; border-radius: 16px; padding: 30px; width: 90%; max-width: 400px; box-shadow: 0 10px 40px rgba(0,0,0,0.3);">
            <h2 style="margin: 0 0 20px 0; color: #1e293b; font-size: 20px;">¿Dónde añadir la empresa?</h2>
            <div style="display: grid; gap: 12px;">
                <button onclick="addNewReunion();" style="background: linear-gradient(135deg, #a855f7 0%, #9333ea 100%); color: white; border: none; padding: 16px; border-radius: 10px; font-weight: 600; cursor: pointer; font-size: 15px; box-shadow: 0 2px 8px rgba(168, 85, 247, 0.3);">
                    🤝 Reuniones
                </button>
                <button onclick="addNewAdicional();" style="background: linear-gradient(135deg, #10b981 0%, #059669 100%); color: white; border: none; padding: 16px; border-radius: 10px; font-weight: 600; cursor: pointer; font-size: 15px; box-shadow: 0 2px 8px rgba(16, 185, 129, 0.3);">
                    📋 Info Adicional
                </button>
                <button onclick="hideAddEmpresaModal();" style="background: #e5e7eb; color: #64748b; border: none; padding: 16px; border-radius: 10px; font-weight: 600; cursor: pointer; font-size: 15px;">
                    Cancelar
                </button>
            </div>
        </div>
    </div>
    
    <div class="header">
        <div class="logo">🚗</div>
        <h1>Seguimiento Automechanika Shanghai 2025</h1>
        <div class="subtitle">Lizarte - Sistema de Gestión de Contactos</div>
        <div class="version-badge">V12 by Krum Kovachev</div>
    </div>
    
    <div class="stats">
        <div class="stat-card">
            <div class="stat-value" id="statTotal">0</div>
            <div class="stat-label">Total</div>
        </div>
        <div class="stat-card">
            <div class="stat-value" id="statPendientes">0</div>
            <div class="stat-label">Pendientes</div>
        </div>
        <div class="stat-card">
            <div class="stat-value" id="statContactados">0</div>
            <div class="stat-label">Contactados</div>
        </div>
        <div class="stat-card">
            <div class="stat-value" id="statProceso">0</div>
            <div class="stat-label">En Proceso</div>
        </div>
        <div class="stat-card">
            <div class="stat-value" id="statFinalizados">0</div>
            <div class="stat-label">Finalizados</div>
        </div>
    </div>
    
    <!-- Botón único para añadir empresa -->
    <div style="text-align: right; margin: 15px 0;">
        <button onclick="showAddEmpresaModal()" style="background: linear-gradient(135deg, #a855f7 0%, #9333ea 100%); color: white; border: none; padding: 12px 24px; border-radius: 8px; font-weight: 600; cursor: pointer; box-shadow: 0 2px 8px rgba(168, 85, 247, 0.3); font-size: 14px;">
            ➕ Añadir Nueva Empresa
        </button>
    </div>
    
    <div class="tabs">
        <button class="tab active" onclick="switchTab('guia')">📖 Guía</button>
        <button class="tab" onclick="switchTab('reuniones')">🤝 Reuniones (25)</button>
        <button class="tab" onclick="switchTab('adicional')">📋 Info Adicional (11)</button>
        <button class="tab" onclick="switchTab('nuevosCoches')">🚗 Nuevos Coches (0)</button>
        <button class="tab" onclick="switchTab('ahorros')">💰 Ahorros Conseguidos (0)</button>
        <button class="tab" onclick="switchTab('config')">⚙️ Configuración</button>
    </div>
    
    <div class="filters">
        <div class="filter-grid">
            <div class="filter-item">
                <label>🔍 Buscar</label>
                <input type="text" id="searchInput" placeholder="Empresa..." oninput="applyFilters()">
            </div>
            <div class="filter-item">
                <label>🏢 Departamento</label>
                <select id="filterDepartamento" onchange="applyFilters()">
                    <option value="">Todos</option>
                    <option value="Lizarte">🔵 Lizarte</option>
                    <option value="Innovación">⭐ Innovación</option>
                </select>
            </div>
            <div class="filter-item">
                <label>👤 Responsable</label>
                <select id="filterResponsable" onchange="applyFilters()">
                    <option value="">Todos</option>
                </select>
            </div>
            <div class="filter-item">
                <label>📊 Estado</label>
                <select id="filterEstado" onchange="applyFilters()">
                    <option value="">Todos</option>
                    <option value="pendiente">Pendiente</option>
                    <option value="contactado">Contactado</option>
                    <option value="proceso">En Proceso</option>
                    <option value="finalizado">Finalizado</option>
                </select>
            </div>
            <div class="filter-item">
                <label>⭐ Prioridad</label>
                <select id="filterPrioridad" onchange="applyFilters()">
                    <option value="">Todas</option>
                    <option value="0">🔴 0 - Muy Importante</option>
                    <option value="1">🟢 1 - Alta</option>
                    <option value="2">🟡 2 - Media</option>
                    <option value="3">🟠 3 - Baja</option>
                </select>
            </div>
        </div>
    </div>
    
    <div id="guiaSection" class="content-section active">
        <div class="config-section" style="max-width: 900px; margin: 0 auto; padding: 20px;">
            <div class="config-title" style="text-align: center; margin-bottom: 30px;">📘 Guía de Uso - Sistema de Seguimiento Automechanika Shanghai 2025</div>
            
            <div style="background: white; border-radius: 12px; padding: 30px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); line-height: 1.8; color: #2d3748; max-height: 80vh; overflow-y: auto;">
                <div style="margin-bottom: 30px;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">🎯 Introducción</h2>
                    <p>Esta aplicación web ha sido diseñada para gestionar y hacer seguimiento de todos los contactos y reuniones realizadas durante la feria <strong>Automechanika Shanghai 2025</strong> (19 Nov - 6 Dic). Permite organizar la información de empresas, reuniones programadas, oportunidades de negocio y mantener un control completo del estado de seguimiento de cada contacto.</p>
                </div>

                <div style="margin-bottom: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">🚀 Pantalla Inicial (Splash Screen)</h2>
                    <p>Al abrir la aplicación, verás una pantalla de bienvenida que muestra:</p>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li><strong>🏢 Empresas Priorizadas Contactadas</strong>: Total de empresas registradas en el sistema</li>
                        <li><strong>🤝 Reuniones Estratégicas</strong>: Número de reuniones programadas</li>
                        <li><strong>📷 Registros Visuales</strong>: Total de fotos subidas</li>
                        <li><strong>⭐ Oportunidades Innovación</strong>: Empresas asignadas al departamento de Innovación</li>
                    </ul>
                    <p style="margin-top: 10px;"><strong>Nota</strong>: Esta pantalla se muestra automáticamente al cargar la aplicación. Haz clic en "🚀 ACCEDER AL SISTEMA" para continuar.</p>
                </div>

                <div style="margin-bottom: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">📊 Dashboard Principal</h2>
                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">Tarjetas de Estadísticas</h3>
                    <p>En la parte superior de la pantalla principal encontrarás 5 tarjetas con estadísticas en tiempo real:</p>
                    <ol style="margin-left: 20px; margin-top: 10px;">
                        <li><strong>Total</strong>: Número total de empresas (reuniones + información adicional)</li>
                        <li><strong>Pendientes</strong>: Empresas que aún no han sido contactadas</li>
                        <li><strong>Contactados</strong>: Empresas con las que ya se ha establecido contacto</li>
                        <li><strong>En Proceso</strong>: Empresas con negociaciones o seguimiento activo</li>
                        <li><strong>Finalizados</strong>: Empresas con seguimiento completado</li>
                    </ol>
                    <p style="margin-top: 10px;"><strong>💡 Importante</strong>: Estos números se actualizan automáticamente cuando añades, modificas o cambias el estado de las empresas.</p>
                </div>

                <div style="margin-bottom: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">📑 Pestañas Principales</h2>
                    <p>La aplicación está organizada en seis pestañas:</p>
                    
                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">🤝 Reuniones</h3>
                    <p>Contiene todas las <strong>reuniones programadas</strong> durante la feria. Cada reunión incluye: nombre de empresa, persona de contacto, producto/servicio, hora y stand, comentarios, fotos y sistema de seguimiento completo.</p>
                    <p style="margin-top: 10px;"><strong>Contador</strong>: El número entre paréntesis <code>(X)</code> muestra cuántas reuniones hay registradas.</p>

                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">📋 Info Adicional</h3>
                    <p>Contiene <strong>empresas de interés</strong> que no tienen reunión programada pero son relevantes para el seguimiento. Incluye: nombre de empresa, producto/servicio, notas, oportunidad de negocio, fotos y sistema de seguimiento completo.</p>
                    <p style="margin-top: 10px;"><strong>Contador</strong>: El número entre paréntesis <code>(X)</code> muestra cuántas empresas adicionales hay registradas.</p>

                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">🚗 Nuevos Coches</h3>
                    <p>Registro de <strong>marcas de coches nuevos</strong> observados en China durante la estancia. Son vehículos vistos por la calle, no necesariamente en la feria. Esta pestaña documenta marcas que hace dos años no se habían visto y que este año se están viendo con <strong>alta frecuencia</strong>. Para cada coche se puede registrar el nombre y una descripción detallada.</p>
                    <p style="margin-top: 10px;"><strong>Contador</strong>: El número entre paréntesis <code>(X)</code> muestra cuántos coches nuevos hay registrados.</p>

                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">💰 Ahorros Conseguidos</h3>
                    <p>Registro de todos los <strong>ahorros económicos</strong> conseguidos durante la feria. Incluye tanto ahorros directos conseguidos en la feria como ahorros con productos que se terminarán comprando. Para cada ahorro se registra: empresa, producto, precio actual, precio nuevo, unidades por año y el ahorro total calculado automáticamente.</p>
                    <p style="margin-top: 10px;"><strong>Contador</strong>: El número entre paréntesis <code>(X)</code> muestra cuántos ahorros hay registrados. Además, se muestra un resumen destacado con el <strong>total de ahorros conseguidos</strong> en la parte superior de la pestaña.</p>

                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">📖 Guía</h3>
                    <p>Esta pestaña que estás viendo ahora. Contiene toda la documentación de uso de la aplicación.</p>

                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">⚙️ Configuración</h3>
                    <p>Permite personalizar el título, subtítulo, miembros del equipo y notas generales sobre la feria.</p>
                </div>

                <div style="margin-bottom: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">🏷️ Sistema de Clasificación</h2>
                    
                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">Departamentos</h3>
                    <p>Cada empresa puede estar asignada a uno de dos departamentos:</p>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li><strong>🔵 Lizarte</strong>: Empresas relacionadas con el negocio principal de Lizarte</li>
                        <li><strong>⭐ Innovación</strong>: Empresas relacionadas con proyectos de innovación y nuevas oportunidades</li>
                    </ul>

                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">Prioridades</h3>
                    <p>Cada empresa tiene un nivel de prioridad que puedes ajustar:</p>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li><strong>🔴 0 - Muy Importante</strong>: Máxima prioridad, requiere atención inmediata</li>
                        <li><strong>🟢 1 - Alta</strong>: Alta prioridad, seguimiento prioritario</li>
                        <li><strong>🟡 2 - Media</strong>: Prioridad media, seguimiento normal</li>
                        <li><strong>🟠 3 - Baja</strong>: Baja prioridad, seguimiento ocasional</li>
                    </ul>
                </div>

                <div style="margin-bottom: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">📋 Sistema de Seguimiento</h2>
                    <p>Cada empresa tiene una sección de <strong>Seguimiento</strong> que permite gestionar el estado del contacto:</p>
                    
                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">Estados</h3>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li><strong>⚪ Pendiente</strong>: Aún no se ha contactado con la empresa</li>
                        <li><strong>🟡 Contactado</strong>: Ya se ha establecido contacto inicial</li>
                        <li><strong>🔵 En Proceso</strong>: Hay negociaciones o seguimiento activo en curso</li>
                        <li><strong>🟢 Finalizado</strong>: El seguimiento de esta empresa está completado</li>
                    </ul>
                    <p style="margin-top: 10px;"><strong>Importante</strong>: El estado seleccionado se refleja automáticamente en las estadísticas del dashboard.</p>

                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">Información de Seguimiento</h3>
                    <p>Para cada empresa puedes registrar: responsable, email, fecha de seguimiento, próxima acción y lista de acciones pendientes.</p>
                    
                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">💬 Respuestas</h3>
                    <p>Sección ubicada debajo de "➕ Añadir Acción" que permite registrar <strong>múltiples respuestas</strong> sobre cada empresa. Cada respuesta puede contener texto extenso y aplicar formato especial:</p>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li><strong>Negrita</strong>: Resalta texto importante con formato en negrita</li>
                        <li><strong>Lista</strong>: Formatea el texto como lista con viñetas</li>
                    </ul>
                    <p style="margin-top: 10px;">Puedes añadir tantas respuestas como necesites. Cada respuesta se ajusta automáticamente según el contenido y se guarda junto con el resto de la información de la empresa.</p>
                    
                    <h3 style="color: #764ba2; margin-top: 15px; margin-bottom: 10px; font-size: 16px;">📝 Conclusión Final</h3>
                    <p>Campo único ubicado después de la sección "Respuestas" que permite documentar la <strong>decisión final</strong> sobre cada empresa. Este campo también soporta formato especial (negrita y listas) y permite reportar la conclusión definitiva del seguimiento.</p>
                    <p style="margin-top: 10px;">Al hacer clic en el botón <strong>"✓ Marcar como Finalizado"</strong>, la tarjeta completa cambia su fondo a un <strong>verde suave</strong>, indicando visualmente que el seguimiento de esa empresa está completado. Toda esta información se guarda automáticamente y se exporta tanto en JSON como en Word.</p>
                </div>

                <div style="margin-bottom: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">🔍 Filtros y Búsqueda</h2>
                    <p>En la parte superior encontrarás un panel de filtros:</p>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li><strong>🔍 Buscar</strong>: Busca en nombre de empresa o producto/servicio</li>
                        <li><strong>🏢 Departamento</strong>: Filtra por Lizarte o Innovación</li>
                        <li><strong>👤 Responsable</strong>: Filtra por la persona asignada</li>
                        <li><strong>📊 Estado</strong>: Filtra por el estado de seguimiento</li>
                        <li><strong>⭐ Prioridad</strong>: Filtra por nivel de prioridad</li>
                    </ul>
                    <p style="margin-top: 10px;"><strong>💡 Tip</strong>: Puedes combinar múltiples filtros para encontrar exactamente lo que buscas.</p>
                </div>

                <div style="margin-bottom: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">➕ Añadir Nueva Empresa</h2>
                    <p>Haz clic en el botón <strong>"➕ Añadir Nueva Empresa"</strong> (arriba a la derecha).</p>
                    <p>Se abrirá un menú donde puedes elegir:</p>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li><strong>🤝 Añadir Reunión</strong>: Para empresas con reunión programada</li>
                        <li><strong>📋 Añadir Info Adicional</strong>: Para empresas de interés sin reunión programada</li>
                    </ul>
                </div>

                <div style="margin-bottom: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">✏️ Editar Información</h2>
                    <p><strong>Campos de Texto</strong>: Haz clic en cualquier campo y escribe para modificar. Los cambios se guardan automáticamente.</p>
                    <p><strong>Prioridad</strong>: Haz clic en los botones numéricos (0, 1, 2, 3) en la esquina superior derecha de cada tarjeta.</p>
                    <p><strong>Departamento</strong>: Selecciona en el menú desplegable dentro de la información básica.</p>
                    <p><strong>Estado de Seguimiento</strong>: Selecciona el botón de radio correspondiente en la sección de Seguimiento.</p>
                </div>

                <div style="margin-bottom: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">📤 Exportar Datos</h2>
                    <p><strong>¿Cuándo exportar?</strong> Cuando hayas añadido nuevas empresas, modificado información importante, eliminado empresas o quieras compartir los datos actualizados con el equipo.</p>
                    <p><strong>Cómo exportar</strong>:</p>
                    <ol style="margin-left: 20px; margin-top: 10px;">
                        <li>Haz clic en el botón flotante <strong>"📤 EXPORTAR"</strong> (esquina inferior derecha)</li>
                        <li>El sistema generará un archivo <code>datos.json</code> con todos los datos actualizados</li>
                        <li>El archivo se descargará automáticamente</li>
                        <li>Sube el archivo a GitHub para compartirlo con el equipo</li>
                    </ol>
                    <p style="margin-top: 10px;"><strong>💡 Importante</strong>: Solo cuando subas el archivo a GitHub, los cambios serán visibles para todos los miembros del equipo.</p>
                </div>

                <div style="margin-bottom: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0;">
                    <h2 style="color: #667eea; margin-bottom: 15px; font-size: 20px;">❓ Preguntas Frecuentes</h2>
                    
                    <p style="margin-top: 15px;"><strong>¿Puedo usar la aplicación sin conexión a internet?</strong></p>
                    <p>Sí, la aplicación funciona completamente sin conexión. Solo necesitas internet para cargar la aplicación por primera vez y subir el archivo exportado a GitHub.</p>

                    <p style="margin-top: 15px;"><strong>¿Qué pasa si cierro el navegador?</strong></p>
                    <p>Todos tus cambios están guardados en el almacenamiento local. Al volver a abrir la aplicación, verás todos tus datos.</p>

                    <p style="margin-top: 15px;"><strong>¿Cómo comparto los datos con mi equipo?</strong></p>
                    <p>Exporta los datos, sube el archivo <code>datos.json</code> a GitHub y comparte el enlace de la aplicación con tu equipo.</p>

                    <p style="margin-top: 15px;"><strong>¿Los cambios se guardan automáticamente?</strong></p>
                    <p>Sí, todos los cambios se guardan automáticamente en el almacenamiento local. Solo necesitas exportar cuando quieras compartir los datos con el equipo.</p>
                </div>

                <div style="margin-top: 30px; padding-top: 20px; border-top: 2px solid #e2e8f0; text-align: center; color: #718096; font-size: 14px;">
                    <p><strong>Versión</strong>: V12 by Krum Kovachev</p>
                    <p style="margin-top: 10px;">Para dudas o problemas técnicos, contacta con el desarrollador.</p>
                </div>
            </div>
        </div>
    </div>
    
    <div id="reunionesSection" class="content-section">
        <div id="reunionesContainer" class="items-container"></div>
    </div>
    
    <div id="adicionalSection" class="content-section">
        <div id="adicionalContainer" class="items-container"></div>
    </div>
    
    <div id="nuevosCochesSection" class="content-section">
        <div style="text-align: right; margin: 15px 0;">
            <button onclick="showAddNuevoCocheModal()" style="background: linear-gradient(135deg, #10b981 0%, #059669 100%); color: white; border: none; padding: 12px 24px; border-radius: 8px; font-weight: 600; cursor: pointer; box-shadow: 0 2px 8px rgba(16, 185, 129, 0.3); font-size: 14px;">
                ➕ Añadir Nuevo Coche
            </button>
        </div>
        <div id="nuevosCochesContainer" class="items-container"></div>
    </div>
    
    <div id="ahorrosSection" class="content-section">
        <div style="text-align: right; margin: 15px 0;">
            <button onclick="showAddAhorroModal()" style="background: linear-gradient(135deg, #10b981 0%, #059669 100%); color: white; border: none; padding: 12px 24px; border-radius: 8px; font-weight: 600; cursor: pointer; box-shadow: 0 2px 8px rgba(16, 185, 129, 0.3); font-size: 14px;">
                ➕ Añadir Ahorro
            </button>
        </div>
        <div id="ahorrosContainer" class="items-container"></div>
    </div>
    
    <div id="configSection" class="content-section">
        <div class="config-section">
            <div class="config-title">⚙️ Configuración General</div>
            
            <div class="config-group">
                <label>Título Principal</label>
                <input type="text" id="configTitulo" value="Seguimiento Automechanika Shanghai 2025">
            </div>
            
            <div class="config-group">
                <label>Subtítulo</label>
                <input type="text" id="configSubtitulo" value="Lizarte - Sistema de Gestión de Contactos">
            </div>
            
            <div class="config-group">
                <label>Miembros del Equipo (separados por comas)</label>
                <textarea id="configEquipo">Innovación, Calidad, Comercial, Dirección, Compras</textarea>
            </div>
            
            <div class="config-group">
                <label>Notas Generales del Proyecto</label>
                <textarea id="configNotas" placeholder="Añade notas generales sobre la feria, objetivos, conclusiones..."></textarea>
            </div>
            
            <button class="btn-save-config" onclick="saveConfig()">💾 Guardar Configuración</button>
        </div>
    </div>
    
    <button class="btn-export" onclick="exportarInforme()">
        📊 Exportar Informe Completo
    </button>
    
    <div id="photoModal" class="modal" onclick="closeModal()">
        <span class="modal-close">&times;</span>
        <img id="modalImage" class="modal-content">
    </div>
    
    <div id="saveIndicator" class="save-indicator">✓ Guardado</div>
    
    <input type="file" id="fileInput" accept="image/*" multiple style="display: none;" onchange="handleFileUpload(event)">
    
    <script>
        let appData = null;
        let equipoLizarte = [];
        let currentUploadTarget = null;
        let appConfig = {
            titulo: 'Seguimiento Automechanika Shanghai 2025',
            subtitulo: 'Lizarte - Sistema de Gestión de Contactos',
            equipo: 'Innovación, Calidad, Comercial, Dirección, Compras',
            notas: ''
        };
        
        async function loadData() {
            try {
            const response = await fetch('datos.json');
                if (!response.ok) {
                    throw new Error('Error al cargar datos.json');
                }
            appData = await response.json();
                
                console.log('📥 JSON cargado - Reuniones:', appData.reuniones.length, 'Adicional:', appData.adicional.length);
                console.log('📋 Total empresas en JSON:', appData.reuniones.length + appData.adicional.length);
                
                // Inicializar nuevos arrays si no existen
                if (!appData.nuevosCoches) appData.nuevosCoches = [];
                if (!appData.ahorros) appData.ahorros = [];
            } catch (error) {
                console.error('❌ Error al cargar datos:', error);
                // Inicializar con estructura vacía si falla la carga
                appData = {
                    reuniones: [],
                    adicional: [],
                    nuevosCoches: [],
                    ahorros: []
                };
                console.log('⚠️ Inicializando con estructura vacía');
            }
            
            // Inicializar campos básicos si no existen en el JSON (ANTES de aplicar modificaciones)
            appData.reuniones.forEach(item => {
                if (!item.seguimiento) {
                    item.seguimiento = {
                        responsable: '',
                        email: '',
                        estado: 'pendiente',
                        acciones: [],
                        fecha_contacto: '',
                        notas: ''
                    };
                }
                if (!item.seguimiento.acciones) item.seguimiento.acciones = [];
                if (!item.seguimiento.estado) item.seguimiento.estado = 'pendiente';
                if (!item.fotos || !Array.isArray(item.fotos)) item.fotos = [];
                if (!item.fotos_extra) item.fotos_extra = [];
                if (!item.documentos) item.documentos = [];
            });
            
            appData.adicional.forEach(item => {
                if (!item.seguimiento) {
                    item.seguimiento = {
                        responsable: '',
                        email: '',
                        estado: 'pendiente',
                        acciones: [],
                        fecha_contacto: '',
                        notas: ''
                    };
                }
                if (!item.seguimiento.acciones) item.seguimiento.acciones = [];
                if (!item.seguimiento.estado) item.seguimiento.estado = 'pendiente';
                if (!item.fotos || !Array.isArray(item.fotos)) item.fotos = [];
                if (!item.fotos_extra) item.fotos_extra = [];
                if (!item.documentos) item.documentos = [];
            });
            
            loadConfig();
            
            // Cargar lista de empresas eliminadas PRIMERO para evitar añadirlas
            const empresasEliminadas = JSON.parse(localStorage.getItem('empresas_eliminadas_automechanika') || '{}');
            console.log('🗑️ Empresas eliminadas en localStorage:', empresasEliminadas);
            
            // Aplicar modificaciones de localStorage (textos modificados y nuevas empresas)
            console.log('📝 Aplicando modificaciones de localStorage...');
            const textosModificados = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
            console.log('📋 Total items en textosModificados:', Object.keys(textosModificados).length);
            
            // Función auxiliar para verificar si un ID fue eliminado
            const fueEliminada = (id) => {
                const idStr = String(id);
                const idNum = Number(id);
                return (empresasEliminadas.reuniones && (
                    empresasEliminadas.reuniones.includes(idStr) || 
                    empresasEliminadas.reuniones.includes(id) ||
                    empresasEliminadas.reuniones.includes(idNum) ||
                    empresasEliminadas.reuniones.some(eid => String(eid) === idStr || Number(eid) === idNum)
                )) || (empresasEliminadas.adicional && (
                    empresasEliminadas.adicional.includes(idStr) || 
                    empresasEliminadas.adicional.includes(id) ||
                    empresasEliminadas.adicional.includes(idNum) ||
                    empresasEliminadas.adicional.some(eid => String(eid) === idStr || Number(eid) === idNum)
                ));
            };
            
            // Aplicar modificaciones a empresas existentes (solo si no fueron eliminadas)
            appData.reuniones = appData.reuniones.filter(item => !fueEliminada(item.id));
            appData.reuniones.forEach(item => {
                if (textosModificados[item.id] && !fueEliminada(item.id)) {
                    console.log('📥 Cargando datos desde localStorage para reunión ID:', item.id, textosModificados[item.id]);
                    Object.assign(item, textosModificados[item.id]);
                    // Asegurar que respuestas, conclusionFinal y finalizado se copien explícitamente
                    if (textosModificados[item.id].respuestas !== undefined) {
                        item.respuestas = textosModificados[item.id].respuestas;
                        console.log('✅ Respuestas cargadas para ID', item.id, ':', item.respuestas);
                    }
                    if (textosModificados[item.id].conclusionFinal !== undefined) {
                        item.conclusionFinal = textosModificados[item.id].conclusionFinal;
                        console.log('✅ Conclusión final cargada para ID', item.id, ':', item.conclusionFinal);
                    }
                    if (textosModificados[item.id].finalizado !== undefined) {
                        item.finalizado = textosModificados[item.id].finalizado;
                        console.log('✅ Finalizado cargado para ID', item.id, ':', item.finalizado);
                    }
                }
            });
            
            appData.adicional = appData.adicional.filter(item => !fueEliminada(item.id));
            appData.adicional.forEach(item => {
                if (textosModificados[item.id] && !fueEliminada(item.id)) {
                    console.log('📥 Cargando datos desde localStorage para adicional ID:', item.id, textosModificados[item.id]);
                    Object.assign(item, textosModificados[item.id]);
                    // Asegurar que respuestas, conclusionFinal y finalizado se copien explícitamente
                    if (textosModificados[item.id].respuestas !== undefined) {
                        item.respuestas = textosModificados[item.id].respuestas;
                        console.log('✅ Respuestas cargadas para ID', item.id, ':', item.respuestas);
                    }
                    if (textosModificados[item.id].conclusionFinal !== undefined) {
                        item.conclusionFinal = textosModificados[item.id].conclusionFinal;
                        console.log('✅ Conclusión final cargada para ID', item.id, ':', item.conclusionFinal);
                    }
                    if (textosModificados[item.id].finalizado !== undefined) {
                        item.finalizado = textosModificados[item.id].finalizado;
                        console.log('✅ Finalizado cargado para ID', item.id, ':', item.finalizado);
                    }
                }
            });
            
            // Inicializar respuestas, conclusionFinal y finalizado DESPUÉS de aplicar modificaciones (solo si no existen)
            appData.reuniones.forEach(item => {
                if (!item.respuestas || !Array.isArray(item.respuestas)) {
                    item.respuestas = [];
                    console.log('⚠️ Inicializando respuestas vacías para ID', item.id);
                }
                if (item.conclusionFinal === undefined) {
                    item.conclusionFinal = '';
                    console.log('⚠️ Inicializando conclusión final vacía para ID', item.id);
                }
                if (item.finalizado === undefined) {
                    item.finalizado = false;
                    console.log('⚠️ Inicializando finalizado false para ID', item.id);
                }
            });
            
            appData.adicional.forEach(item => {
                if (!item.respuestas || !Array.isArray(item.respuestas)) {
                    item.respuestas = [];
                    console.log('⚠️ Inicializando respuestas vacías para ID', item.id);
                }
                if (item.conclusionFinal === undefined) {
                    item.conclusionFinal = '';
                    console.log('⚠️ Inicializando conclusión final vacía para ID', item.id);
                }
                if (item.finalizado === undefined) {
                    item.finalizado = false;
                    console.log('⚠️ Inicializando finalizado false para ID', item.id);
                }
            });
            
            // Añadir NUEVAS empresas que no están en el JSON base Y no fueron eliminadas
            Object.keys(textosModificados).forEach(id => {
                // No añadir si fue eliminada
                if (fueEliminada(id)) {
                    console.log('🚫 Omitiendo empresa eliminada desde textos_modificados (ID:', id, ')');
                    return;
                }
                
                const existeEnReuniones = appData.reuniones.find(item => String(item.id) === String(id));
                const existeEnAdicional = appData.adicional.find(item => String(item.id) === String(id));
                
                if (!existeEnReuniones && !existeEnAdicional) {
                    const nuevaEmpresa = textosModificados[id];
                    if (nuevaEmpresa.company !== undefined) {
                        console.log('➕ Añadiendo nueva reunión desde localStorage:', nuevaEmpresa.company);
                        appData.reuniones.push({
                            id: id,
                            ...nuevaEmpresa
                        });
                    } else if (nuevaEmpresa.empresa !== undefined) {
                        console.log('➕ Añadiendo nueva empresa adicional desde localStorage:', nuevaEmpresa.empresa);
                        appData.adicional.push({
                            id: id,
                            ...nuevaEmpresa
                        });
                    }
                }
            });
            
            // Aplicar seguimiento de localStorage (por si acaso hay diferencias)
            const seguimientoData = JSON.parse(localStorage.getItem('seguimiento_v2_automechanika') || '{}');
            appData.reuniones.forEach(item => {
                if (seguimientoData[item.id] && !fueEliminada(item.id)) {
                    item.seguimiento = seguimientoData[item.id];
                }
            });
            appData.adicional.forEach(item => {
                if (seguimientoData[item.id] && !fueEliminada(item.id)) {
                    item.seguimiento = seguimientoData[item.id];
                }
            });
            
            // Filtrado final adicional por seguridad (aunque ya se filtró arriba)
            if (empresasEliminadas.reuniones && empresasEliminadas.reuniones.length > 0) {
                console.log('🗑️ Filtrado final - Eliminando', empresasEliminadas.reuniones.length, 'reuniones eliminadas');
                const antes = appData.reuniones.length;
                appData.reuniones = appData.reuniones.filter(item => !fueEliminada(item.id));
                console.log('🗑️ Reuniones antes:', antes, 'después:', appData.reuniones.length);
            }
            if (empresasEliminadas.adicional && empresasEliminadas.adicional.length > 0) {
                console.log('🗑️ Filtrado final - Eliminando', empresasEliminadas.adicional.length, 'empresas adicionales eliminadas');
                const antes = appData.adicional.length;
                appData.adicional = appData.adicional.filter(item => !fueEliminada(item.id));
                console.log('🗑️ Adicional antes:', antes, 'después:', appData.adicional.length);
            }
            
            console.log('✅ Datos procesados - Reuniones:', appData.reuniones.length, 'Adicional:', appData.adicional.length);
            console.log('📋 Total empresas después de aplicar modificaciones:', appData.reuniones.length + appData.adicional.length);
            
            // Asegurar que los arrays existen
            if (!appData.nuevosCoches) appData.nuevosCoches = [];
            if (!appData.ahorros) appData.ahorros = [];
            
            // Cargar nuevos coches y ahorros desde localStorage
            try {
                const nuevosCochesData = localStorage.getItem('nuevos_coches_automechanika');
                if (nuevosCochesData) {
                    appData.nuevosCoches = JSON.parse(nuevosCochesData);
                    console.log('🚗 Nuevos coches cargados desde localStorage:', appData.nuevosCoches.length);
                }
                
                const ahorrosData = localStorage.getItem('ahorros_automechanika');
                if (ahorrosData) {
                    appData.ahorros = JSON.parse(ahorrosData);
                    console.log('💰 Ahorros cargados desde localStorage:', appData.ahorros.length);
                    
                    // Inicializar campos faltantes en ahorros existentes
                    appData.ahorros.forEach(item => {
                        if (!item.moneda) item.moneda = 'EUR';
                        if (!item.tasaCambio) item.tasaCambio = 1;
                        
                        // Si es EUR y no tiene valores EUR, usar valores originales
                        if (item.moneda === 'EUR') {
                            if (item.precioActualEUR === undefined) {
                                item.precioActualEUR = parseFloat(item.precioActual || 0);
                            }
                            if (item.precioNuevoEUR === undefined) {
                                item.precioNuevoEUR = parseFloat(item.precioNuevo || 0);
                            }
                        }
                        // Si es USD y no tiene valores EUR, inicializar a 0 temporalmente
                        // Se convertirán cuando se renderice o cuando se actualice
                        else if (item.moneda === 'USD') {
                            if (item.precioActualEUR === undefined) {
                                item.precioActualEUR = 0;
                            }
                            if (item.precioNuevoEUR === undefined) {
                                item.precioNuevoEUR = 0;
                            }
                        }
                    });
                    
                    // Convertir ahorros en USD a EUR si es necesario (de forma asíncrona)
                    const conversionPromises = appData.ahorros.map(async (item, idx) => {
                        if (item.moneda === 'USD' && (item.precioActualEUR === 0 || item.precioActualEUR === undefined)) {
                            await convertirAhorroAEUR(idx);
                        }
                    });
                    
                    // Esperar a que todas las conversiones se completen antes de continuar
                    Promise.all(conversionPromises).then(() => {
                        console.log('✅ Conversiones de ahorros completadas');
                        saveData(); // Guardar los valores convertidos
                        if (appData) {
                            updateStats(); // Actualizar estadísticas con valores correctos
                        }
                    }).catch(error => {
                        console.error('❌ Error en conversiones de ahorros:', error);
                    });
                }
            } catch (error) {
                console.error('❌ Error al cargar nuevos coches o ahorros desde localStorage:', error);
            }
            
            populateResponsableFilter();
            renderAll();
            updateStats();
            updateTabCounters();
            setTimeout(() => addAutoResizeToAllTextareas(), 100);
        }
        
        function convertAirtableToAppData(records) {
            appData = { reuniones: [], adicional: [], nuevosCoches: [], ahorros: [] };
            
            records.forEach(record => {
                const fields = record.fields;
                
                // Guardar mapeo ID -> Airtable Record ID
                if (fields.ID) {
                    airtableRecords[fields.ID] = record.id;
                }
                
                if (fields.Tipo === 'Reunión') {
                    appData.reuniones.push({
                        id: fields.ID || record.id,
                        company: fields.Empresa || '',
                        person: fields.Persona || '',
                        product: fields.Producto || '',
                        time: fields.Hora || '',
                        stand: fields.Stand || '',
                        comments: fields.Notas || '',
                        departamento: fields.Departamento || 'Lizarte',
                        fotos: [],
                        fotos_extra: [],
                        seguimiento: {
                            responsable: fields.Responsable || '',
                            email: fields.Email || '',
                            estado: fields.Estado || 'pendiente',
                            acciones: fields.Acciones ? fields.Acciones.split('\n').filter(a => a.trim()) : [],
                            fechaSeguimiento: fields.Fecha_Seguimiento || ''
                        }
                    });
                } else if (fields.Tipo === 'Info Adicional') {
                    appData.adicional.push({
                        id: fields.ID || record.id,
                        empresa: fields.Empresa || '',
                        producto: fields.Producto || '',
                        prioridad: fields.Prioridad || 'media',
                        notas: fields.Notas || '',
                        oportunidad: fields.Oportunidad || '',
                        departamento: fields.Departamento || 'Lizarte',
                        fotos: [],
                        fotos_extra: [],
                        seguimiento: {
                            responsable: fields.Responsable || '',
                            email: fields.Email || '',
                            estado: fields.Estado || 'pendiente',
                            acciones: fields.Acciones ? fields.Acciones.split('\n').filter(a => a.trim()) : [],
                            fechaSeguimiento: fields.Fecha_Seguimiento || ''
                        }
                    });
                }
            });
            
            // Guardar mapeo actualizado
            localStorage.setItem('airtable_records_map', JSON.stringify(airtableRecords));
        }
        
        
        function loadConfig() {
            const saved = localStorage.getItem('config_automechanika');
            if (saved) {
                try {
                    const savedConfig = JSON.parse(saved);
                    console.log('📥 Cargando configuración guardada:', savedConfig);
                    
                    // Usar valores guardados si existen, sino usar valores por defecto
                    // IMPORTANTE: Usar !== undefined para permitir cadenas vacías
                    appConfig.titulo = savedConfig.titulo !== undefined ? savedConfig.titulo : appConfig.titulo;
                    appConfig.subtitulo = savedConfig.subtitulo !== undefined ? savedConfig.subtitulo : appConfig.subtitulo;
                    appConfig.equipo = savedConfig.equipo !== undefined ? savedConfig.equipo : appConfig.equipo;
                    appConfig.notas = savedConfig.notas !== undefined ? savedConfig.notas : appConfig.notas;
                    
                    console.log('✅ Configuración cargada - Equipo:', appConfig.equipo);
                    
                    // Actualizar campos del formulario
                    if (document.getElementById('configTitulo')) {
                document.getElementById('configTitulo').value = appConfig.titulo;
                    }
                    if (document.getElementById('configSubtitulo')) {
                document.getElementById('configSubtitulo').value = appConfig.subtitulo;
                    }
                    if (document.getElementById('configEquipo')) {
                document.getElementById('configEquipo').value = appConfig.equipo;
                    }
                    if (document.getElementById('configNotas')) {
                document.getElementById('configNotas').value = appConfig.notas || '';
                    }
                    
                    // Actualizar título y subtítulo en la interfaz
                    const h1 = document.querySelector('h1');
                    if (h1) h1.textContent = appConfig.titulo;
                    const subtitle = document.querySelector('.subtitle');
                    if (subtitle) subtitle.textContent = appConfig.subtitulo;
                } catch (error) {
                    console.error('❌ Error cargando configuración:', error);
                }
            } else {
                console.log('ℹ️ No hay configuración guardada, usando valores por defecto');
                // Si no hay configuración guardada, usar valores por defecto
                if (document.getElementById('configTitulo')) {
                    document.getElementById('configTitulo').value = appConfig.titulo;
                }
                if (document.getElementById('configSubtitulo')) {
                    document.getElementById('configSubtitulo').value = appConfig.subtitulo;
                }
                if (document.getElementById('configEquipo')) {
                    document.getElementById('configEquipo').value = appConfig.equipo;
                }
                if (document.getElementById('configNotas')) {
                    document.getElementById('configNotas').value = appConfig.notas || '';
                }
            }
            
            // Asegurar que equipoLizarte siempre tenga un valor válido
            if (appConfig.equipo && typeof appConfig.equipo === 'string' && appConfig.equipo.trim().length > 0) {
                equipoLizarte = appConfig.equipo.split(',').map(e => e.trim()).filter(e => e.length > 0);
                console.log('👥 Equipo cargado:', equipoLizarte);
            } else {
                // Usar valor por defecto si no hay equipo válido
                const defaultEquipo = 'Innovación, Calidad, Comercial, Dirección, Compras';
                equipoLizarte = defaultEquipo.split(',').map(e => e.trim()).filter(e => e.length > 0);
                console.log('👥 Usando equipo por defecto:', equipoLizarte);
            }
        }
        
        function saveConfig() {
            // Obtener valores de los campos
            const titulo = document.getElementById('configTitulo').value.trim();
            const subtitulo = document.getElementById('configSubtitulo').value.trim();
            const equipo = document.getElementById('configEquipo').value.trim();
            const notas = document.getElementById('configNotas').value.trim();
            
            // Validar que el campo equipo no esté vacío
            if (!equipo) {
                alert('⚠️ El campo "Miembros del Equipo" no puede estar vacío');
                return;
            }
            
            // Actualizar appConfig
            appConfig.titulo = titulo;
            appConfig.subtitulo = subtitulo;
            appConfig.equipo = equipo;
            appConfig.notas = notas;
            
            console.log('💾 Guardando configuración:', appConfig);
            
            // Guardar en localStorage
            try {
            localStorage.setItem('config_automechanika', JSON.stringify(appConfig));
                console.log('✅ Configuración guardada en localStorage');
                
                // Verificar que se guardó correctamente
                const verificacion = localStorage.getItem('config_automechanika');
                if (verificacion) {
                    const verificado = JSON.parse(verificacion);
                    console.log('✅ Verificación - Equipo guardado:', verificado.equipo);
                }
            } catch (error) {
                console.error('❌ Error guardando configuración:', error);
                alert('❌ Error al guardar la configuración. Verifica la consola para más detalles.');
                return;
            }
            
            // Actualizar la interfaz
            const h1 = document.querySelector('h1');
            if (h1) h1.textContent = appConfig.titulo;
            const subtitle = document.querySelector('.subtitle');
            if (subtitle) subtitle.textContent = appConfig.subtitulo;
            
            // Actualizar la lista de responsables
            equipoLizarte = appConfig.equipo.split(',').map(e => e.trim()).filter(e => e.length > 0);
            console.log('👥 Equipo actualizado:', equipoLizarte);
            populateResponsableFilter();
            renderAll();
            
            showSaveIndicator();
            alert('✅ Configuración guardada correctamente');
        }
        
        function loadSeguimiento() {
            const saved = localStorage.getItem('seguimiento_v2_automechanika');
            if (saved) {
                const seguimientoData = JSON.parse(saved);
                
                appData.reuniones.forEach(item => {
                    if (seguimientoData[item.id]) {
                        item.seguimiento = seguimientoData[item.id];
                        if (!item.seguimiento.acciones) item.seguimiento.acciones = [];
                        if (!item.seguimiento.estado) item.seguimiento.estado = 'pendiente';
                        if (!item.seguimiento.email) item.seguimiento.email = '';
                        if (!item.fotos_extra) item.fotos_extra = [];
                    }
                });
                
                appData.adicional.forEach(item => {
                    if (seguimientoData[item.id]) {
                        item.seguimiento = seguimientoData[item.id];
                        if (!item.seguimiento.acciones) item.seguimiento.acciones = [];
                        if (!item.seguimiento.estado) item.seguimiento.estado = 'pendiente';
                        if (!item.seguimiento.email) item.seguimiento.email = '';
                    }
                });
            }
            
            // Cargar fotos borradas
            const deletedPhotos = localStorage.getItem('deleted_photos_automechanika');
            if (deletedPhotos) {
                const deletedList = JSON.parse(deletedPhotos);
                appData.reuniones.forEach(item => {
                    const itemDeleted = deletedList[item.id];
                    if (itemDeleted && itemDeleted.length > 0) {
                        // Filtrar fotos borradas
                        if (!item.fotos || !Array.isArray(item.fotos)) item.fotos = [];
                        item.fotos = item.fotos.filter((foto, idx) => !itemDeleted.includes(idx));
                    }
                });
            }
            
            // Cargar fotos extra
            const fotosExtra = localStorage.getItem('fotos_extra_automechanika');
            if (fotosExtra) {
                const fotosExtraData = JSON.parse(fotosExtra);
                appData.reuniones.forEach(item => {
                    if (fotosExtraData[item.id]) {
                        item.fotos_extra = fotosExtraData[item.id];
                    }
                });
            }
            
            // Cargar textos modificados
            const textosModificados = localStorage.getItem('textos_modificados_automechanika');
            if (textosModificados) {
                const textosData = JSON.parse(textosModificados);
                appData.reuniones.forEach(item => {
                    if (textosData[item.id]) {
                        Object.keys(textosData[item.id]).forEach(field => {
                            item[field] = textosData[item.id][field];
                        });
                    }
                });
                appData.adicional.forEach(item => {
                    if (textosData[item.id]) {
                        Object.keys(textosData[item.id]).forEach(field => {
                            item[field] = textosData[item.id][field];
                        });
                    }
                });
            }
            
            // Inicializar campos nuevos
            appData.reuniones.forEach(item => {
                if (!item.seguimiento.acciones) item.seguimiento.acciones = [];
                if (!item.seguimiento.estado) item.seguimiento.estado = 'pendiente';
                if (!item.seguimiento.email) item.seguimiento.email = '';
                if (!item.fotos_extra) item.fotos_extra = [];
            });
            
            appData.adicional.forEach(item => {
                if (!item.seguimiento.acciones) item.seguimiento.acciones = [];
                if (!item.seguimiento.estado) item.seguimiento.estado = 'pendiente';
                if (!item.seguimiento.email) item.seguimiento.email = '';
                if (!item.fotos) item.fotos = [];
                if (!item.fotos_extra) item.fotos_extra = [];
            });
        }
        
        function saveSeguimiento() {
            const seguimientoData = {};
            
            appData.reuniones.forEach(item => {
                seguimientoData[item.id] = item.seguimiento;
            });
            
            appData.adicional.forEach(item => {
                seguimientoData[item.id] = item.seguimiento;
            });
            
            localStorage.setItem('seguimiento_v2_automechanika', JSON.stringify(seguimientoData));
            
            // Guardar fotos extra
            const fotosExtra = {};
            appData.reuniones.forEach(item => {
                if (item.fotos_extra && item.fotos_extra.length > 0) {
                    fotosExtra[item.id] = item.fotos_extra;
                }
            });
            localStorage.setItem('fotos_extra_automechanika', JSON.stringify(fotosExtra));
            
            showSaveIndicator();
            updateStats();
        }
        
        function showSaveIndicator() {
            const indicator = document.getElementById('saveIndicator');
            indicator.classList.add('show');
            setTimeout(() => indicator.classList.remove('show'), 2000);
        }
        
        function updateTabCounters() {
            // Actualizar contadores en las pestañas
            const numReuniones = appData.reuniones.length;
            const numAdicional = appData.adicional.length;
            const numNuevosCoches = (appData.nuevosCoches || []).length;
            const numAhorros = (appData.ahorros || []).length;
            
            console.log('🔢 Actualizando contadores de pestañas - Reuniones:', numReuniones, 'Adicional:', numAdicional, 'Nuevos Coches:', numNuevosCoches, 'Ahorros:', numAhorros);
            
            // Buscar y actualizar el botón de pestaña "Reuniones"
            const tabs = document.querySelectorAll('.tab');
            let reunionesUpdated = false;
            let adicionalUpdated = false;
            let nuevosCochesUpdated = false;
            let ahorrosUpdated = false;
            
            tabs.forEach(tab => {
                const text = tab.textContent || '';
                const onclickAttr = tab.getAttribute('onclick');
                
                // Buscar por el onclick que contiene 'reuniones' o 'adicional'
                const onclickValue = onclickAttr || '';
                
                if (onclickValue.includes("switchTab('reuniones')") || text.includes('Reuniones')) {
                    // Reemplazar el número manteniendo el emoji y el texto
                    tab.textContent = `🤝 Reuniones (${numReuniones})`;
                    if (onclickAttr) tab.setAttribute('onclick', onclickAttr);
                    reunionesUpdated = true;
                    console.log('✅ Contador Reuniones actualizado a:', numReuniones);
                } else if (onclickValue.includes("switchTab('adicional')") || text.includes('Info Adicional')) {
                    // Reemplazar el número manteniendo el emoji y el texto
                    tab.textContent = `📋 Info Adicional (${numAdicional})`;
                    if (onclickAttr) tab.setAttribute('onclick', onclickAttr);
                    adicionalUpdated = true;
                    console.log('✅ Contador Info Adicional actualizado a:', numAdicional);
                } else if (onclickValue.includes("switchTab('nuevosCoches')") || text.includes('Nuevos Coches')) {
                    tab.textContent = `🚗 Nuevos Coches (${numNuevosCoches})`;
                    if (onclickAttr) tab.setAttribute('onclick', onclickAttr);
                    nuevosCochesUpdated = true;
                    console.log('✅ Contador Nuevos Coches actualizado a:', numNuevosCoches);
                } else if (onclickValue.includes("switchTab('ahorros')") || text.includes('Ahorros Conseguidos')) {
                    tab.textContent = `💰 Ahorros Conseguidos (${numAhorros})`;
                    if (onclickAttr) tab.setAttribute('onclick', onclickAttr);
                    ahorrosUpdated = true;
                    console.log('✅ Contador Ahorros actualizado a:', numAhorros);
                }
            });
            
            if (!reunionesUpdated) {
                console.warn('⚠️ No se encontró la pestaña de Reuniones para actualizar');
            }
            if (!adicionalUpdated) {
                console.warn('⚠️ No se encontró la pestaña de Info Adicional para actualizar');
            }
            if (!nuevosCochesUpdated) {
                console.warn('⚠️ No se encontró la pestaña de Nuevos Coches para actualizar');
            }
            if (!ahorrosUpdated) {
                console.warn('⚠️ No se encontró la pestaña de Ahorros para actualizar');
            }
        }
        
        function updateStats() {
            const allItems = [...appData.reuniones, ...appData.adicional];
            const total = allItems.length;
            const pendientes = allItems.filter(i => i.seguimiento.estado === 'pendiente').length;
            const contactados = allItems.filter(i => i.seguimiento.estado === 'contactado').length;
            const proceso = allItems.filter(i => i.seguimiento.estado === 'proceso').length;
            const finalizados = allItems.filter(i => i.seguimiento.estado === 'finalizado').length;
            
            console.log('📊 Calculando estadísticas - Total:', total, 'Reuniones:', appData.reuniones.length, 'Adicional:', appData.adicional.length);
            
            // Actualizar contadores del dashboard principal
            const statTotalEl = document.getElementById('statTotal');
            if (statTotalEl) {
                statTotalEl.textContent = total;
                console.log('✅ statTotal actualizado a:', total);
            } else {
                console.warn('⚠️ No se encontró el elemento statTotal');
            }
            
            const statPendientesEl = document.getElementById('statPendientes');
            if (statPendientesEl) statPendientesEl.textContent = pendientes;
            const statContactadosEl = document.getElementById('statContactados');
            if (statContactadosEl) statContactadosEl.textContent = contactados;
            const statProcesoEl = document.getElementById('statProceso');
            if (statProcesoEl) statProcesoEl.textContent = proceso;
            const statFinalizadosEl = document.getElementById('statFinalizados');
            if (statFinalizadosEl) statFinalizadosEl.textContent = finalizados;
            
            // Actualizar contadores de las pestañas
            updateTabCounters();
            
            // Actualizar contadores de la pantalla splash
            const numReuniones = appData.reuniones.length;
            const numOportunidades = allItems.filter(item => (item.departamento || 'Lizarte') === 'Innovación').length;
            
            // Contar fotos totales
            let numFotos = 0;
            appData.reuniones.forEach(item => {
                numFotos += (Array.isArray(item.fotos) ? item.fotos.length : 0);
                numFotos += (Array.isArray(item.fotos_extra) ? item.fotos_extra.length : 0);
            });
            appData.adicional.forEach(item => {
                numFotos += (Array.isArray(item.fotos) ? item.fotos.length : 0);
                numFotos += (Array.isArray(item.fotos_extra) ? item.fotos_extra.length : 0);
            });
            
            // Calcular ahorro total en EUR
            let ahorroTotal = 0;
            if (appData.ahorros && appData.ahorros.length > 0) {
                appData.ahorros.forEach(item => {
                    // Usar valores en EUR si existen, sino usar valores originales
                    const precioActualEUR = item.precioActualEUR !== undefined ? item.precioActualEUR : parseFloat(item.precioActual || 0);
                    const precioNuevoEUR = item.precioNuevoEUR !== undefined ? item.precioNuevoEUR : parseFloat(item.precioNuevo || 0);
                    const unidadesAno = parseFloat(item.unidadesAno || 0);
                    const ahorroUnitarioEUR = precioActualEUR - precioNuevoEUR;
                    const ahorroItem = ahorroUnitarioEUR * unidadesAno;
                    ahorroTotal += ahorroItem;
                });
            }
            
            // Actualizar los elementos de la pantalla splash si existen
            const stat1El = document.getElementById('stat1');
            if (stat1El) stat1El.textContent = total;
            const stat2El = document.getElementById('stat2');
            if (stat2El) stat2El.textContent = numReuniones;
            const stat3El = document.getElementById('stat3');
            if (stat3El) stat3El.textContent = numFotos;
            const stat4El = document.getElementById('stat4');
            if (stat4El) stat4El.textContent = numOportunidades;
            const stat5El = document.getElementById('stat5');
            if (stat5El) {
                // Solo actualizar si el splash screen no está visible
                const splashScreen = document.getElementById('splashScreen');
                if (!splashScreen || splashScreen.style.display === 'none') {
                    const ahorroFormateado = formatearMoneda(ahorroTotal);
                    stat5El.textContent = ahorroFormateado;
                }
            }
        }
        
        function populateResponsableFilter() {
            const select = document.getElementById('filterResponsable');
            select.innerHTML = '<option value="">Todos</option>';
            equipoLizarte.forEach(nombre => {
                const option = document.createElement('option');
                option.value = nombre;
                option.textContent = nombre;
                select.appendChild(option);
            });
        }
        
        function switchTab(tab) {
            try {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
            
            // Activar pestaña por nombre
            const tabs = document.querySelectorAll('.tab');
            tabs.forEach(t => {
                    const onclickAttr = t.getAttribute('onclick') || '';
                    if (onclickAttr.includes(`switchTab('${tab}')`) || t.textContent.toLowerCase().includes(tab.toLowerCase())) {
                    t.classList.add('active');
                }
            });
            
                // Activar sección de contenido
                const sectionId = tab + 'Section';
                const section = document.getElementById(sectionId);
                if (section) {
                    section.classList.add('active');
                } else {
                    console.error('❌ No se encontró la sección:', sectionId);
                }
            } catch (error) {
                console.error('❌ Error en switchTab:', error);
            }
        }
        
        function getPrioridadTexto(prioridad) {
            if (prioridad === 0) return 'MUY IMPORTANTE';
            if (prioridad === 1) return 'ALTA';
            if (prioridad === 2) return 'MEDIA';
            if (prioridad === 3) return 'BAJA';
            if (typeof prioridad === 'string') return prioridad.toUpperCase();
            return 'N/A';
        }
        
        
        function saveData() {
            // Guardar los datos de las nuevas empresas en localStorage
            const textosData = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
            
            // Actualizar textos modificados con appData actual (ESTRUCTURA COMPLETA)
            appData.reuniones.forEach(item => {
                if (!textosData[item.id]) {
                    textosData[item.id] = {};
                }
                // Guardar TODA la estructura completa del item (incluyendo respuestas, conclusionFinal y finalizado)
                textosData[item.id] = {
                    company: item.company || '',
                    person: item.person || '',
                    product: item.product || '',
                    time: item.time || '',
                    stand: item.stand || '',
                    comments: item.comments || '',
                    departamento: item.departamento || 'Lizarte',
                    prioridad: item.prioridad !== undefined ? item.prioridad : 1,
                    fotos: item.fotos || [],
                    fotos_extra: item.fotos_extra || [],
                    respuestas: item.respuestas || [],
                    conclusionFinal: item.conclusionFinal || '',
                    finalizado: item.finalizado || false,
                    seguimiento: item.seguimiento || {
                        responsable: "",
                        contactado: false,
                        respuestaRecibida: false,
                        proximaAccion: "",
                        fechaSeguimiento: "",
                        acciones: [],
                        estado: "pendiente",
                        email: ""
                    }
                };
            });
            
            appData.adicional.forEach(item => {
                if (!textosData[item.id]) {
                    textosData[item.id] = {};
                }
                // Guardar TODA la estructura completa del item (incluyendo respuestas, conclusionFinal y finalizado)
                textosData[item.id] = {
                    empresa: item.empresa || '',
                    producto: item.producto || '',
                    notas: item.notas || '',
                    oportunidad: item.oportunidad || '',
                    departamento: item.departamento || 'Lizarte',
                    prioridad: item.prioridad !== undefined ? item.prioridad : 1,
                    fotos: item.fotos || [],
                    fotos_extra: item.fotos_extra || [],
                    respuestas: item.respuestas || [],
                    conclusionFinal: item.conclusionFinal || '',
                    finalizado: item.finalizado || false,
                    seguimiento: item.seguimiento || {
                        responsable: "",
                        contactado: false,
                        respuestaRecibida: false,
                        proximaAccion: "",
                        fechaSeguimiento: "",
                        acciones: [],
                        estado: "pendiente"
                    }
                };
            });
            
            localStorage.setItem('textos_modificados_automechanika', JSON.stringify(textosData));
            console.log('💾 Datos guardados en localStorage (estructura completa con fotos)');
            
            // Guardar nuevos coches y ahorros en localStorage
            if (appData.nuevosCoches) {
                localStorage.setItem('nuevos_coches_automechanika', JSON.stringify(appData.nuevosCoches));
                console.log('💾 Nuevos coches guardados:', appData.nuevosCoches.length);
            }
            
            if (appData.ahorros) {
                localStorage.setItem('ahorros_automechanika', JSON.stringify(appData.ahorros));
                console.log('💾 Ahorros guardados:', appData.ahorros.length);
            }
        }
        
        function showAddEmpresaModal() {
            document.getElementById('addEmpresaModal').style.display = 'flex';
        }
        
        function hideAddEmpresaModal() {
            document.getElementById('addEmpresaModal').style.display = 'none';
        }
        
        function addNewReunion() {
            try {
                console.log('📝 Añadiendo nueva reunión...');
                
                // Cerrar modal primero
                hideAddEmpresaModal();
                
                const newReunion = {
                    company: "Nueva Empresa",
                    person: "",
                    product: "",
                    time: "",
                    stand: "",
                    comments: "",
                    id: Date.now(),
                    fotos: [],
                    seguimiento: {
                        responsable: "",
                        contactado: false,
                        respuestaRecibida: false,
                        proximaAccion: "",
                        fechaSeguimiento: "",
                        acciones: [],
                        estado: "pendiente",
                        email: ""
                    },
                    departamento: "Lizarte",
                    prioridad: 1
                };
                
                appData.reuniones.push(newReunion);
                saveData();
                
                // Cambiar a pestaña reuniones
                switchTab('reuniones');
                
                renderAll();
                updateStats();
                
                setTimeout(() => {
                    addAutoResizeToAllTextareas();
                    // Scroll al final donde está la nueva empresa
                    const container = document.getElementById('reunionesContainer');
                    if (container) {
                        // Buscar el último elemento hijo válido (no nodos de texto)
                        let lastElement = container.lastElementChild;
                        if (!lastElement) {
                            // Si no hay lastElementChild, buscar el último nodo que sea un Element
                            let child = container.lastChild;
                            while (child && child.nodeType !== 1) {
                                child = child.previousSibling;
                            }
                            lastElement = child;
                        }
                        if (lastElement && typeof lastElement.scrollIntoView === 'function') {
                            lastElement.scrollIntoView({ behavior: 'smooth', block: 'start' });
                        }
                    }
                }, 100);
                
                console.log('✅ Reunión añadida');
            } catch (error) {
                console.error('❌ Error añadiendo reunión:', error);
                alert('Error al añadir empresa. Por favor, revisa la consola (F12).');
            }
        }
        
        function addNewAdicional() {
            try {
                console.log('📝 Añadiendo nueva empresa en adicional...');
                
                // Cerrar modal primero
                hideAddEmpresaModal();
                
                const newAdicional = {
                    id: "add_" + Date.now(),
                    empresa: "Nueva Empresa",
                    producto: "",
                    notas: "",
                    oportunidad: "",
                    prioridad: 1,
                    seguimiento: {
                        responsable: "",
                        contactado: false,
                        respuestaRecibida: false,
                        proximaAccion: "",
                        fechaSeguimiento: "",
                        acciones: [],
                        estado: "pendiente"
                    },
                    departamento: "Lizarte",
                    fotos: []
                };
                
                appData.adicional.push(newAdicional);
                saveData();
                
                // Cambiar a pestaña adicional
                switchTab('adicional');
                
                renderAll();
                updateStats();
                
                setTimeout(() => {
                    addAutoResizeToAllTextareas();
                    // Scroll al final donde está la nueva empresa
                    const container = document.getElementById('adicionalContainer');
                    if (container) {
                        // Buscar el último elemento hijo válido (no nodos de texto)
                        let lastElement = container.lastElementChild;
                        if (!lastElement) {
                            // Si no hay lastElementChild, buscar el último nodo que sea un Element
                            let child = container.lastChild;
                            while (child && child.nodeType !== 1) {
                                child = child.previousSibling;
                            }
                            lastElement = child;
                        }
                        if (lastElement && typeof lastElement.scrollIntoView === 'function') {
                            lastElement.scrollIntoView({ behavior: 'smooth', block: 'start' });
                        }
                    }
                }, 100);
                
                console.log('✅ Empresa adicional añadida');
            } catch (error) {
                console.error('❌ Error añadiendo empresa adicional:', error);
                alert('Error al añadir empresa. Por favor, revisa la consola (F12).');
            }
        }
        
        function deleteReunion(index) {
            if (confirm('¿Estás seguro de que quieres eliminar esta empresa?')) {
                const item = appData.reuniones[index];
                const itemId = item.id;
                
                // Guardar en lista de empresas eliminadas
                const empresasEliminadas = JSON.parse(localStorage.getItem('empresas_eliminadas_automechanika') || '{}');
                if (!empresasEliminadas.reuniones) empresasEliminadas.reuniones = [];
                const itemIdStr = String(itemId);
                if (!empresasEliminadas.reuniones.includes(itemIdStr) && !empresasEliminadas.reuniones.includes(itemId)) {
                    empresasEliminadas.reuniones.push(itemIdStr);
                }
                localStorage.setItem('empresas_eliminadas_automechanika', JSON.stringify(empresasEliminadas));
                
                // Eliminar de appData
                appData.reuniones.splice(index, 1);
                
                // Eliminar de textos_modificados si existe
                const textosData = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
                delete textosData[itemIdStr];
                delete textosData[itemId];
                localStorage.setItem('textos_modificados_automechanika', JSON.stringify(textosData));
                
                saveData();
                renderAll();
                updateStats();
                console.log('🗑️ Empresa eliminada:', item.company, '(ID:', itemId, ')');
            }
        }
        
        function deleteAdicional(index) {
            if (confirm('¿Estás seguro de que quieres eliminar esta empresa?')) {
                const item = appData.adicional[index];
                const itemId = item.id;
                
                // Guardar en lista de empresas eliminadas
                const empresasEliminadas = JSON.parse(localStorage.getItem('empresas_eliminadas_automechanika') || '{}');
                if (!empresasEliminadas.adicional) empresasEliminadas.adicional = [];
                const itemIdStr = String(itemId);
                if (!empresasEliminadas.adicional.includes(itemIdStr) && !empresasEliminadas.adicional.includes(itemId)) {
                    empresasEliminadas.adicional.push(itemIdStr);
                }
                localStorage.setItem('empresas_eliminadas_automechanika', JSON.stringify(empresasEliminadas));
                
                // Eliminar de appData
                appData.adicional.splice(index, 1);
                
                // Eliminar de textos_modificados si existe
                const textosData = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
                delete textosData[itemIdStr];
                delete textosData[itemId];
                localStorage.setItem('textos_modificados_automechanika', JSON.stringify(textosData));
                
                saveData();
                renderAll();
                updateStats();
                console.log('🗑️ Empresa eliminada:', item.empresa, '(ID:', itemId, ')');
            }
        }
        
        // Funciones para Nuevos Coches
        function showAddNuevoCocheModal() {
            try {
                console.log('🚗 showAddNuevoCocheModal llamada');
                if (!appData) {
                    console.error('❌ appData no está inicializado');
                    alert('Error: Los datos no están cargados. Por favor, recarga la página.');
                    return;
                }
                if (!appData.nuevosCoches) appData.nuevosCoches = [];
                const nuevoCoche = {
                    id: 'coche_' + Date.now(),
                    nombre: '',
                    descripcion: ''
                };
                appData.nuevosCoches.push(nuevoCoche);
                console.log('✅ Nuevo coche añadido. Total:', appData.nuevosCoches.length);
                saveData();
                renderNuevosCoches();
                updateTabCounters();
                // Scroll al nuevo elemento
                setTimeout(() => {
                    const container = document.getElementById('nuevosCochesContainer');
                    if (container) {
                        const lastCard = container.lastElementChild;
                        if (lastCard) lastCard.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
                    }
                }, 100);
            } catch (error) {
                console.error('❌ Error en showAddNuevoCocheModal:', error);
                alert('Error al añadir nuevo coche. Por favor, revisa la consola (F12).');
            }
        }
        
        function updateNuevoCoche(index, field, value) {
            if (!appData.nuevosCoches) appData.nuevosCoches = [];
            appData.nuevosCoches[index][field] = value;
            saveData();
        }
        
        function deleteNuevoCoche(index) {
            if (confirm('¿Estás seguro de que quieres eliminar este coche?')) {
                appData.nuevosCoches.splice(index, 1);
                saveData();
                renderNuevosCoches();
                updateTabCounters();
            }
        }
        
        // Funciones para Ahorros
        function showAddAhorroModal() {
            try {
                console.log('💰 showAddAhorroModal llamada');
                if (!appData) {
                    console.error('❌ appData no está inicializado');
                    alert('Error: Los datos no están cargados. Por favor, recarga la página.');
                    return;
                }
                if (!appData.ahorros) appData.ahorros = [];
                const nuevoAhorro = {
                    id: 'ahorro_' + Date.now(),
                    empresa: '',
                    producto: '',
                    precioActual: '',
                    precioNuevo: '',
                    unidadesAno: '',
                    moneda: 'EUR', // Por defecto EUR
                    tasaCambio: 1,
                    precioActualEUR: 0,
                    precioNuevoEUR: 0,
                    ahorroTotal: 0
                };
                appData.ahorros.push(nuevoAhorro);
                console.log('✅ Nuevo ahorro añadido. Total:', appData.ahorros.length);
                saveData();
                renderAhorros();
                updateTabCounters();
                // Scroll al nuevo elemento
                setTimeout(() => {
                    const container = document.getElementById('ahorrosContainer');
                    if (container) {
                        const lastCard = container.lastElementChild;
                        if (lastCard) lastCard.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
                    }
                }, 100);
            } catch (error) {
                console.error('❌ Error en showAddAhorroModal:', error);
                alert('Error al añadir ahorro. Por favor, revisa la consola (F12).');
            }
        }
        
        async function updateAhorro(index, field, value) {
            if (!appData.ahorros) appData.ahorros = [];
            appData.ahorros[index][field] = value;
            
            const item = appData.ahorros[index];
            
            // Si cambió la moneda o los precios, convertir a EUR
            if (field === 'moneda' || field === 'precioActual' || field === 'precioNuevo') {
                await convertirAhorroAEUR(index);
            }
            
            // Calcular ahorro total automáticamente usando valores en EUR
            const precioActualEUR = item.precioActualEUR || parseFloat(item.precioActual || 0);
            const precioNuevoEUR = item.precioNuevoEUR || parseFloat(item.precioNuevo || 0);
            const unidadesAno = parseFloat(item.unidadesAno || 0);
            const ahorroUnitarioEUR = precioActualEUR - precioNuevoEUR;
            item.ahorroTotal = ahorroUnitarioEUR * unidadesAno;
            
            saveData();
            // Re-renderizar para mostrar los valores actualizados
            renderAhorros();
        }
        
        function deleteAhorro(index) {
            if (confirm('¿Estás seguro de que quieres eliminar este ahorro?')) {
                appData.ahorros.splice(index, 1);
                saveData();
                renderAhorros();
                updateTabCounters();
            }
            }

        function addFotos(type, index, files) {
            const item = appData[type][index];
            if (!item.fotos || !Array.isArray(item.fotos)) item.fotos = [];
            
            Array.from(files).forEach(file => {
                const reader = new FileReader();
                reader.onload = (e) => {
                    const fotoName = `fotos/${type}_${item.company || item.empresa}_foto${item.fotos.length + 1}.jpg`;
                    item.fotos.push(fotoName);
                    saveData();
                    renderAll();
                };
                reader.readAsDataURL(file);
            });
        }
        
        function deleteFoto(type, index, fotoIndex) {
            if (confirm('¿Eliminar esta foto?')) {
                appData[type][index].fotos.splice(fotoIndex, 1);
                saveData();
                renderAll();
            }
        }

        function renderAll() {
            renderReuniones();
            renderAdicional();
            renderNuevosCoches();
            renderAhorros();
            
            // Aplicar auto-resize a todos los textareas después de renderizar
            setTimeout(() => {
                addAutoResizeToAllTextareas();
            }, 50);
        }
        
        function applyFilters() {
            renderAll();
        }
        
        function applyFiltersToData(items) {
            const search = document.getElementById('searchInput').value.toLowerCase();
            const departamento = document.getElementById('filterDepartamento').value;
            const responsable = document.getElementById('filterResponsable').value;
            const estado = document.getElementById('filterEstado').value;
            const prioridad = document.getElementById('filterPrioridad').value;
            
            return items.filter(item => {
                const matchSearch = !search || 
                    item.company?.toLowerCase().includes(search) ||
                    item.empresa?.toLowerCase().includes(search) ||
                    item.product?.toLowerCase().includes(search) ||
                    item.producto?.toLowerCase().includes(search);
                
                const matchDepartamento = !departamento || (item.departamento || 'Lizarte') === departamento;
                const matchResponsable = !responsable || item.seguimiento.responsable === responsable;
                const matchEstado = !estado || item.seguimiento.estado === estado;
                const matchPrioridad = !prioridad || item.prioridad === parseInt(prioridad);
                
                return matchSearch && matchDepartamento && matchResponsable && matchEstado && matchPrioridad;
            });
        }
        
        function renderReuniones() {
            const container = document.getElementById('reunionesContainer');
            console.log('🎨 Renderizando reuniones - Total en appData:', appData.reuniones.length);
            const filtered = applyFiltersToData(appData.reuniones);
            console.log('🎨 Reuniones después de filtros:', filtered.length);
            
            container.innerHTML = filtered.map((item, idx) => {
                const realIdx = appData.reuniones.indexOf(item);
                const allFotos = [...(Array.isArray(item.fotos) ? item.fotos : []), ...(item.fotos_extra || [])];
                
                return `
                <div class="item-card ${item.finalizado ? 'finalizado' : ''}">
                    <div class="item-header" style="position: relative;">
                        <div class="item-company" id="company-title-reuniones-${realIdx}">
                            ${item.company}
                            <span class="depto-badge depto-${item.departamento?.toLowerCase() || 'lizarte'}">${item.departamento || 'Lizarte'}</span>
                        </div>
                        <div style="position: absolute; top: 10px; right: 10px; display: flex; gap: 6px; align-items: center;">
                            <div style="display: flex; gap: 4px;">
                                <button onclick="updateTexto('reuniones', ${realIdx}, 'prioridad', 0); renderAll();" title="Muy Importante"
                                    style="width: 32px; height: 32px; border-radius: 50%; border: 3px solid ${item.prioridad === 0 ? '#be185d' : '#e2e8f0'}; background: ${item.prioridad === 0 ? '#fce7f3' : 'white'}; color: ${item.prioridad === 0 ? '#be185d' : '#94a3b8'}; cursor: pointer; padding: 0; font-size: 14px; font-weight: 700; display: flex; align-items: center; justify-content: center;">
                                    0
                                </button>
                                <button onclick="updateTexto('reuniones', ${realIdx}, 'prioridad', 1); renderAll();" title="Alta"
                                    style="width: 32px; height: 32px; border-radius: 50%; border: 3px solid ${item.prioridad === 1 ? '#166534' : '#e2e8f0'}; background: ${item.prioridad === 1 ? '#dcfce7' : 'white'}; color: ${item.prioridad === 1 ? '#166534' : '#94a3b8'}; cursor: pointer; padding: 0; font-size: 14px; font-weight: 700; display: flex; align-items: center; justify-content: center;">
                                    1
                                </button>
                                <button onclick="updateTexto('reuniones', ${realIdx}, 'prioridad', 2); renderAll();" title="Media"
                                    style="width: 32px; height: 32px; border-radius: 50%; border: 3px solid ${item.prioridad === 2 ? '#92400e' : '#e2e8f0'}; background: ${item.prioridad === 2 ? '#fef3c7' : 'white'}; color: ${item.prioridad === 2 ? '#92400e' : '#94a3b8'}; cursor: pointer; padding: 0; font-size: 14px; font-weight: 700; display: flex; align-items: center; justify-content: center;">
                                    2
                                </button>
                                <button onclick="updateTexto('reuniones', ${realIdx}, 'prioridad', 3); renderAll();" title="Baja"
                                    style="width: 32px; height: 32px; border-radius: 50%; border: 3px solid ${item.prioridad === 3 ? '#c2410c' : '#e2e8f0'}; background: ${item.prioridad === 3 ? '#ffedd5' : 'white'}; color: ${item.prioridad === 3 ? '#c2410c' : '#94a3b8'}; cursor: pointer; padding: 0; font-size: 14px; font-weight: 700; display: flex; align-items: center; justify-content: center;">
                                    3
                                </button>
                            </div>
                            <button onclick="deleteReunion(${realIdx})" style="background: #ef4444; color: white; border: none; padding: 4px 12px; border-radius: 6px; font-size: 11px; font-weight: 600; cursor: pointer;">
                                🗑️
                            </button>
                        </div>
                        <div class="item-meta" id="meta-reuniones-${realIdx}">
                            <span>👤 ${item.person}</span>
                            <span>📦 ${item.product}</span>
                        </div>
                    </div>
                    <div class="item-body">
                        <div class="form-group">
                            <label>🏢 Datos de la Empresa</label>
                            <div style="display: grid; gap: 8px;">
                                <input type="text" value="${item.company}" 
                                    onchange="updateTextoConTitulo('reuniones', ${realIdx}, 'company', this.value)"
                                    placeholder="Nombre empresa" style="font-weight: 600;">
                                <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 8px;">
                                    <input type="text" value="${item.person}" 
                                        onchange="updateTexto('reuniones', ${realIdx}, 'person', this.value)"
                                        placeholder="Persona contacto">
                                    <input type="text" value="${item.product}" 
                                        onchange="updateTextoConTitulo('reuniones', ${realIdx}, 'product', this.value)"
                                        placeholder="Producto">
                                    <select onchange="updateTexto('reuniones', ${realIdx}, 'departamento', this.value)" style="padding: 8px; border: 2px solid #e2e8f0; border-radius: 8px; font-size: 13px;">
                                        <option value="Lizarte" ${(item.departamento || 'Lizarte') === 'Lizarte' ? 'selected' : ''}>🔵 Lizarte</option>
                                        <option value="Innovación" ${item.departamento === 'Innovación' ? 'selected' : ''}>⭐ Innovación</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label>📝 Notas / Comentarios</label>
                            <div style="margin-bottom: 8px; display: flex; gap: 8px; flex-wrap: wrap;">
                                <button class="btn-formato" 
                                    onclick="aplicarFormatoNotas('reuniones', ${realIdx}, 'comments', 'bold')"
                                    title="Negrita">
                                    <strong>B</strong>
                                </button>
                                <input type="color" 
                                    id="color-picker-comments-${realIdx}"
                                    value="#000000"
                                    style="width: 40px; height: 32px; border: 1px solid #d1d5db; border-radius: 6px; cursor: pointer;"
                                    onchange="aplicarFormatoNotas('reuniones', ${realIdx}, 'comments', 'color', this.value)"
                                    title="Color del texto">
                                <button class="btn-formato" 
                                    onclick="limpiarFormatoNotas('reuniones', ${realIdx}, 'comments')"
                                    title="Limpiar formato">
                                    🧹 Limpiar
                                </button>
                            </div>
                            <div 
                                id="notas-editor-comments-${realIdx}"
                                contenteditable="true"
                                class="notas-editor"
                                oninput="updateTextoFormateado('reuniones', ${realIdx}, 'comments', this.innerHTML)"
                                onblur="updateTextoFormateado('reuniones', ${realIdx}, 'comments', this.innerHTML)"
                                placeholder="Añade notas o comentarios sobre esta reunión..."
                                style="min-height: 80px; padding: 10px; border: 1px solid #d1d5db; border-radius: 6px; background: white; font-size: 14px; line-height: 1.5; white-space: pre-wrap; word-wrap: break-word;">${item.comments || ''}</div>
                        </div>
                        
                        <div class="fotos-section">
                            <div class="fotos-section-title">📷 Fotos (${allFotos.length})</div>
                            <input type="file" accept="image/*" multiple onchange="addFotos('reuniones', ${realIdx}, this.files)" style="display: block; font-size: 11px; padding: 4px 8px; border: 1.5px solid #e2e8f0; border-radius: 6px; width: auto; margin-top: 8px; margin-bottom: 8px;">
                            ${allFotos.length > 0 ? `
                                <div class="fotos-grid">
                                    ${allFotos.map((foto, fIdx) => `
                                        <div class="foto-item">
                                            <img src="${foto}" class="foto-thumb" onclick="openModal('${foto}')" alt="Foto">
                                            <button class="foto-delete" onclick="deleteFoto('reuniones', ${realIdx}, ${fIdx})">×</button>
                                        </div>
                                    `).join('')}
                                </div>
                            ` : '<p style="font-size: 12px; color: #9ca3af;">Sin fotos</p>'}
                        </div>
                        
                        ${renderSeguimiento('reuniones', realIdx, item)}
                    </div>
                </div>
            `}).join('');
        }
        
        function renderAdicional() {
            const container = document.getElementById('adicionalContainer');
            console.log('🎨 Renderizando adicional - Total en appData:', appData.adicional.length);
            const filtered = applyFiltersToData(appData.adicional);
            console.log('🎨 Adicional después de filtros:', filtered.length);
            
            container.innerHTML = filtered.map((item, idx) => {
                const realIdx = appData.adicional.indexOf(item);
                const allFotos = [...(item.fotos || []), ...(item.fotos_extra || [])];
                
                return `
                <div class="item-card ${item.finalizado ? 'finalizado' : ''}">
                    <div class="item-header" style="position: relative;">
                        <div class="item-company" id="company-title-adicional-${realIdx}">
                            ${item.empresa}
                            <span class="depto-badge depto-${item.departamento?.toLowerCase() || 'lizarte'}">${item.departamento || 'Lizarte'}</span>
                        </div>
                        <div style="position: absolute; top: 10px; right: 10px; display: flex; gap: 6px; align-items: center;">
                            <div style="display: flex; gap: 4px;">
                                <button onclick="updateTexto('adicional', ${realIdx}, 'prioridad', 0); renderAll();" title="Muy Importante"
                                    style="width: 32px; height: 32px; border-radius: 50%; border: 3px solid ${item.prioridad === 0 ? '#be185d' : '#e2e8f0'}; background: ${item.prioridad === 0 ? '#fce7f3' : 'white'}; color: ${item.prioridad === 0 ? '#be185d' : '#94a3b8'}; cursor: pointer; padding: 0; font-size: 14px; font-weight: 700; display: flex; align-items: center; justify-content: center;">
                                    0
                                </button>
                                <button onclick="updateTexto('adicional', ${realIdx}, 'prioridad', 1); renderAll();" title="Alta"
                                    style="width: 32px; height: 32px; border-radius: 50%; border: 3px solid ${item.prioridad === 1 ? '#166534' : '#e2e8f0'}; background: ${item.prioridad === 1 ? '#dcfce7' : 'white'}; color: ${item.prioridad === 1 ? '#166534' : '#94a3b8'}; cursor: pointer; padding: 0; font-size: 14px; font-weight: 700; display: flex; align-items: center; justify-content: center;">
                                    1
                                </button>
                                <button onclick="updateTexto('adicional', ${realIdx}, 'prioridad', 2); renderAll();" title="Media"
                                    style="width: 32px; height: 32px; border-radius: 50%; border: 3px solid ${item.prioridad === 2 ? '#92400e' : '#e2e8f0'}; background: ${item.prioridad === 2 ? '#fef3c7' : 'white'}; color: ${item.prioridad === 2 ? '#92400e' : '#94a3b8'}; cursor: pointer; padding: 0; font-size: 14px; font-weight: 700; display: flex; align-items: center; justify-content: center;">
                                    2
                                </button>
                                <button onclick="updateTexto('adicional', ${realIdx}, 'prioridad', 3); renderAll();" title="Baja"
                                    style="width: 32px; height: 32px; border-radius: 50%; border: 3px solid ${item.prioridad === 3 ? '#c2410c' : '#e2e8f0'}; background: ${item.prioridad === 3 ? '#ffedd5' : 'white'}; color: ${item.prioridad === 3 ? '#c2410c' : '#94a3b8'}; cursor: pointer; padding: 0; font-size: 14px; font-weight: 700; display: flex; align-items: center; justify-content: center;">
                                    3
                                </button>
                            </div>
                            <button onclick="deleteAdicional(${realIdx})" style="background: #ef4444; color: white; border: none; padding: 4px 12px; border-radius: 6px; font-size: 11px; font-weight: 600; cursor: pointer;">
                                🗑️
                            </button>
                        </div>
                        <div class="item-meta" id="meta-adicional-${realIdx}">
                            <span>📦 ${item.producto}</span>
                        </div>
                    </div>
                    <div class="item-body">
                        <div class="form-group">
                            <label>🏢 Información Básica</label>
                            <div style="display: grid; gap: 8px;">
                                <input type="text" value="${item.empresa}" 
                                    onchange="updateTextoConTitulo('adicional', ${realIdx}, 'company', this.value)"
                                    placeholder="Nombre empresa" style="font-weight: 600;">
                                <div style="display: grid; grid-template-columns: 2fr 1fr; gap: 8px;">
                                    <input type="text" value="${item.producto}" 
                                        onchange="updateTextoConTitulo('adicional', ${realIdx}, 'producto', this.value)"
                                        placeholder="Producto / Servicio">
                                    <select onchange="updateTexto('adicional', ${realIdx}, 'departamento', this.value)" style="padding: 8px; border: 2px solid #e2e8f0; border-radius: 8px; font-size: 13px;">
                                        <option value="Lizarte" ${(item.departamento || 'Lizarte') === 'Lizarte' ? 'selected' : ''}>🔵 Lizarte</option>
                                        <option value="Innovación" ${item.departamento === 'Innovación' ? 'selected' : ''}>⭐ Innovación</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label>📝 Notas</label>
                            <div style="margin-bottom: 8px; display: flex; gap: 8px; flex-wrap: wrap;">
                                <button class="btn-formato" 
                                    onclick="aplicarFormatoNotas('adicional', ${realIdx}, 'notas', 'bold')"
                                    title="Negrita">
                                    <strong>B</strong>
                                </button>
                                <input type="color" 
                                    id="color-picker-notas-${realIdx}"
                                    value="#000000"
                                    style="width: 40px; height: 32px; border: 1px solid #d1d5db; border-radius: 6px; cursor: pointer;"
                                    onchange="aplicarFormatoNotas('adicional', ${realIdx}, 'notas', 'color', this.value)"
                                    title="Color del texto">
                                <button class="btn-formato" 
                                    onclick="limpiarFormatoNotas('adicional', ${realIdx}, 'notas')"
                                    title="Limpiar formato">
                                    🧹 Limpiar
                                </button>
                            </div>
                            <div 
                                id="notas-editor-notas-${realIdx}"
                                contenteditable="true"
                                class="notas-editor"
                                oninput="updateTextoFormateado('adicional', ${realIdx}, 'notas', this.innerHTML)"
                                onblur="updateTextoFormateado('adicional', ${realIdx}, 'notas', this.innerHTML)"
                                placeholder="Añade notas sobre esta empresa..."
                                style="min-height: 60px; padding: 10px; border: 1px solid #d1d5db; border-radius: 6px; background: white; font-size: 14px; line-height: 1.5; white-space: pre-wrap; word-wrap: break-word;">${item.notas || ''}</div>
                        </div>
                        
                        <div class="form-group">
                            <label>💡 Oportunidad</label>
                            <textarea 
                                class="auto-resize-textarea"
                                onchange="updateTexto('adicional', ${realIdx}, 'oportunidad', this.value)"
                                placeholder="Describe la oportunidad de negocio..."
                                style="min-height: 60px;">${item.oportunidad || ''}</textarea>
                        </div>
                        
                        ${allFotos.length > 0 ? `
                            <div class="fotos-section">
                                <div class="fotos-section-title">📷 Fotos (${allFotos.length})</div>
                                <input type="file" accept="image/*" multiple onchange="addFotos('adicional', ${realIdx}, this.files)" 
                                    style="display: block; font-size: 11px; padding: 4px 8px; border: 1.5px solid #e2e8f0; border-radius: 6px; width: auto; margin-top: 8px; margin-bottom: 8px;">
                                <div class="fotos-grid">
                                    ${allFotos.map((foto, fIdx) => `
                                        <div class="foto-item">
                                            <img src="${foto}" class="foto-thumb" onclick="openModal('${foto}')" alt="Foto">
                                            <button class="foto-delete" onclick="deleteFoto('adicional', ${realIdx}, ${fIdx})">×</button>
                                        </div>
                                    `).join('')}
                                </div>
                            </div>
                        ` : `
                            <div class="fotos-section">
                                <div class="fotos-section-title">📷 Fotos (0)</div>
                                <input type="file" accept="image/*" multiple onchange="addFotos('adicional', ${realIdx}, this.files)" 
                                    style="display: block; font-size: 11px; padding: 4px 8px; border: 1.5px solid #e2e8f0; border-radius: 6px; width: auto; margin-top: 8px; margin-bottom: 8px;">
                                <p style="font-size: 12px; color: #9ca3af; margin-bottom: 8px;">Sin fotos</p>
                            </div>
                        `}
                        
                        ${renderSeguimiento('adicional', realIdx, item)}
                    </div>
                </div>
            `}).join('');
        }
        
        function renderNuevosCoches() {
            if (!appData) {
                console.warn('⚠️ appData no está inicializado en renderNuevosCoches');
                return;
            }
            const container = document.getElementById('nuevosCochesContainer');
            if (!container) {
                console.warn('⚠️ No se encontró el contenedor nuevosCochesContainer');
                return;
            }
            if (!appData.nuevosCoches) appData.nuevosCoches = [];
            
            console.log('🎨 Renderizando nuevos coches - Total:', appData.nuevosCoches.length);
            
            if (appData.nuevosCoches.length === 0) {
                container.innerHTML = '<div style="text-align: center; padding: 40px; color: #9ca3af; background: white; border-radius: 12px;"><p>No hay coches registrados. Haz clic en "➕ Añadir Nuevo Coche" para comenzar.</p></div>';
                return;
            }
            
            container.innerHTML = appData.nuevosCoches.map((item, idx) => {
                return `
                <div class="item-card">
                    <div class="item-header" style="position: relative;">
                        <div class="item-company">
                            ${escapeHtml(item.nombre || 'Sin nombre')}
                        </div>
                        <div style="position: absolute; top: 10px; right: 10px;">
                            <button onclick="deleteNuevoCoche(${idx})" style="background: #ef4444; color: white; border: none; padding: 4px 12px; border-radius: 6px; font-size: 11px; font-weight: 600; cursor: pointer;">
                                🗑️
                            </button>
                        </div>
                    </div>
                    <div class="item-body">
                        <div class="form-group">
                            <label>🚗 Nombre del Coche</label>
                            <input type="text" value="${escapeHtml(item.nombre || '')}" 
                                onchange="updateNuevoCoche(${idx}, 'nombre', this.value)"
                                placeholder="Nombre del coche" style="font-weight: 600;">
                        </div>
                        <div class="form-group">
                            <label>📝 Descripción</label>
                            <textarea 
                                class="auto-resize-textarea"
                                onchange="updateNuevoCoche(${idx}, 'descripcion', this.value)"
                                placeholder="Añade una descripción del coche..."
                                style="min-height: 100px;">${escapeHtml(item.descripcion || '')}</textarea>
                        </div>
                    </div>
                </div>
            `}).join('');
        }
        
        function escapeHtml(text) {
            if (!text) return '';
            return String(text)
                .replace(/&/g, '&amp;')
                .replace(/</g, '&lt;')
                .replace(/>/g, '&gt;')
                .replace(/"/g, '&quot;')
                .replace(/'/g, '&#039;');
        }
        
        function formatearMoneda(valor) {
            return new Intl.NumberFormat('es-ES', {style: 'currency', currency: 'EUR'}).format(valor);
        }
        
        function formatearMonedaUSD(valor) {
            return new Intl.NumberFormat('en-US', {style: 'currency', currency: 'USD'}).format(valor);
        }
        
        // Función para obtener la tasa de cambio USD/EUR desde API
        async function obtenerTasaCambioUSD() {
            try {
                console.log('🔄 Obteniendo tasa de cambio USD/EUR...');
                const response = await fetch('https://api.exchangerate-api.com/v4/latest/USD');
                if (!response.ok) {
                    throw new Error('Error al obtener tasa de cambio');
                }
                const data = await response.json();
                const tasaEUR = data.rates.EUR;
                console.log('✅ Tasa de cambio obtenida:', tasaEUR, 'EUR por 1 USD');
                return tasaEUR;
            } catch (error) {
                console.error('❌ Error al obtener tasa de cambio:', error);
                // Fallback a tasa aproximada si falla la API
                console.warn('⚠️ Usando tasa de cambio de respaldo: 0.92');
                return 0.92;
            }
        }
        
        // Función para convertir y actualizar valores en EUR
        async function convertirAhorroAEUR(index) {
            if (!appData.ahorros || !appData.ahorros[index]) return;
            
            const item = appData.ahorros[index];
            const moneda = item.moneda || 'EUR';
            
            // Si ya está en EUR, los valores EUR son iguales a los originales
            if (moneda === 'EUR') {
                item.precioActualEUR = parseFloat(item.precioActual || 0);
                item.precioNuevoEUR = parseFloat(item.precioNuevo || 0);
                item.tasaCambio = 1;
                return;
            }
            
            // Si está en USD, obtener tasa de cambio y convertir
            if (moneda === 'USD') {
                const tasaCambio = await obtenerTasaCambioUSD();
                item.tasaCambio = tasaCambio;
                item.precioActualEUR = parseFloat(item.precioActual || 0) * tasaCambio;
                item.precioNuevoEUR = parseFloat(item.precioNuevo || 0) * tasaCambio;
                console.log(`💱 Convertido a EUR (tasa: ${tasaCambio}):`, {
                    precioActual: item.precioActual,
                    precioActualEUR: item.precioActualEUR,
                    precioNuevo: item.precioNuevo,
                    precioNuevoEUR: item.precioNuevoEUR
                });
            }
        }
        
        function renderAhorros() {
            if (!appData) {
                console.warn('⚠️ appData no está inicializado');
                return;
            }
            const container = document.getElementById('ahorrosContainer');
            if (!container) {
                console.warn('⚠️ No se encontró el contenedor ahorrosContainer');
                return;
            }
            if (!appData.ahorros) appData.ahorros = [];
            
            console.log('🎨 Renderizando ahorros - Total:', appData.ahorros.length);
            
            // Calcular suma total de todos los ahorros en EUR
            let sumaTotalAhorros = 0;
            appData.ahorros.forEach(item => {
                // Usar valores en EUR si existen, sino usar valores originales (asumiendo EUR)
                const precioActualEUR = item.precioActualEUR !== undefined ? item.precioActualEUR : parseFloat(item.precioActual || 0);
                const precioNuevoEUR = item.precioNuevoEUR !== undefined ? item.precioNuevoEUR : parseFloat(item.precioNuevo || 0);
                const unidadesAno = parseFloat(item.unidadesAno || 0);
                const ahorroUnitarioEUR = precioActualEUR - precioNuevoEUR;
                const ahorroTotal = ahorroUnitarioEUR * unidadesAno;
                sumaTotalAhorros += ahorroTotal;
            });
            
            const sumaFormateada = formatearMoneda(sumaTotalAhorros);
            
            if (appData.ahorros.length === 0) {
                container.innerHTML = '<div style="text-align: center; padding: 40px; color: #9ca3af; background: white; border-radius: 12px;"><p>No hay ahorros registrados. Haz clic en "➕ Añadir Ahorro" para comenzar.</p></div>';
                return;
            }
            
            // Crear HTML con el resumen total y las empresas
            let html = `
                <div style="background: linear-gradient(135deg, #10b981 0%, #059669 100%); color: white; padding: 30px; border-radius: 16px; margin-bottom: 25px; box-shadow: 0 8px 24px rgba(16, 185, 129, 0.3); text-align: center;">
                    <div style="font-size: 16px; font-weight: 700; margin-bottom: 12px; opacity: 0.95; text-transform: uppercase; letter-spacing: 1.5px;">💰 TOTAL AHORROS CONSEGUIDOS</div>
                    <div style="font-size: 56px; font-weight: 900; margin: 15px 0; text-shadow: 0 4px 12px rgba(0, 0, 0, 0.3); line-height: 1.2;">${sumaFormateada}</div>
                    <div style="font-size: 14px; opacity: 0.9; margin-top: 8px; font-weight: 500;">${appData.ahorros.length} ${appData.ahorros.length === 1 ? 'ahorro registrado' : 'ahorros registrados'}</div>
                </div>
            `;
            
            html += appData.ahorros.map((item, idx) => {
                const moneda = item.moneda || 'EUR';
                const precioActual = parseFloat(item.precioActual || 0);
                const precioNuevo = parseFloat(item.precioNuevo || 0);
                const precioActualEUR = item.precioActualEUR !== undefined ? item.precioActualEUR : precioActual;
                const precioNuevoEUR = item.precioNuevoEUR !== undefined ? item.precioNuevoEUR : precioNuevo;
                const unidadesAno = parseFloat(item.unidadesAno || 0);
                const ahorroUnitarioEUR = precioActualEUR - precioNuevoEUR;
                const ahorroTotal = ahorroUnitarioEUR * unidadesAno;
                const ahorroTotalFormateado = formatearMoneda(ahorroTotal);
                const ahorroUnitarioFormateado = formatearMoneda(ahorroUnitarioEUR);
                const unidadesFormateadas = unidadesAno.toLocaleString('es-ES');
                
                // Formatear valores originales si es USD
                const precioActualOriginalFormateado = moneda === 'USD' ? formatearMonedaUSD(precioActual) : formatearMoneda(precioActual);
                const precioNuevoOriginalFormateado = moneda === 'USD' ? formatearMonedaUSD(precioNuevo) : formatearMoneda(precioNuevo);
                const precioActualEURFormateado = formatearMoneda(precioActualEUR);
                const precioNuevoEURFormateado = formatearMoneda(precioNuevoEUR);
                const tasaCambio = item.tasaCambio || 1;
                
                return `
                <div class="item-card">
                    <div class="item-header" style="position: relative;">
                        <div class="item-company">
                            ${escapeHtml(item.empresa || 'Sin empresa')}
                        </div>
                        <div style="position: absolute; top: 10px; right: 10px;">
                            <button onclick="deleteAhorro(${idx})" style="background: #ef4444; color: white; border: none; padding: 4px 12px; border-radius: 6px; font-size: 11px; font-weight: 600; cursor: pointer;">
                                🗑️
                            </button>
                        </div>
                        <div class="item-meta">
                            <span>💰 Ahorro Total: ${ahorroTotalFormateado}</span>
                            ${moneda === 'USD' ? `<span style="margin-left: 10px; font-size: 11px; opacity: 0.8;">(${formatearMonedaUSD((precioActual - precioNuevo) * unidadesAno)})</span>` : ''}
                        </div>
                    </div>
                    <div class="item-body">
                        <div class="form-group">
                            <label>🏢 Nombre de Empresa</label>
                            <input type="text" value="${escapeHtml(item.empresa || '')}" 
                                onchange="updateAhorro(${idx}, 'empresa', this.value)"
                                placeholder="Nombre de la empresa" style="font-weight: 600;">
                        </div>
                        <div class="form-group">
                            <label>📦 Producto</label>
                            <input type="text" value="${escapeHtml(item.producto || '')}" 
                                onchange="updateAhorro(${idx}, 'producto', this.value)"
                                placeholder="Producto">
                        </div>
                        <div class="form-group">
                            <label>💱 Moneda</label>
                            <select onchange="updateAhorro(${idx}, 'moneda', this.value)" style="width: 100%; padding: 10px; border: 1px solid #d1d5db; border-radius: 6px; font-size: 14px;">
                                <option value="EUR" ${moneda === 'EUR' ? 'selected' : ''}>EUR (Euro)</option>
                                <option value="USD" ${moneda === 'USD' ? 'selected' : ''}>USD (Dólar)</option>
                            </select>
                        </div>
                        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px;">
                            <div class="form-group">
                                <label>💵 Precio Actual ${moneda === 'USD' ? '(USD)' : '(EUR)'}</label>
                                <input type="number" step="0.01" value="${item.precioActual || ''}" 
                                    onchange="updateAhorro(${idx}, 'precioActual', this.value)"
                                    placeholder="0.00">
                                ${moneda === 'USD' && precioActual > 0 ? `
                                    <div style="font-size: 11px; color: #6b7280; margin-top: 4px;">
                                        ≈ ${precioActualEURFormateado} EUR (tasa: ${tasaCambio.toFixed(4)})
                                    </div>
                                ` : ''}
                            </div>
                            <div class="form-group">
                                <label>💵 Precio Nuevo ${moneda === 'USD' ? '(USD)' : '(EUR)'}</label>
                                <input type="number" step="0.01" value="${item.precioNuevo || ''}" 
                                    onchange="updateAhorro(${idx}, 'precioNuevo', this.value)"
                                    placeholder="0.00">
                                ${moneda === 'USD' && precioNuevo > 0 ? `
                                    <div style="font-size: 11px; color: #6b7280; margin-top: 4px;">
                                        ≈ ${precioNuevoEURFormateado} EUR (tasa: ${tasaCambio.toFixed(4)})
                                    </div>
                                ` : ''}
                            </div>
                        </div>
                        <div class="form-group">
                            <label>📊 Unidades/Año</label>
                            <input type="number" step="1" value="${item.unidadesAno || ''}" 
                                onchange="updateAhorro(${idx}, 'unidadesAno', this.value)"
                                placeholder="0">
                        </div>
                        <div class="form-group" style="background: #f0fdf4; padding: 12px; border-radius: 8px; border: 2px solid #10b981;">
                            <label style="color: #166534; font-weight: 700;">💰 Ahorro Total Calculado (EUR)</label>
                            <div style="font-size: 24px; font-weight: 700; color: #166534; margin-top: 8px;">
                                ${ahorroTotalFormateado}
                            </div>
                            ${moneda === 'USD' && ahorroTotal > 0 ? `
                                <div style="font-size: 12px; color: #059669; margin-top: 4px;">
                                    Original: ${formatearMonedaUSD((precioActual - precioNuevo) * unidadesAno)} USD
                                </div>
                            ` : ''}
                            <div style="font-size: 12px; color: #059669; margin-top: 4px;">
                                Ahorro unitario: ${ahorroUnitarioFormateado} × ${unidadesFormateadas} unidades
                            </div>
                        </div>
                    </div>
                </div>
            `}).join('');
            
            container.innerHTML = html;
        }
        
        function renderSeguimiento(type, index, item) {
            const seg = item.seguimiento;
            const id = item.id || index;
            
            return `
                <div class="seguimiento-box">
                    <div class="seguimiento-title">📋 Seguimiento</div>
                    
                    <div class="form-group">
                        <label>Estado</label>
                        <div class="estado-selector">
                            <div class="estado-option estado-pendiente">
                                <input type="radio" id="estado_${type}_${id}_pendiente" name="estado_${type}_${id}" value="pendiente" 
                                    ${seg.estado === 'pendiente' ? 'checked' : ''}
                                    onchange="updateEstado('${type}', ${index}, 'pendiente')">
                                <label for="estado_${type}_${id}_pendiente">⚪ Pendiente</label>
                            </div>
                            <div class="estado-option estado-contactado">
                                <input type="radio" id="estado_${type}_${id}_contactado" name="estado_${type}_${id}" value="contactado"
                                    ${seg.estado === 'contactado' ? 'checked' : ''}
                                    onchange="updateEstado('${type}', ${index}, 'contactado')">
                                <label for="estado_${type}_${id}_contactado">🟡 Contactado</label>
                            </div>
                            <div class="estado-option estado-proceso">
                                <input type="radio" id="estado_${type}_${id}_proceso" name="estado_${type}_${id}" value="proceso"
                                    ${seg.estado === 'proceso' ? 'checked' : ''}
                                    onchange="updateEstado('${type}', ${index}, 'proceso')">
                                <label for="estado_${type}_${id}_proceso">🔵 En Proceso</label>
                            </div>
                            <div class="estado-option estado-finalizado">
                                <input type="radio" id="estado_${type}_${id}_finalizado" name="estado_${type}_${id}" value="finalizado"
                                    ${seg.estado === 'finalizado' ? 'checked' : ''}
                                    onchange="updateEstado('${type}', ${index}, 'finalizado')">
                                <label for="estado_${type}_${id}_finalizado">🟢 Finalizado</label>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group" style="margin: 0;">
                            <label>Responsable</label>
                            <select onchange="updateSeguimiento('${type}', ${index}, 'responsable', this.value)">
                                <option value="">Sin asignar</option>
                                ${equipoLizarte.map(nombre => `
                                    <option value="${nombre}" ${seg.responsable === nombre ? 'selected' : ''}>${nombre}</option>
                                `).join('')}
                            </select>
                        </div>
                        <div class="form-group" style="margin: 0;">
                            <label>Email</label>
                            <input type="email" value="${seg.email || ''}" 
                                onchange="updateSeguimiento('${type}', ${index}, 'email', this.value)"
                                placeholder="email@ejemplo.com">
                        </div>
                    </div>
                    
                    ${seg.email ? `
                        <button class="btn-notify" onclick="sendNotification('${type}', ${index})">
                            📧 Enviar Notificación
                        </button>
                    ` : ''}
                    
                    <div class="form-group">
                        <label>Próximas Acciones</label>
                        <div class="acciones-list">
                            ${seg.acciones && seg.acciones.length > 0 ? seg.acciones.map((accion, aIdx) => `
                                <div class="accion-item">
                                    <textarea onchange="updateAccion('${type}', ${index}, ${aIdx}, this.value)"
                                        placeholder="Descripción de la acción...">${accion}</textarea>
                                    <button class="btn-delete-accion" onclick="deleteAccion('${type}', ${index}, ${aIdx})">🗑️</button>
                                </div>
                            `).join('') : '<p style="font-size: 12px; color: #9ca3af; margin-bottom: 8px;">Sin acciones definidas</p>'}
                        </div>
                        <button class="btn-add-accion" onclick="addAccion('${type}', ${index})">➕ Añadir Acción</button>
                    </div>
                    
                    <div class="form-group" style="margin-top: 20px;">
                        <label>💬 Respuestas</label>
                        <div id="respuestas-list-${type}-${index}">
                            ${item.respuestas && item.respuestas.length > 0 ? item.respuestas.map((respuesta, rIdx) => {
                                const texto = typeof respuesta === 'string' ? respuesta : (respuesta.texto || '');
                                const formato = typeof respuesta === 'object' ? (respuesta.formato || {}) : {};
                                const tieneNegrita = formato.negrita || false;
                                const tieneLista = formato.lista || false;
                                return `
                                <div class="respuesta-item">
                                    <textarea id="respuesta-textarea-${type}-${index}-${rIdx}" 
                                        oninput="autoResizeTextarea(this); updateRespuesta('${type}', ${index}, ${rIdx}, this.value)"
                                        placeholder="Escribe tu respuesta aquí...">${escapeHtml(texto)}</textarea>
                                    <div class="respuesta-controls">
                                        <button class="btn-formato ${tieneNegrita ? 'active' : ''}" 
                                            onclick="toggleFormatoRespuesta('${type}', ${index}, ${rIdx}, 'negrita')"
                                            title="Negrita">
                                            <strong>B</strong>
                                        </button>
                                        <button class="btn-formato ${tieneLista ? 'active' : ''}" 
                                            onclick="toggleFormatoRespuesta('${type}', ${index}, ${rIdx}, 'lista')"
                                            title="Lista">
                                            • Lista
                                        </button>
                                        <button class="btn-delete-respuesta" onclick="deleteRespuesta('${type}', ${index}, ${rIdx})">🗑️ Eliminar</button>
                                    </div>
                                </div>
                            `;
                            }).join('') : '<p style="font-size: 12px; color: #9ca3af; margin-bottom: 8px;">Sin respuestas registradas</p>'}
                        </div>
                        <button class="btn-add-respuesta" onclick="addRespuesta('${type}', ${index})">➕ Añadir Respuesta</button>
                    </div>
                    
                    <div class="conclusion-final-section">
                        <h3>📝 Conclusión Final</h3>
                        <textarea id="conclusion-textarea-${type}-${index}" 
                            oninput="autoResizeTextarea(this); updateConclusionFinal('${type}', ${index}, this.value)"
                            placeholder="Escribe la conclusión final y decisión sobre esta empresa...">${escapeHtml(item.conclusionFinal || '')}</textarea>
                        <div class="conclusion-controls">
                            <button class="btn-formato" 
                                onclick="toggleFormatoConclusion('${type}', ${index}, 'negrita')"
                                title="Negrita">
                                <strong>B</strong>
                            </button>
                            <button class="btn-formato" 
                                onclick="toggleFormatoConclusion('${type}', ${index}, 'lista')"
                                title="Lista">
                                • Lista
                            </button>
                            <button class="btn-finalizado ${item.finalizado ? 'finalizado' : ''}" 
                                onclick="toggleFinalizado('${type}', ${index})">
                                ${item.finalizado ? '✅ Finalizado' : '✓ Marcar como Finalizado'}
                            </button>
                        </div>
                    </div>
                </div>
            `;
        }
        
        function renderDocumentacion(type, index, item) {
            const docs = item.documentos || [];
            
            return `
                <div class="seguimiento-section" style="margin-top: 15px;">
                    <div class="seguimiento-title">📎 Documentación</div>
                    
                    <div class="form-group">
                        ${docs.length > 0 ? `
                            <div style="display: grid; gap: 8px; margin-bottom: 12px;">
                                ${docs.map((doc, dIdx) => `
                                    <div style="display: flex; align-items: center; gap: 8px; padding: 10px; background: #f9fafb; border-radius: 8px; border: 1px solid #e5e7eb;">
                                        <span style="flex: 1;">
                                            ${doc.tipo === 'link' ? '🔗' : '📄'} 
                                            ${doc.tipo === 'link' ? 
                                                `<a href="${doc.url}" target="_blank" style="color: #3b82f6; text-decoration: underline;">${doc.nombre}</a>` : 
                                                `<span>${doc.nombre}</span>`
                                            }
                                        </span>
                                        <button class="btn-delete-accion" onclick="deleteDocumento('${type}', ${index}, ${dIdx})" style="padding: 4px 8px;">🗑️</button>
                                    </div>
                                `).join('')}
                            </div>
                        ` : '<p style="font-size: 12px; color: #9ca3af; margin-bottom: 12px;">Sin documentos adjuntos</p>'}
                        
                        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 8px;">
                            <button class="btn-add-accion" onclick="addDocumentoLink('${type}', ${index})">🔗 Añadir Link Email</button>
                            <button class="btn-add-accion" onclick="addDocumentoArchivo('${type}', ${index})">📄 Subir Catálogo</button>
                        </div>
                    </div>
                </div>
            `;
        }
        
        function updateSeguimiento(type, index, field, value) {
            if (type === 'reuniones') {
                appData.reuniones[index].seguimiento[field] = value;
            } else {
                appData.adicional[index].seguimiento[field] = value;
            }
            
            // También actualizar en textos_modificados_automechanika para mantener consistencia
            const textosData = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            const itemId = item.id;
            
            if (type === 'reuniones') {
                if (!textosData[itemId]) textosData[itemId] = {};
                textosData[itemId].seguimiento = item.seguimiento;
                textosData[itemId].company = item.company || '';
                textosData[itemId].person = item.person || '';
                textosData[itemId].product = item.product || '';
                textosData[itemId].time = item.time || '';
                textosData[itemId].stand = item.stand || '';
                textosData[itemId].comments = item.comments || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
                textosData[itemId].prioridad = item.prioridad !== undefined ? item.prioridad : 1;
                textosData[itemId].fotos = item.fotos || [];
                textosData[itemId].fotos_extra = item.fotos_extra || [];
            } else {
                if (!textosData[itemId]) textosData[itemId] = {};
                textosData[itemId].seguimiento = item.seguimiento;
                textosData[itemId].empresa = item.empresa || '';
                textosData[itemId].producto = item.producto || '';
                textosData[itemId].notas = item.notas || '';
                textosData[itemId].oportunidad = item.oportunidad || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
                textosData[itemId].prioridad = item.prioridad !== undefined ? item.prioridad : 1;
                textosData[itemId].fotos = item.fotos || [];
                textosData[itemId].fotos_extra = item.fotos_extra || [];
            }
            
            localStorage.setItem('textos_modificados_automechanika', JSON.stringify(textosData));
            console.log('💾 Seguimiento actualizado:', field, '=', value, 'para', type, index);
            console.log('💾 Datos guardados en localStorage (textos_modificados_automechanika)');
            saveSeguimiento();
        }
        
        function updateTexto(type, index, field, value) {
            if (type === 'reuniones') {
                appData.reuniones[index][field] = value;
            } else {
                appData.adicional[index][field] = value;
            }
            
            // Guardar TODA la estructura completa del item en localStorage
            const textosData = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            const itemId = item.id;
            
            if (type === 'reuniones') {
                // Guardar estructura completa de reunión
                textosData[itemId] = {
                    company: item.company || '',
                    person: item.person || '',
                    product: item.product || '',
                    time: item.time || '',
                    stand: item.stand || '',
                    comments: item.comments || '',
                    departamento: item.departamento || 'Lizarte',
                    prioridad: item.prioridad !== undefined ? item.prioridad : 1,
                    fotos: item.fotos || [],
                    fotos_extra: item.fotos_extra || [],
                    seguimiento: item.seguimiento || {
                        responsable: "",
                        contactado: false,
                        respuestaRecibida: false,
                        proximaAccion: "",
                        fechaSeguimiento: "",
                        acciones: [],
                        estado: "pendiente",
                        email: ""
                    }
                };
            } else {
                // Guardar estructura completa de adicional
                textosData[itemId] = {
                    empresa: item.empresa || '',
                    producto: item.producto || '',
                    notas: item.notas || '',
                    oportunidad: item.oportunidad || '',
                    departamento: item.departamento || 'Lizarte',
                    prioridad: item.prioridad !== undefined ? item.prioridad : 1,
                    fotos: item.fotos || [],
                    fotos_extra: item.fotos_extra || [],
                    seguimiento: item.seguimiento || {
                        responsable: "",
                        contactado: false,
                        respuestaRecibida: false,
                        proximaAccion: "",
                        fechaSeguimiento: "",
                        acciones: [],
                        estado: "pendiente",
                        email: ""
                    }
                };
            }
            
            localStorage.setItem('textos_modificados_automechanika', JSON.stringify(textosData));
            console.log('💾 Campo actualizado:', field, '=', value, 'para', type, index);
            console.log('💾 Datos guardados en localStorage (textos_modificados_automechanika)');
            
            // También llamar a saveData() para mantener consistencia completa
            saveData();
            
            showSaveIndicator();
        }
        
        function updateTextoConTitulo(type, index, field, value) {
            // Mapear campo si es necesario (adicional usa 'empresa' en lugar de 'company')
            let actualField = field;
            if (type === 'adicional' && field === 'company') {
                actualField = 'empresa';
            }
            
            // Actualizar datos
            updateTexto(type, index, actualField, value);
            
            // Actualizar título en tiempo real
            if (field === 'company' && type === 'reuniones') {
                const titleElement = document.getElementById(`company-title-reuniones-${index}`);
                if (titleElement) {
                    const item = appData.reuniones[index];
                    const badge = titleElement.querySelector('.depto-badge');
                    const badgeHTML = badge ? badge.outerHTML : '';
                    titleElement.innerHTML = `${value || item.company} ${badgeHTML}`;
                }
            } else if (field === 'company' && type === 'adicional') {
                const titleElement = document.getElementById(`company-title-adicional-${index}`);
                if (titleElement) {
                    const item = appData.adicional[index];
                    const badge = titleElement.querySelector('.depto-badge');
                    const badgeHTML = badge ? badge.outerHTML : '';
                    titleElement.innerHTML = `${value || item.empresa} ${badgeHTML}`;
                }
            }
            
            // Actualizar metadata (persona y producto)
            if ((field === 'person' || field === 'product') && type === 'reuniones') {
                const metaElement = document.getElementById(`meta-reuniones-${index}`);
                if (metaElement) {
                    const item = appData.reuniones[index];
                    metaElement.innerHTML = `
                        <span>👤 ${item.person}</span>
                        <span>📦 ${item.product}</span>
                    `;
                }
            } else if (field === 'producto' && type === 'adicional') {
                const metaElement = document.getElementById(`meta-adicional-${index}`);
                if (metaElement) {
                    const item = appData.adicional[index];
                    metaElement.innerHTML = `
                        <span>📦 ${item.producto}</span>
                        <span class="priority-badge priority-${item.prioridad}">${getPrioridadTexto(item.prioridad)}</span>
                    `;
                }
            }
        }
        
        function updateEstado(type, index, estado) {
            updateSeguimiento(type, index, 'estado', estado);
            renderAll();
        }
        
        function addAccion(type, index) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            if (!item.seguimiento.acciones) item.seguimiento.acciones = [];
            item.seguimiento.acciones.push('');
            
            // Actualizar en textos_modificados_automechanika (actualizar seguimiento completo)
            const textosData = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
            const itemId = item.id;
            
            if (type === 'reuniones') {
                if (!textosData[itemId]) textosData[itemId] = {};
                textosData[itemId].seguimiento = item.seguimiento;
                textosData[itemId].company = item.company || '';
                textosData[itemId].person = item.person || '';
                textosData[itemId].product = item.product || '';
                textosData[itemId].time = item.time || '';
                textosData[itemId].stand = item.stand || '';
                textosData[itemId].comments = item.comments || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
                textosData[itemId].prioridad = item.prioridad !== undefined ? item.prioridad : 1;
                textosData[itemId].fotos = item.fotos || [];
                textosData[itemId].fotos_extra = item.fotos_extra || [];
            } else {
                if (!textosData[itemId]) textosData[itemId] = {};
                textosData[itemId].seguimiento = item.seguimiento;
                textosData[itemId].empresa = item.empresa || '';
                textosData[itemId].producto = item.producto || '';
                textosData[itemId].notas = item.notas || '';
                textosData[itemId].oportunidad = item.oportunidad || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
                textosData[itemId].prioridad = item.prioridad !== undefined ? item.prioridad : 1;
                textosData[itemId].fotos = item.fotos || [];
                textosData[itemId].fotos_extra = item.fotos_extra || [];
            }
            
            localStorage.setItem('textos_modificados_automechanika', JSON.stringify(textosData));
            saveSeguimiento();
            
            renderAll();
        }
        
        function updateAccion(type, index, accionIdx, value) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            item.seguimiento.acciones[accionIdx] = value;
            
            // Actualizar en textos_modificados_automechanika (actualizar seguimiento completo)
            const textosData = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
            const itemId = item.id;
            
            if (type === 'reuniones') {
                if (!textosData[itemId]) textosData[itemId] = {};
                textosData[itemId].seguimiento = item.seguimiento;
                textosData[itemId].company = item.company || '';
                textosData[itemId].person = item.person || '';
                textosData[itemId].product = item.product || '';
                textosData[itemId].time = item.time || '';
                textosData[itemId].stand = item.stand || '';
                textosData[itemId].comments = item.comments || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
                textosData[itemId].prioridad = item.prioridad !== undefined ? item.prioridad : 1;
                textosData[itemId].fotos = item.fotos || [];
                textosData[itemId].fotos_extra = item.fotos_extra || [];
            } else {
                if (!textosData[itemId]) textosData[itemId] = {};
                textosData[itemId].seguimiento = item.seguimiento;
                textosData[itemId].empresa = item.empresa || '';
                textosData[itemId].producto = item.producto || '';
                textosData[itemId].notas = item.notas || '';
                textosData[itemId].oportunidad = item.oportunidad || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
                textosData[itemId].prioridad = item.prioridad !== undefined ? item.prioridad : 1;
                textosData[itemId].fotos = item.fotos || [];
                textosData[itemId].fotos_extra = item.fotos_extra || [];
            }
            
            localStorage.setItem('textos_modificados_automechanika', JSON.stringify(textosData));
            saveSeguimiento();
        }
        
        function deleteAccion(type, index, accionIdx) {
            if (!confirm('¿Eliminar esta acción?')) return;
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            item.seguimiento.acciones.splice(accionIdx, 1);
            
            // Actualizar en textos_modificados_automechanika (actualizar seguimiento completo)
            const textosData = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
            const itemId = item.id;
            
            if (type === 'reuniones') {
                if (!textosData[itemId]) textosData[itemId] = {};
                textosData[itemId].seguimiento = item.seguimiento;
                textosData[itemId].company = item.company || '';
                textosData[itemId].person = item.person || '';
                textosData[itemId].product = item.product || '';
                textosData[itemId].time = item.time || '';
                textosData[itemId].stand = item.stand || '';
                textosData[itemId].comments = item.comments || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
                textosData[itemId].prioridad = item.prioridad !== undefined ? item.prioridad : 1;
                textosData[itemId].fotos = item.fotos || [];
                textosData[itemId].fotos_extra = item.fotos_extra || [];
            } else {
                if (!textosData[itemId]) textosData[itemId] = {};
                textosData[itemId].seguimiento = item.seguimiento;
                textosData[itemId].empresa = item.empresa || '';
                textosData[itemId].producto = item.producto || '';
                textosData[itemId].notas = item.notas || '';
                textosData[itemId].oportunidad = item.oportunidad || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
                textosData[itemId].prioridad = item.prioridad !== undefined ? item.prioridad : 1;
                textosData[itemId].fotos = item.fotos || [];
                textosData[itemId].fotos_extra = item.fotos_extra || [];
            }
            
            localStorage.setItem('textos_modificados_automechanika', JSON.stringify(textosData));
            saveSeguimiento();
            
            renderAll();
        }
        
        // Función auxiliar para guardar respuestas y conclusión final en localStorage
        function saveRespuestasYConclusion(type, index) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            if (!item) {
                console.error('❌ Error: item no encontrado en saveRespuestasYConclusion', type, index);
                return;
            }
            
            const textosData = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
            const itemId = item.id;
            
            if (type === 'reuniones') {
                if (!textosData[itemId]) textosData[itemId] = {};
                textosData[itemId].respuestas = item.respuestas || [];
                textosData[itemId].conclusionFinal = item.conclusionFinal || '';
                textosData[itemId].finalizado = item.finalizado || false;
                textosData[itemId].seguimiento = item.seguimiento;
                textosData[itemId].company = item.company || '';
                textosData[itemId].person = item.person || '';
                textosData[itemId].product = item.product || '';
                textosData[itemId].time = item.time || '';
                textosData[itemId].stand = item.stand || '';
                textosData[itemId].comments = item.comments || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
                textosData[itemId].prioridad = item.prioridad !== undefined ? item.prioridad : 1;
                textosData[itemId].fotos = item.fotos || [];
                textosData[itemId].fotos_extra = item.fotos_extra || [];
            } else {
                if (!textosData[itemId]) textosData[itemId] = {};
                textosData[itemId].respuestas = item.respuestas || [];
                textosData[itemId].conclusionFinal = item.conclusionFinal || '';
                textosData[itemId].finalizado = item.finalizado || false;
                textosData[itemId].seguimiento = item.seguimiento;
                textosData[itemId].empresa = item.empresa || '';
                textosData[itemId].producto = item.producto || '';
                textosData[itemId].notas = item.notas || '';
                textosData[itemId].oportunidad = item.oportunidad || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
                textosData[itemId].prioridad = item.prioridad !== undefined ? item.prioridad : 1;
                textosData[itemId].fotos = item.fotos || [];
                textosData[itemId].fotos_extra = item.fotos_extra || [];
            }
            
            localStorage.setItem('textos_modificados_automechanika', JSON.stringify(textosData));
            console.log('💾 Guardado respuestas y conclusión para', type, index, 'ID:', itemId, {
                respuestas: textosData[itemId].respuestas,
                conclusionFinal: textosData[itemId].conclusionFinal,
                finalizado: textosData[itemId].finalizado
            });
            saveData();
            showSaveIndicator();
        }
        
        function addRespuesta(type, index) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            if (!item.respuestas) item.respuestas = [];
            item.respuestas.push({ texto: '', formato: { negrita: false, lista: false } });
            
            saveRespuestasYConclusion(type, index);
            renderAll();
            
            // Scroll a la nueva respuesta después de renderizar
            setTimeout(() => {
                const textareaId = `respuesta-textarea-${type}-${index}-${item.respuestas.length - 1}`;
                const textarea = document.getElementById(textareaId);
                if (textarea) {
                    textarea.focus();
                    textarea.scrollIntoView({ behavior: 'smooth', block: 'center' });
                }
            }, 100);
        }
        
        function updateRespuesta(type, index, respIdx, value) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            if (!item.respuestas || !item.respuestas[respIdx]) return;
            
            if (typeof item.respuestas[respIdx] === 'string') {
                // Convertir string antiguo a objeto
                item.respuestas[respIdx] = { texto: value, formato: { negrita: false, lista: false } };
            } else {
                item.respuestas[respIdx].texto = value;
            }
            
            saveRespuestasYConclusion(type, index);
        }
        
        function deleteRespuesta(type, index, respIdx) {
            if (!confirm('¿Eliminar esta respuesta?')) return;
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            if (!item.respuestas) item.respuestas = [];
            item.respuestas.splice(respIdx, 1);
            
            saveRespuestasYConclusion(type, index);
            renderAll();
        }
        
        function toggleFormatoRespuesta(type, index, respIdx, formato) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            if (!item.respuestas || !item.respuestas[respIdx]) return;
            
            if (typeof item.respuestas[respIdx] === 'string') {
                // Convertir string antiguo a objeto
                item.respuestas[respIdx] = { 
                    texto: item.respuestas[respIdx], 
                    formato: { negrita: false, lista: false } 
                };
            }
            
            if (!item.respuestas[respIdx].formato) {
                item.respuestas[respIdx].formato = { negrita: false, lista: false };
            }
            
            item.respuestas[respIdx].formato[formato] = !item.respuestas[respIdx].formato[formato];
            
            saveRespuestasYConclusion(type, index);
            renderAll();
        }
        
        function updateConclusionFinal(type, index, value) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            item.conclusionFinal = value;
            
            saveRespuestasYConclusion(type, index);
        }
        
        function toggleFormatoConclusion(type, index, formato) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            const textareaId = `conclusion-textarea-${type}-${index}`;
            const textarea = document.getElementById(textareaId);
            
            if (!textarea) {
                console.error('❌ No se encontró el textarea de conclusión');
                return;
            }
            
            const texto = textarea.value || '';
            const inicio = textarea.selectionStart;
            const fin = textarea.selectionEnd;
            const textoSeleccionado = texto.substring(inicio, fin);
            
            if (formato === 'negrita') {
                // Aplicar negrita: **texto**
                if (textoSeleccionado) {
                    const textoAntes = texto.substring(0, inicio);
                    const textoDespues = texto.substring(fin);
                    item.conclusionFinal = textoAntes + '**' + textoSeleccionado + '**' + textoDespues;
                } else {
                    // Si no hay selección, añadir marcadores al final
                    item.conclusionFinal = texto + '****';
                }
                saveRespuestasYConclusion(type, index);
                renderAll();
                
                // Restaurar cursor después de renderizar
                setTimeout(() => {
                    const newTextarea = document.getElementById(textareaId);
                    if (newTextarea) {
                        if (textoSeleccionado) {
                            newTextarea.setSelectionRange(inicio + 2, fin + 2);
                        } else {
                            newTextarea.setSelectionRange(item.conclusionFinal.length - 2, item.conclusionFinal.length - 2);
                        }
                        newTextarea.focus();
                    }
                }, 50);
            } else if (formato === 'lista') {
                // Aplicar lista: añadir • al inicio de cada línea
                const lineas = texto.split('\n');
                const tieneLista = lineas.some(linea => linea.trim().startsWith('•'));
                
                if (tieneLista) {
                    // Quitar formato de lista
                    item.conclusionFinal = lineas.map(linea => linea.replace(/^•\s*/, '')).join('\n');
                } else {
                    // Añadir formato de lista
                    item.conclusionFinal = lineas.map(linea => linea.trim() ? '• ' + linea.trim() : '').join('\n');
                }
                
                saveRespuestasYConclusion(type, index);
                renderAll();
            }
        }
        
        function toggleFinalizado(type, index) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            item.finalizado = !item.finalizado;
            
            saveRespuestasYConclusion(type, index);
            renderAll();
        }
        
        // Funciones para formato de notas/comentarios
        function aplicarFormatoNotas(type, index, field, formato, color = null) {
            const editorId = `notas-editor-${field}-${index}`;
            const editor = document.getElementById(editorId);
            
            if (!editor) {
                console.error('❌ No se encontró el editor de notas');
                return;
            }
            
            // Guardar selección
            const selection = window.getSelection();
            const range = selection.rangeCount > 0 ? selection.getRangeAt(0) : null;
            
            if (!range || range.collapsed) {
                // Si no hay selección, mostrar mensaje
                if (formato === 'bold') {
                    alert('Selecciona el texto que quieres poner en negrita');
                } else if (formato === 'color') {
                    alert('Selecciona el texto al que quieres cambiar el color');
                }
                return;
            }
            
            // Enfocar el editor para que funcione execCommand
            editor.focus();
            
            if (formato === 'bold') {
                // Aplicar negrita
                document.execCommand('bold', false, null);
            } else if (formato === 'color' && color) {
                // Aplicar color
                document.execCommand('foreColor', false, color);
            }
            
            // Actualizar el contenido guardado
            updateTextoFormateado(type, index, field, editor.innerHTML);
        }
        
        function limpiarFormatoNotas(type, index, field) {
            const editorId = `notas-editor-${field}-${index}`;
            const editor = document.getElementById(editorId);
            
            if (!editor) {
                console.error('❌ No se encontró el editor de notas');
                return;
            }
            
            // Limpiar todo el formato HTML, mantener solo el texto
            const textoLimpio = editor.innerText || editor.textContent || '';
            editor.innerHTML = textoLimpio;
            
            // Actualizar el contenido guardado
            updateTextoFormateado(type, index, field, editor.innerHTML);
        }
        
        function updateTextoFormateado(type, index, field, htmlValue) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            if (!item) return;
            
            // Guardar el HTML formateado
            item[field] = htmlValue;
            
            // Guardar en localStorage
            const textosData = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
            const itemId = item.id;
            
            if (!textosData[itemId]) textosData[itemId] = {};
            textosData[itemId][field] = htmlValue;
            
            // Guardar también otros campos importantes
            if (type === 'reuniones') {
                textosData[itemId].company = item.company || '';
                textosData[itemId].person = item.person || '';
                textosData[itemId].product = item.product || '';
                textosData[itemId].time = item.time || '';
                textosData[itemId].stand = item.stand || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
            } else {
                textosData[itemId].empresa = item.empresa || '';
                textosData[itemId].producto = item.producto || '';
                textosData[itemId].oportunidad = item.oportunidad || '';
                textosData[itemId].departamento = item.departamento || 'Lizarte';
            }
            
            localStorage.setItem('textos_modificados_automechanika', JSON.stringify(textosData));
        }
        
        function autoResizeTextarea(element) {
            element.style.height = 'auto';
            element.style.height = element.scrollHeight + 'px';
        }
        
        function addFoto(type, index) {
            currentUploadTarget = { type, index };
            document.getElementById('fileInput').click();
        }
        
        function handleFileUpload(event) {
            const files = event.target.files;
            if (!files.length || !currentUploadTarget) return;
            
            const { type, index } = currentUploadTarget;
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            
            if (!item.fotos_extra) item.fotos_extra = [];
            
            Array.from(files).forEach(file => {
                const reader = new FileReader();
                reader.onload = (e) => {
                    item.fotos_extra.push(e.target.result);
                    saveSeguimiento();
                    renderAll();
                };
                reader.readAsDataURL(file);
            });
            
            event.target.value = '';
        }
        
        function deleteFoto(type, index, fotoIdx) {
            if (!confirm('¿Eliminar esta foto? (Podrás recuperarla desde la papelera)')) return;
            
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            const allFotos = [...(Array.isArray(item.fotos) ? item.fotos : []), ...(item.fotos_extra || [])];
            const fotoUrl = allFotos[fotoIdx];
            
            // Guardar en papelera
            const papelera = JSON.parse(localStorage.getItem('papelera_fotos_automechanika') || '{}');
            if (!papelera[item.id]) papelera[item.id] = [];
            
            papelera[item.id].push({
                url: fotoUrl,
                fecha: new Date().toISOString(),
                tipo: fotoIdx < item.fotos.length ? 'original' : 'extra',
                indice: fotoIdx
            });
            
            localStorage.setItem('papelera_fotos_automechanika', JSON.stringify(papelera));
            
            // Eliminar del array correspondiente
            if (!item.fotos || !Array.isArray(item.fotos)) item.fotos = [];
            if (!item.fotos_extra || !Array.isArray(item.fotos_extra)) item.fotos_extra = [];
            
            if (fotoIdx < item.fotos.length) {
                item.fotos.splice(fotoIdx, 1);
            } else {
                const extraIdx = fotoIdx - item.fotos.length;
                item.fotos_extra.splice(extraIdx, 1);
            }
            
            saveSeguimiento();
            renderAll();
        }
        
        function verPapelera(type, index) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            const papelera = JSON.parse(localStorage.getItem('papelera_fotos_automechanika') || '{}');
            const fotosBorradas = papelera[item.id] || [];
            
            if (fotosBorradas.length === 0) {
                alert('No hay fotos borradas para recuperar');
                return;
            }
            
            const html = `
                <div style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); z-index: 2000; display: flex; align-items: center; justify-content: center; padding: 20px;" id="papeleraModal" onclick="cerrarPapelera(event)">
                    <div style="background: white; border-radius: 16px; padding: 20px; max-width: 600px; max-height: 80vh; overflow-y: auto;" onclick="event.stopPropagation()">
                        <h3 style="margin-bottom: 15px;">♻️ Papelera de Fotos</h3>
                        <p style="font-size: 13px; color: #6b7280; margin-bottom: 15px;">Haz clic en una foto para recuperarla</p>
                        <div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(100px, 1fr)); gap: 10px;">
                            ${fotosBorradas.map((foto, idx) => `
                                <div style="position: relative; cursor: pointer;" onclick="recuperarFoto('${type}', ${index}, ${idx})">
                                    <img src="${foto.url}" style="width: 100%; height: 100px; object-fit: cover; border-radius: 8px; border: 2px solid #e5e7eb;">
                                    <div style="position: absolute; bottom: 4px; right: 4px; background: #10b981; color: white; padding: 4px 8px; border-radius: 4px; font-size: 10px;">Recuperar</div>
                                </div>
                            `).join('')}
                        </div>
                        <button onclick="cerrarPapelera()" style="margin-top: 15px; width: 100%; padding: 10px; background: #6b7280; color: white; border: none; border-radius: 8px; cursor: pointer;">Cerrar</button>
                    </div>
                </div>
            `;
            
            document.body.insertAdjacentHTML('beforeend', html);
        }
        
        function recuperarFoto(type, index, papeleraIdx) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            const papelera = JSON.parse(localStorage.getItem('papelera_fotos_automechanika') || '{}');
            const fotosBorradas = papelera[item.id] || [];
            
            if (fotosBorradas[papeleraIdx]) {
                const foto = fotosBorradas[papeleraIdx];
                
                // Restaurar foto
                if (!item.fotos_extra) item.fotos_extra = [];
                item.fotos_extra.push(foto.url);
                
                // Eliminar de papelera
                fotosBorradas.splice(papeleraIdx, 1);
                papelera[item.id] = fotosBorradas;
                localStorage.setItem('papelera_fotos_automechanika', JSON.stringify(papelera));
                
                saveSeguimiento();
                cerrarPapelera();
                renderAll();
                
                alert('✅ Foto recuperada');
            }
        }
        
        function cerrarPapelera(event) {
            if (event && event.target.id !== 'papeleraModal') return;
            const modal = document.getElementById('papeleraModal');
            if (modal) modal.remove();
        }
        
        // ========== FUNCIONES DOCUMENTACIÓN ==========
        
        function addDocumentoLink(type, index) {
            const nombre = prompt('Título del documento/email:');
            if (!nombre) return;
            
            const url = prompt('URL o link del email:');
            if (!url) return;
            
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            if (!item.documentos) item.documentos = [];
            
            item.documentos.push({
                tipo: 'link',
                nombre: nombre,
                url: url,
                fecha: new Date().toISOString()
            });
            
            saveDocumentos();
            renderAll();
        }
        
        function addDocumentoArchivo(type, index) {
            currentUploadTarget = { type, index, isDoc: true };
            
            const input = document.createElement('input');
            input.type = 'file';
            input.accept = '.pdf,.doc,.docx,.xls,.xlsx,.jpg,.jpeg,.png';
            input.multiple = false;
            
            input.onchange = (e) => {
                const file = e.target.files[0];
                if (!file) return;
                
                // Validar tamaño (max 5MB)
                if (file.size > 5 * 1024 * 1024) {
                    alert('El archivo es demasiado grande. Máximo 5MB.');
                    return;
                }
                
                const reader = new FileReader();
                reader.onload = (event) => {
                    const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
                    if (!item.documentos) item.documentos = [];
                    
                    item.documentos.push({
                        tipo: 'archivo',
                        nombre: file.name,
                        data: event.target.result,
                        tamano: file.size,
                        fecha: new Date().toISOString()
                    });
                    
                    saveDocumentos();
                    renderAll();
                };
                
                reader.readAsDataURL(file);
            };
            
            input.click();
        }
        
        function deleteDocumento(type, index, docIdx) {
            if (!confirm('¿Eliminar este documento?')) return;
            
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            if (item.documentos) {
                item.documentos.splice(docIdx, 1);
            }
            
            saveDocumentos();
            renderAll();
        }
        
        function saveDocumentos() {
            const docsData = {};
            
            appData.reuniones.forEach(item => {
                if (item.documentos && item.documentos.length > 0) {
                    docsData[item.id] = item.documentos;
                }
            });
            
            appData.adicional.forEach(item => {
                if (item.documentos && item.documentos.length > 0) {
                    docsData[item.id] = item.documentos;
                }
            });
            
            localStorage.setItem('documentos_automechanika', JSON.stringify(docsData));
            showSaveIndicator();
        }
        
        function loadDocumentos() {
            const docsData = JSON.parse(localStorage.getItem('documentos_automechanika') || '{}');
            
            appData.reuniones.forEach(item => {
                if (docsData[item.id]) {
                    item.documentos = docsData[item.id];
                }
            });
            
            appData.adicional.forEach(item => {
                if (docsData[item.id]) {
                    item.documentos = docsData[item.id];
                }
            });
        }
        
        function sendNotification(type, index) {
            const item = type === 'reuniones' ? appData.reuniones[index] : appData.adicional[index];
            const seg = item.seguimiento;
            const empresa = item.company || item.empresa;
            
            if (!seg.email) {
                alert('No hay email configurado');
                return;
            }
            
            const subject = `Acción pendiente - ${empresa}`;
            const body = `Hola ${seg.responsable || ''},

Tienes una acción pendiente de seguimiento:

Empresa: ${empresa}
Estado: ${seg.estado.toUpperCase()}
${seg.fechaSeguimiento ? `Fecha seguimiento: ${seg.fechaSeguimiento}` : ''}

${seg.acciones && seg.acciones.length > 0 ? `Acciones pendientes:
${seg.acciones.map((a, i) => `${i + 1}. ${a}`).join('\n')}` : ''}

Puedes ver más detalles en:
https://krumkk.github.io/seguimiento-automechanika-2025/

Saludos,
Sistema de Seguimiento Automechanika`;
            
            const mailto = `mailto:${seg.email}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
            window.location.href = mailto;
        }
        
        function openModal(src) {
            document.getElementById('modalImage').src = src;
            document.getElementById('photoModal').classList.add('show');
        }
        
        function closeModal() {
            document.getElementById('photoModal').classList.remove('show');
        }
        
        async function exportarDatosActualizados(evt) {
            let button = null;
            let originalText = '📤 EXPORTAR';
            
            try {
                button = evt && evt.target ? evt.target : document.querySelector('.btn-float-export');
                if (button) {
                    originalText = button.innerHTML;
                    button.innerHTML = '⏳ Exportando...';
                    button.disabled = true;
                }
                
                console.log('📤 Iniciando exportación de datos actualizados...');
                
                // Cargar datos base
                console.log('📥 Cargando datos.json...');
                const response = await fetch('datos.json');
                if (!response.ok) {
                    throw new Error('No se pudo cargar datos.json');
                }
                const datosBase = await response.json();
                console.log('✅ datos.json cargado:', datosBase);
                
                // Aplicar textos modificados Y añadir empresas nuevas
                console.log('📝 Aplicando textos modificados...');
                const textosModificados = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
                console.log('📊 Total items en textosModificados:', Object.keys(textosModificados).length);
                // Verificar si ALTEZZA está en textosModificados
                const altezzaId = '1763364468847';
                if (textosModificados[altezzaId]) {
                    console.log('✅ ALTEZZA encontrada en textosModificados:', {
                        respuestas: textosModificados[altezzaId].respuestas,
                        conclusionFinal: textosModificados[altezzaId].conclusionFinal,
                        finalizado: textosModificados[altezzaId].finalizado
                    });
                } else {
                    console.log('⚠️ ALTEZZA NO encontrada en textosModificados. IDs disponibles:', Object.keys(textosModificados).slice(0, 10));
                }
                
                // Cargar lista de empresas eliminadas ANTES de añadir nuevas
                const empresasEliminadas = JSON.parse(localStorage.getItem('empresas_eliminadas_automechanika') || '{}');
                
                // Función auxiliar para hacer merge inteligente preservando texto original
                function mergeItemData(original, modificado) {
                    // Crear una copia del original
                    const merged = { ...original };
                    // Lista de campos de texto que pueden tener contenido largo
                    const camposTexto = ['comments', 'notas', 'oportunidad', 'product', 'producto', 'company', 'empresa', 'person', 'conclusionFinal'];
                    // Campos especiales que siempre deben usar el valor modificado si existe
                    const camposEspeciales = ['respuestas', 'finalizado'];
                    
                    // Aplicar modificaciones
                    Object.keys(modificado).forEach(key => {
                        if (key === 'seguimiento' && typeof modificado[key] === 'object') {
                            // Merge profundo para seguimiento
                            merged[key] = { ...original[key], ...modificado[key] };
                            // Preservar arrays dentro de seguimiento (acciones)
                            if (modificado[key].acciones && Array.isArray(modificado[key].acciones)) {
                                merged[key].acciones = modificado[key].acciones;
                            }
                        } else if (camposEspeciales.includes(key)) {
                            // Para campos especiales (respuestas, finalizado), usar siempre el modificado si existe
                            if (modificado[key] !== undefined) {
                                merged[key] = modificado[key];
                            }
                        } else if (Array.isArray(modificado[key])) {
                            // Para arrays, usar el modificado directamente
                            merged[key] = modificado[key];
                        } else if (camposTexto.includes(key)) {
                            // Para campos de texto: preservar original si el modificado está vacío
                            const valorModificado = modificado[key];
                            const valorOriginal = original[key];
                            
                            // Si el modificado es string vacío pero el original tiene contenido,
                            // preservar el original (probablemente no fue editado, solo se guardó como '')
                            if (typeof valorModificado === 'string' && valorModificado === '' && 
                                typeof valorOriginal === 'string' && valorOriginal !== '') {
                                merged[key] = valorOriginal;
                            } else {
                                // Usar el modificado (tiene contenido o fue explícitamente borrado)
                                merged[key] = valorModificado;
                            }
                        } else {
                            // Para otros campos, usar el modificado
                            merged[key] = modificado[key];
                        }
                    });
                    // Preservar campos del original que no están en modificados
                    Object.keys(original).forEach(key => {
                        if (modificado[key] === undefined && original[key] !== undefined) {
                            merged[key] = original[key];
                        }
                    });
                    return merged;
                }
                
                // Actualizar empresas existentes en reuniones
                datosBase.reuniones.forEach(item => {
                    // Buscar por ID como string y como número
                    const itemIdStr = String(item.id);
                    const itemIdNum = Number(item.id);
                    const datosModificados = textosModificados[item.id] || textosModificados[itemIdStr] || textosModificados[itemIdNum];
                    
                    if (datosModificados) {
                        console.log('📤 Exportando reunión ID:', item.id, 'Company:', item.company);
                        console.log('📋 Datos en textosModificados:', {
                            respuestas: datosModificados.respuestas,
                            conclusionFinal: datosModificados.conclusionFinal,
                            finalizado: datosModificados.finalizado
                        });
                        // Hacer merge preservando texto original si el modificado está vacío
                        const merged = mergeItemData(item, datosModificados);
                        Object.assign(item, merged);
                        // Asegurar que respuestas, conclusionFinal y finalizado se copien explícitamente
                        if (datosModificados.respuestas !== undefined) {
                            item.respuestas = datosModificados.respuestas;
                            console.log('✅ Respuestas copiadas al exportar:', item.respuestas);
                        }
                        if (datosModificados.conclusionFinal !== undefined) {
                            item.conclusionFinal = datosModificados.conclusionFinal;
                            console.log('✅ Conclusión final copiada al exportar:', item.conclusionFinal);
                        }
                        if (datosModificados.finalizado !== undefined) {
                            item.finalizado = datosModificados.finalizado;
                            console.log('✅ Finalizado copiado al exportar:', item.finalizado);
                        }
                        console.log('📦 Item final después del merge:', {
                            respuestas: item.respuestas,
                            conclusionFinal: item.conclusionFinal,
                            finalizado: item.finalizado
                        });
                    }
                });
                
                // Añadir NUEVAS empresas en reuniones que no están en datosBase Y no fueron eliminadas
                Object.keys(textosModificados).forEach(id => {
                    const existeEnReuniones = datosBase.reuniones.find(item => item.id == id);
                    const existeEnAdicional = datosBase.adicional.find(item => item.id == id);
                    
                    // Verificar si fue eliminada
                    const idStr = String(id);
                    const idNum = Number(id);
                    const fueEliminada = (empresasEliminadas.reuniones && (
                        empresasEliminadas.reuniones.includes(idStr) || 
                        empresasEliminadas.reuniones.includes(id) ||
                        empresasEliminadas.reuniones.includes(idNum)
                    )) || (empresasEliminadas.adicional && (
                        empresasEliminadas.adicional.includes(idStr) || 
                        empresasEliminadas.adicional.includes(id) ||
                        empresasEliminadas.adicional.includes(idNum)
                    ));
                    
                    if (!existeEnReuniones && !existeEnAdicional && !fueEliminada) {
                        const nuevaEmpresa = textosModificados[id];
                        // Si tiene campo 'company', es de reuniones
                        if (nuevaEmpresa.company !== undefined) {
                            console.log('➕ Añadiendo nueva reunión:', nuevaEmpresa.company);
                            datosBase.reuniones.push({
                                id: id,
                                ...nuevaEmpresa
                            });
                        }
                        // Si tiene campo 'empresa', es de adicional
                        else if (nuevaEmpresa.empresa !== undefined) {
                            console.log('➕ Añadiendo nueva empresa adicional:', nuevaEmpresa.empresa);
                            datosBase.adicional.push({
                                id: id,
                                ...nuevaEmpresa
                            });
                        }
                    } else if (fueEliminada) {
                        console.log('🚫 Omitiendo empresa eliminada (ID:', id, ')');
                    }
                });
                
                // Actualizar empresas existentes en adicional
                datosBase.adicional.forEach(item => {
                    // Buscar por ID como string y como número
                    const itemIdStr = String(item.id);
                    const itemIdNum = Number(item.id);
                    const datosModificados = textosModificados[item.id] || textosModificados[itemIdStr] || textosModificados[itemIdNum];
                    
                    if (datosModificados) {
                        console.log('📤 Exportando adicional ID:', item.id, 'Empresa:', item.empresa);
                        console.log('📋 Datos en textosModificados:', {
                            respuestas: datosModificados.respuestas,
                            conclusionFinal: datosModificados.conclusionFinal,
                            finalizado: datosModificados.finalizado
                        });
                        // Hacer merge preservando texto original si el modificado está vacío
                        const merged = mergeItemData(item, datosModificados);
                        Object.assign(item, merged);
                        // Asegurar que respuestas, conclusionFinal y finalizado se copien explícitamente
                        if (datosModificados.respuestas !== undefined) {
                            item.respuestas = datosModificados.respuestas;
                            console.log('✅ Respuestas copiadas al exportar:', item.respuestas);
                        }
                        if (datosModificados.conclusionFinal !== undefined) {
                            item.conclusionFinal = datosModificados.conclusionFinal;
                            console.log('✅ Conclusión final copiada al exportar:', item.conclusionFinal);
                        }
                        if (datosModificados.finalizado !== undefined) {
                            item.finalizado = datosModificados.finalizado;
                            console.log('✅ Finalizado copiado al exportar:', item.finalizado);
                        }
                        console.log('📦 Item final después del merge:', {
                            respuestas: item.respuestas,
                            conclusionFinal: item.conclusionFinal,
                            finalizado: item.finalizado
                        });
                    }
                });
                
                // NO aplicar seguimiento desde seguimiento_v2_automechanika aquí
                // porque ya está incluido en textosModificados y se aplicó en el merge
                // Solo aplicar si NO está en textosModificados (casos legacy)
                console.log('📊 Verificando seguimiento legacy...');
                const seguimientoData = JSON.parse(localStorage.getItem('seguimiento_v2_automechanika') || '{}');
                
                datosBase.reuniones.forEach(item => {
                    // Solo aplicar seguimiento legacy si no está en textosModificados
                    if (seguimientoData[item.id] && !textosModificados[item.id]) {
                        item.seguimiento = seguimientoData[item.id];
                    }
                });
                
                datosBase.adicional.forEach(item => {
                    // Solo aplicar seguimiento legacy si no está en textosModificados
                    if (seguimientoData[item.id] && !textosModificados[item.id]) {
                        item.seguimiento = seguimientoData[item.id];
                    }
                });
                
                // Aplicar fotos borradas (eliminarlas del JSON)
                console.log('🗑️ Aplicando fotos borradas...');
                const deletedPhotosData = JSON.parse(localStorage.getItem('deleted_photos_automechanika') || '{}');
                
                datosBase.reuniones.forEach(item => {
                    if (deletedPhotosData[item.id] && deletedPhotosData[item.id].length > 0) {
                        const deletedIndices = deletedPhotosData[item.id];
                        if (!item.fotos || !Array.isArray(item.fotos)) item.fotos = [];
                        item.fotos = item.fotos.filter((foto, idx) => !deletedIndices.includes(idx));
                    }
                });
                
                datosBase.adicional.forEach(item => {
                    if (deletedPhotosData[item.id] && deletedPhotosData[item.id].length > 0) {
                        const deletedIndices = deletedPhotosData[item.id];
                        if (!item.fotos || !Array.isArray(item.fotos)) item.fotos = [];
                        item.fotos = item.fotos.filter((foto, idx) => !deletedIndices.includes(idx));
                    }
                });
                
                // Eliminar empresas que fueron borradas (ya cargamos empresasEliminadas arriba)
                console.log('🗑️ Eliminando empresas borradas...');
                
                if (empresasEliminadas.reuniones && empresasEliminadas.reuniones.length > 0) {
                    console.log('🗑️ Eliminando', empresasEliminadas.reuniones.length, 'reuniones borradas');
                    console.log('🗑️ IDs de reuniones eliminadas:', empresasEliminadas.reuniones);
                    const antes = datosBase.reuniones.length;
                    datosBase.reuniones = datosBase.reuniones.filter(item => {
                        const itemId = String(item.id);
                        const itemIdNum = Number(item.id);
                        // Comparar tanto como string como número
                        const estaEliminada = empresasEliminadas.reuniones.includes(itemId) || 
                                             empresasEliminadas.reuniones.includes(item.id) ||
                                             empresasEliminadas.reuniones.includes(itemIdNum) ||
                                             empresasEliminadas.reuniones.some(id => String(id) === itemId || Number(id) === itemIdNum);
                        if (estaEliminada) {
                            console.log('🗑️ Eliminando reunión:', item.company, '(ID:', item.id, ')');
                        }
                        return !estaEliminada;
                    });
                    console.log('🗑️ Reuniones antes:', antes, 'después:', datosBase.reuniones.length);
                }
                
                if (empresasEliminadas.adicional && empresasEliminadas.adicional.length > 0) {
                    console.log('🗑️ Eliminando', empresasEliminadas.adicional.length, 'empresas adicionales borradas');
                    console.log('🗑️ IDs de adicional eliminadas:', empresasEliminadas.adicional);
                    const antes = datosBase.adicional.length;
                    datosBase.adicional = datosBase.adicional.filter(item => {
                        const itemId = String(item.id);
                        const itemIdNum = Number(item.id);
                        // Comparar tanto como string como número
                        const estaEliminada = empresasEliminadas.adicional.includes(itemId) || 
                                             empresasEliminadas.adicional.includes(item.id) ||
                                             empresasEliminadas.adicional.includes(itemIdNum) ||
                                             empresasEliminadas.adicional.some(id => String(id) === itemId || Number(id) === itemIdNum);
                        if (estaEliminada) {
                            console.log('🗑️ Eliminando adicional:', item.empresa, '(ID:', item.id, ')');
                        }
                        return !estaEliminada;
                    });
                    console.log('🗑️ Adicional antes:', antes, 'después:', datosBase.adicional.length);
                }
                
                // Añadir nuevos campos (nuevosCoches y ahorros) al JSON exportado
                console.log('🚗 Añadiendo nuevos coches al JSON exportado...');
                if (appData.nuevosCoches && appData.nuevosCoches.length > 0) {
                    datosBase.nuevosCoches = appData.nuevosCoches;
                    console.log('✅ Nuevos coches añadidos:', appData.nuevosCoches.length);
                } else {
                    datosBase.nuevosCoches = [];
                }
                
                console.log('💰 Añadiendo ahorros al JSON exportado...');
                if (appData.ahorros && appData.ahorros.length > 0) {
                    datosBase.ahorros = appData.ahorros;
                    console.log('✅ Ahorros añadidos:', appData.ahorros.length);
                } else {
                    datosBase.ahorros = [];
                }
                
                // Generar JSON
                console.log('📦 Generando archivo JSON...');
                const jsonString = JSON.stringify(datosBase, null, 2);
                const blob = new Blob([jsonString], { type: 'application/json' });
                
                // Descargar
                console.log('💾 Descargando archivo...');
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = 'datos.json';
                a.style.display = 'none';
                document.body.appendChild(a);
                a.click();
                
                // Limpiar
                setTimeout(() => {
                    document.body.removeChild(a);
                    URL.revokeObjectURL(url);
                }, 100);
                
                console.log('✅ Datos exportados correctamente');
                
                // Limpiar lista de empresas eliminadas ya que están eliminadas del JSON exportado
                // IMPORTANTE: El usuario debe reemplazar datos.json con el archivo exportado para que sea permanente
                let empresasEliminadasCount = 0;
                if (empresasEliminadas.reuniones && empresasEliminadas.reuniones.length > 0) {
                    empresasEliminadasCount += empresasEliminadas.reuniones.length;
                    console.log('🧹 Limpiando', empresasEliminadas.reuniones.length, 'reuniones eliminadas de la lista');
                    empresasEliminadas.reuniones = [];
                }
                if (empresasEliminadas.adicional && empresasEliminadas.adicional.length > 0) {
                    empresasEliminadasCount += empresasEliminadas.adicional.length;
                    console.log('🧹 Limpiando', empresasEliminadas.adicional.length, 'empresas adicionales eliminadas de la lista');
                    empresasEliminadas.adicional = [];
                }
                
                if (empresasEliminadasCount > 0) {
                    localStorage.setItem('empresas_eliminadas_automechanika', JSON.stringify(empresasEliminadas));
                    console.log('✅ Lista de empresas eliminadas limpiada. Total eliminadas:', empresasEliminadasCount);
                }
                
                // Restaurar botón (en un try-catch separado para no afectar el éxito)
                try {
                    if (button) {
                        button.innerHTML = '✅ ¡Exportado!';
                        setTimeout(() => {
                            button.innerHTML = originalText;
                            button.disabled = false;
                        }, 2000);
                    }
                } catch (btnError) {
                    console.warn('⚠️ Error restaurando botón (no crítico):', btnError);
                }
                
                // Mostrar instrucciones (en un try-catch separado)
                try {
                    alert('✅ Archivo datos.json descargado\n\n📤 IMPORTANTE:\n\n1. Reemplaza el archivo datos.json en la raíz del proyecto con este archivo descargado\n2. Las empresas eliminadas ya NO aparecerán en el JSON\n3. La lista de eliminadas se ha limpiado\n\n⚠️ Si no reemplazas el archivo, las empresas eliminadas volverán a aparecer al recargar.');
                } catch (alertError) {
                    console.warn('⚠️ Error mostrando alert (no crítico):', alertError);
                }
                
            } catch (error) {
                console.error('❌ Error exportando datos:', error);
                console.error('Stack trace:', error.stack);
                
                // Intentar restaurar botón incluso si hay error
                try {
                    if (button) {
                        button.innerHTML = '❌ Error';
                        setTimeout(() => {
                            button.innerHTML = originalText;
                            button.disabled = false;
                        }, 2000);
                    }
                } catch (btnError) {
                    console.warn('⚠️ Error restaurando botón después de error:', btnError);
                }
                
                alert('❌ Error al exportar datos.\n\nError: ' + error.message + '\n\nRevisa la consola (F12) para más detalles.');
            }
        }
        
        function exportarInforme() {
            // Generar HTML que Word puede abrir directamente
            let html = `<!DOCTYPE html>
<html xmlns:o='urn:schemas-microsoft-com:office:office' xmlns:w='urn:schemas-microsoft-com:office:word' xmlns='http://www.w3.org/TR/REC-html40'>
<head>
    <meta charset='utf-8'>
    <title>${appConfig.titulo}</title>
    <style>
        @page {
            size: A4;
            margin: 2.5cm 2cm 2.5cm 2cm;
        }
        body {
            font-family: 'Calibri', 'Arial', sans-serif;
            font-size: 11pt;
            line-height: 1.5;
            color: #000;
        }
        .empresa-page {
            width: 100%;
            min-height: 100vh;
        }
        h1 {
            font-size: 18pt;
            font-weight: bold;
            margin-bottom: 10pt;
            color: #2d3748;
        }
        h2 {
            font-size: 16pt;
            font-weight: bold;
            margin-top: 20pt;
            margin-bottom: 10pt;
            color: #4a5568;
            border-bottom: 2px solid #667eea;
            padding-bottom: 5pt;
        }
        h3 {
            font-size: 14pt;
            font-weight: bold;
            margin-top: 15pt;
            margin-bottom: 8pt;
            color: #718096;
        }
        .empresa-nombre {
            font-size: 20pt;
            font-weight: bold;
            color: #667eea;
            margin-bottom: 15pt;
            padding-bottom: 10pt;
            border-bottom: 3px solid #667eea;
        }
        .info-row {
            margin: 8pt 0;
        }
        .info-label {
            font-weight: bold;
            display: inline-block;
            width: 120pt;
            color: #4a5568;
        }
        .info-value {
            display: inline-block;
        }
        .seguimiento-section {
            margin-top: 20pt;
            padding: 15pt;
            background-color: #f7fafc;
            border-left: 4px solid #667eea;
        }
        .acciones-list {
            margin-left: 20pt;
            margin-top: 10pt;
        }
        .accion-item {
            margin: 5pt 0;
        }
        .texto-largo {
            margin-top: 10pt;
            padding: 10pt;
            background-color: #ffffff;
            border: 1px solid #e2e8f0;
            white-space: pre-wrap;
            word-wrap: break-word;
        }
        .badge {
            display: inline-block;
            padding: 3pt 8pt;
            border-radius: 4pt;
            font-size: 9pt;
            font-weight: bold;
            margin-left: 8pt;
        }
        .badge-lizarte {
            background-color: #dbeafe;
            color: #1e40af;
        }
        .badge-innovacion {
            background-color: #fef3c7;
            color: #92400e;
        }
        .badge-prioridad-0 {
            background-color: #fce7f3;
            color: #be185d;
        }
        .badge-prioridad-1 {
            background-color: #dcfce7;
            color: #166534;
        }
        .badge-prioridad-2 {
            background-color: #fef3c7;
            color: #92400e;
        }
        .badge-prioridad-3 {
            background-color: #ffedd5;
            color: #c2410c;
        }
        .badge-estado {
            display: inline-block;
            padding: 4pt 10pt;
            border-radius: 6pt;
            font-size: 10pt;
            font-weight: bold;
            text-transform: uppercase;
        }
        .estado-pendiente {
            background-color: #f3f4f6;
            color: #6b7280;
        }
        .estado-contactado {
            background-color: #fef3c7;
            color: #d97706;
        }
        .estado-proceso {
            background-color: #dbeafe;
            color: #2563eb;
        }
        .estado-finalizado {
            background-color: #d1fae5;
            color: #059669;
        }
    </style>
</head>
<body>`;

            // NO incluir página de resumen - empezar directamente con las empresas

            // Función auxiliar para escapar HTML
            function escapeHtml(text) {
                if (!text) return '';
                return String(text)
                    .replace(/&/g, '&amp;')
                    .replace(/</g, '&lt;')
                    .replace(/>/g, '&gt;')
                    .replace(/"/g, '&quot;')
                    .replace(/'/g, '&#039;');
            }

            // Función para generar HTML de una empresa (TODA la información en una página)
            function generarEmpresaHTML(item, esReunion, esPrimeraEmpresa) {
                const nombre = esReunion ? item.company : item.empresa;
                const depto = item.departamento || 'Lizarte';
                const deptoClass = depto.toLowerCase() === 'innovación' ? 'badge-innovacion' : 'badge-lizarte';
                const seg = item.seguimiento || {};
                const estadoClass = `estado-${seg.estado || 'pendiente'}`;
                
                let empresaHTML = '';
                // Salto de página solo si no es la primera empresa del documento
                if (!esPrimeraEmpresa) {
                    empresaHTML += `<div style="page-break-before: always; break-before: page;"></div>`;
                    empresaHTML += `<!--[if gte mso 9]><br clear=all style='mso-special-character:line-break; page-break-before:always'><![endif]-->`;
                }
                empresaHTML += `
    <div class="empresa-page" style="width: 29.7cm; min-height: 21cm; margin: 0; padding: 1.5cm; page-break-after: auto; break-after: auto;">
        <table style="width: 100%; border-collapse: collapse;">
            <!-- Fila 1: Nombre + Información Básica (izquierda) y Seguimiento (derecha) -->
            <tr>
                <!-- Columna Izquierda: Nombre e Información Básica -->
                <td style="width: 50%; vertical-align: top; padding-right: 15pt;">
                    <div class="empresa-nombre" style="margin-bottom: 15pt;">
                        ${escapeHtml(nombre)}
                        <span class="badge ${deptoClass}">${escapeHtml(depto)}</span>
                    </div>

                    <div>
                        <h3 style="font-size: 12pt; margin-bottom: 8pt; color: #4a5568; border-bottom: 2px solid #e2e8f0; padding-bottom: 3pt;">Información Básica</h3>`;

                if (esReunion) {
                    empresaHTML += `
                        <div class="info-row" style="margin: 5pt 0;"><span class="info-label">Persona de contacto:</span><span class="info-value">${escapeHtml(item.person || 'N/A')}</span></div>
                        <div class="info-row" style="margin: 5pt 0;"><span class="info-label">Producto/Servicio:</span><span class="info-value">${escapeHtml(item.product || 'N/A')}</span></div>`;
                    const allFotos = [...(Array.isArray(item.fotos) ? item.fotos : []), ...(item.fotos_extra || [])];
                    empresaHTML += `
                        <div class="info-row" style="margin: 5pt 0;"><span class="info-label">Fotos:</span><span class="info-value">${allFotos.length} foto(s)</span></div>`;
                } else {
                    empresaHTML += `
                        <div class="info-row" style="margin: 5pt 0;"><span class="info-label">Producto/Servicio:</span><span class="info-value">${escapeHtml(item.producto || 'N/A')}</span></div>
                        <div class="info-row" style="margin: 5pt 0;"><span class="info-label">Prioridad:</span><span class="info-value"><span class="badge badge-prioridad-${item.prioridad !== undefined ? item.prioridad : 1}">${getPrioridadTexto(item.prioridad)}</span></span></div>`;
                }

                empresaHTML += `
                    </div>
                </td>

                <!-- Columna Derecha: Seguimiento -->
                <td style="width: 50%; vertical-align: top; padding-left: 15pt;">
                    <div class="seguimiento-section" style="padding: 15pt; background-color: #f7fafc; border-left: 4px solid #667eea;">
                        <h3 style="font-size: 12pt; margin-bottom: 12pt; color: #4a5568; border-bottom: 2px solid #667eea; padding-bottom: 3pt;">Seguimiento</h3>
                        
                        <div>
                            <div class="info-row" style="margin: 5pt 0;">
                                <span class="info-label">Estado:</span>
                                <span class="info-value"><span class="badge-estado ${estadoClass}">${(seg.estado || 'pendiente').toUpperCase()}</span></span>
                            </div>
                            <div class="info-row" style="margin: 5pt 0;">
                                <span class="info-label">Responsable:</span>
                                <span class="info-value">${seg.responsable ? escapeHtml(seg.responsable) : '<em style="color: #a0aec0;">Sin asignar</em>'}</span>
                            </div>
                            <div class="info-row" style="margin: 5pt 0;">
                                <span class="info-label">Email:</span>
                                <span class="info-value">${seg.email ? escapeHtml(seg.email) : '<em style="color: #a0aec0;">Sin email</em>'}</span>
                            </div>
                            <div class="info-row" style="margin: 5pt 0;">
                                <span class="info-label">Fecha seguimiento:</span>
                                <span class="info-value">${seg.fechaSeguimiento ? escapeHtml(seg.fechaSeguimiento) : '<em style="color: #a0aec0;">Sin fecha</em>'}</span>
                            </div>
                        </div>`;
                
                if (seg.proximaAccion) {
                    empresaHTML += `
                        <div style="margin-top: 12pt;">
                            <h3 style="font-size: 11pt; margin-bottom: 5pt; color: #718096;">Próxima Acción</h3>
                            <div class="texto-largo" style="font-size: 10pt; padding: 8pt; background: #ffffff; border: 1px solid #e2e8f0; white-space: pre-wrap; word-wrap: break-word;">${escapeHtml(seg.proximaAccion).replace(/\n/g, '<br>')}</div>
                        </div>`;
                }
                
                empresaHTML += `
                    </div>
                </td>
            </tr>

            <!-- Fila 2: Notas/Comentarios (ancho completo) -->
            <tr>
                <td colspan="2" style="vertical-align: top; padding-top: 20pt;">`;

                // Notas/Comentarios - Ancho completo (con formato HTML)
                if (esReunion) {
                    empresaHTML += `
                    <h3 style="font-size: 12pt; margin-bottom: 10pt; color: #4a5568; border-bottom: 2px solid #e2e8f0; padding-bottom: 3pt;">Notas / Comentarios</h3>
                    <div class="texto-largo" style="padding: 15pt; background: #ffffff; border: 1px solid #e2e8f0; white-space: pre-wrap; word-wrap: break-word; min-height: 200pt;">${item.comments ? item.comments.replace(/\n/g, '<br>') : '<em style="color: #a0aec0;">Sin notas</em>'}</div>`;
                } else {
                    empresaHTML += `
                    <h3 style="font-size: 12pt; margin-bottom: 10pt; color: #4a5568; border-bottom: 2px solid #e2e8f0; padding-bottom: 3pt;">Notas</h3>
                    <div class="texto-largo" style="padding: 15pt; background: #ffffff; border: 1px solid #e2e8f0; white-space: pre-wrap; word-wrap: break-word; min-height: 150pt; margin-bottom: 15pt;">${item.notas ? item.notas.replace(/\n/g, '<br>') : '<em style="color: #a0aec0;">Sin notas</em>'}</div>`;
                    
                    if (item.oportunidad) {
                        empresaHTML += `
                    <h3 style="font-size: 12pt; margin-bottom: 10pt; color: #4a5568; border-bottom: 2px solid #e2e8f0; padding-bottom: 3pt;">Oportunidad de Negocio</h3>
                    <div class="texto-largo" style="padding: 15pt; background: #ffffff; border: 1px solid #e2e8f0; white-space: pre-wrap; word-wrap: break-word; min-height: 150pt;">${escapeHtml(item.oportunidad).replace(/\n/g, '<br>')}</div>`;
                    }
                }
                
                empresaHTML += `
                </td>
            </tr>

            <!-- Fila 3: Acciones Pendientes (ancho completo, abajo) -->
            <tr>
                <td colspan="2" style="vertical-align: top; padding-top: 20pt;">
                    <div style="padding: 15pt; background-color: #f7fafc; border-left: 4px solid #667eea;">
                        <h3 style="font-size: 12pt; margin-bottom: 10pt; color: #4a5568; border-bottom: 2px solid #667eea; padding-bottom: 3pt;">Acciones Pendientes</h3>`;
                
                if (seg.acciones && seg.acciones.length > 0 && seg.acciones.some(a => a && a.trim())) {
                    empresaHTML += `
                        <div class="acciones-list">`;
                    seg.acciones.forEach((accion, i) => {
                        if (accion && accion.trim()) {
                            empresaHTML += `
                            <div class="accion-item" style="margin-bottom: 10pt; padding: 10pt; background: #ffffff; border-left: 3px solid #667eea; white-space: pre-wrap; word-wrap: break-word;">${i + 1}. ${escapeHtml(accion)}</div>`;
                        }
                    });
                    empresaHTML += `
                        </div>`;
                } else {
                    empresaHTML += `
                        <div style="color: #a0aec0; font-style: italic; padding: 10pt;">No hay acciones registradas</div>`;
                }
                
                empresaHTML += `
                    </div>
                </td>
            </tr>
            
            <!-- Fila 4: Respuestas (ancho completo, después de Acciones Pendientes) -->
            <tr>
                <td colspan="2" style="vertical-align: top; padding-top: 20pt;">
                    <div style="padding: 15pt; background-color: #f0f9ff; border-left: 4px solid #3b82f6;">
                        <h3 style="font-size: 12pt; margin-bottom: 10pt; color: #4a5568; border-bottom: 2px solid #3b82f6; padding-bottom: 3pt;">💬 Respuestas</h3>`;
                
                if (item.respuestas && item.respuestas.length > 0) {
                    empresaHTML += `<div class="respuestas-list">`;
                    item.respuestas.forEach((respuesta, rIdx) => {
                        const texto = typeof respuesta === 'string' ? respuesta : (respuesta.texto || '');
                        const formato = typeof respuesta === 'object' ? (respuesta.formato || {}) : {};
                        let textoFormateado = escapeHtml(texto);
                        
                        // Aplicar formato negrita (**texto**)
                        if (formato.negrita) {
                            textoFormateado = textoFormateado.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
                        }
                        
                        // Aplicar formato lista (• al inicio de línea)
                        if (formato.lista) {
                            textoFormateado = textoFormateado.split('\n').map(linea => {
                                if (linea.trim() && !linea.trim().startsWith('•')) {
                                    return '• ' + linea.trim();
                                }
                                return linea;
                            }).join('\n');
                        }
                        
                        if (texto && texto.trim()) {
                            empresaHTML += `
                            <div style="margin-bottom: 12pt; padding: 10pt; background: #ffffff; border-left: 3px solid #3b82f6; white-space: pre-wrap; word-wrap: break-word;">${rIdx + 1}. ${textoFormateado.replace(/\n/g, '<br>')}</div>`;
                        }
                    });
                    empresaHTML += `</div>`;
                } else {
                    empresaHTML += `
                        <div style="color: #a0aec0; font-style: italic; padding: 10pt;">No hay respuestas registradas</div>`;
                }
                
                empresaHTML += `
                    </div>
                </td>
            </tr>
            
            <!-- Fila 5: Conclusión Final (ancho completo, después de Respuestas) -->
            <tr>
                <td colspan="2" style="vertical-align: top; padding-top: 20pt;">
                    <div style="padding: 15pt; background-color: #fef3c7; border-left: 4px solid #fbbf24;">
                        <h3 style="font-size: 12pt; margin-bottom: 10pt; color: #92400e; border-bottom: 2px solid #fbbf24; padding-bottom: 3pt;">📝 Conclusión Final ${item.finalizado ? '<span style="background: #10b981; color: white; padding: 4pt 10pt; border-radius: 6pt; font-size: 9pt; margin-left: 10pt;">✅ FINALIZADO</span>' : ''}</h3>`;
                
                if (item.conclusionFinal && item.conclusionFinal.trim()) {
                    let conclusionFormateada = escapeHtml(item.conclusionFinal);
                    // Aplicar formato negrita (**texto**)
                    conclusionFormateada = conclusionFormateada.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
                    // Aplicar formato lista (• al inicio de línea)
                    conclusionFormateada = conclusionFormateada.split('\n').map(linea => {
                        if (linea.trim() && !linea.trim().startsWith('•')) {
                            return '• ' + linea.trim();
                        }
                        return linea;
                    }).join('\n');
                    
                    empresaHTML += `
                        <div style="padding: 12pt; background: #ffffff; border: 1px solid #fbbf24; white-space: pre-wrap; word-wrap: break-word; min-height: 100pt;">${conclusionFormateada.replace(/\n/g, '<br>')}</div>`;
                } else {
                    empresaHTML += `
                        <div style="color: #a0aec0; font-style: italic; padding: 10pt;">No hay conclusión final registrada</div>`;
                }
                
                empresaHTML += `
                    </div>
                </td>
            </tr>
        </table>
    </div>`;

                return empresaHTML;
            }

            // REUNIONES - cada empresa en página nueva (orden del JSON/HTML, sin ordenar por hora)
            appData.reuniones.forEach((item, index) => {
                // Primera empresa del documento sin salto de página, resto con salto
                const esPrimera = index === 0 && appData.adicional.length === 0;
                html += generarEmpresaHTML(item, true, esPrimera);
            });

            // INFO ADICIONAL - cada empresa en página nueva (después de todas las reuniones)
            appData.adicional.forEach((item, index) => {
                // Primera adicional solo sin salto si no hay reuniones, resto con salto
                const esPrimera = index === 0 && appData.reuniones.length === 0;
                html += generarEmpresaHTML(item, false, esPrimera);
            });

            // Función para generar sección de Nuevos Coches (agrupada)
            function generarSeccionNuevosCoches(nuevosCoches) {
                let html = `
    <div style="page-break-before: always; padding: 20pt 0;">
        <h1 style="font-size: 20pt; font-weight: bold; margin-bottom: 20pt; color: #667eea; border-bottom: 3px solid #667eea; padding-bottom: 10pt;">🚗 Nuevos Coches</h1>
        <p style="font-size: 11pt; color: #718096; margin-bottom: 20pt; font-style: italic;">
            Marcas de coches nuevas observadas en China durante la estancia. Vehículos vistos por la calle, no necesariamente en la feria. 
            Marcas que no se habían visto en los últimos dos años pero que ahora se observan con alta frecuencia.
        </p>`;

                nuevosCoches.forEach((coche, index) => {
                    html += `
        <div style="margin-bottom: 25pt; padding: 15pt; background-color: #f7fafc; border-left: 4px solid #10b981; border-radius: 4px;">
            <h3 style="font-size: 14pt; font-weight: bold; margin-bottom: 10pt; color: #2d3748;">
                ${index + 1}. ${escapeHtml(coche.nombre || 'Sin nombre')}
            </h3>`;
                    
                    if (coche.descripcion && coche.descripcion.trim()) {
                        html += `
            <div style="font-size: 11pt; line-height: 1.6; color: #4a5568; white-space: pre-wrap; word-wrap: break-word;">
                ${escapeHtml(coche.descripcion)}
            </div>`;
                    } else {
                        html += `
            <div style="font-size: 11pt; color: #a0aec0; font-style: italic;">
                Sin descripción
            </div>`;
                    }
                    
                    html += `
        </div>`;
                });

                html += `
    </div>`;
                return html;
            }

            // Función para generar sección de Ahorros Conseguidos (agrupada)
            function generarSeccionAhorros(ahorros) {
                // Calcular suma total
                let sumaTotalAhorros = 0;
                ahorros.forEach(item => {
                    const precioActualEUR = item.precioActualEUR !== undefined ? item.precioActualEUR : parseFloat(item.precioActual || 0);
                    const precioNuevoEUR = item.precioNuevoEUR !== undefined ? item.precioNuevoEUR : parseFloat(item.precioNuevo || 0);
                    const unidadesAno = parseFloat(item.unidadesAno || 0);
                    const ahorroUnitarioEUR = precioActualEUR - precioNuevoEUR;
                    const ahorroTotal = ahorroUnitarioEUR * unidadesAno;
                    sumaTotalAhorros += ahorroTotal;
                });

                const sumaFormateada = new Intl.NumberFormat('es-ES', {style: 'currency', currency: 'EUR'}).format(sumaTotalAhorros);

                let html = `
    <div style="page-break-before: always; padding: 20pt 0;">
        <h1 style="font-size: 20pt; font-weight: bold; margin-bottom: 20pt; color: #667eea; border-bottom: 3px solid #667eea; padding-bottom: 10pt;">💰 Ahorros Conseguidos</h1>
        <p style="font-size: 11pt; color: #718096; margin-bottom: 20pt; font-style: italic;">
            Ahorros directos conseguidos en la feria y otros con productos que terminaremos comprando.
        </p>
        
        <div style="background: linear-gradient(135deg, #10b981 0%, #059669 100%); color: white; padding: 20pt; border-radius: 8px; margin-bottom: 25pt; text-align: center; box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);">
            <div style="font-size: 12pt; font-weight: 600; margin-bottom: 8pt; opacity: 0.95; text-transform: uppercase; letter-spacing: 1px;">💰 TOTAL AHORROS CONSEGUIDOS</div>
            <div style="font-size: 36pt; font-weight: 800; margin: 10pt 0; text-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);">${sumaFormateada}</div>
            <div style="font-size: 11pt; opacity: 0.9; margin-top: 5pt;">${ahorros.length} ${ahorros.length === 1 ? 'ahorro registrado' : 'ahorros registrados'}</div>
        </div>`;

                ahorros.forEach((ahorro, index) => {
                    const moneda = ahorro.moneda || 'EUR';
                    const precioActual = parseFloat(ahorro.precioActual || 0);
                    const precioNuevo = parseFloat(ahorro.precioNuevo || 0);
                    const precioActualEUR = ahorro.precioActualEUR !== undefined ? ahorro.precioActualEUR : precioActual;
                    const precioNuevoEUR = ahorro.precioNuevoEUR !== undefined ? ahorro.precioNuevoEUR : precioNuevo;
                    const unidadesAno = parseFloat(ahorro.unidadesAno || 0);
                    const ahorroUnitarioEUR = precioActualEUR - precioNuevoEUR;
                    const ahorroTotal = ahorroUnitarioEUR * unidadesAno;
                    const ahorroTotalFormateado = new Intl.NumberFormat('es-ES', {style: 'currency', currency: 'EUR'}).format(ahorroTotal);
                    const ahorroUnitarioFormateado = new Intl.NumberFormat('es-ES', {style: 'currency', currency: 'EUR'}).format(ahorroUnitarioEUR);
                    const unidadesFormateadas = unidadesAno.toLocaleString('es-ES');
                    
                    const precioActualOriginalFormateado = moneda === 'USD' 
                        ? new Intl.NumberFormat('en-US', {style: 'currency', currency: 'USD'}).format(precioActual)
                        : new Intl.NumberFormat('es-ES', {style: 'currency', currency: 'EUR'}).format(precioActual);
                    const precioNuevoOriginalFormateado = moneda === 'USD'
                        ? new Intl.NumberFormat('en-US', {style: 'currency', currency: 'USD'}).format(precioNuevo)
                        : new Intl.NumberFormat('es-ES', {style: 'currency', currency: 'EUR'}).format(precioNuevo);
                    const precioActualEURFormateado = new Intl.NumberFormat('es-ES', {style: 'currency', currency: 'EUR'}).format(precioActualEUR);
                    const precioNuevoEURFormateado = new Intl.NumberFormat('es-ES', {style: 'currency', currency: 'EUR'}).format(precioNuevoEUR);

                    html += `
        <div style="margin-bottom: 25pt; padding: 15pt; background-color: #f7fafc; border-left: 4px solid #10b981; border-radius: 4px;">
            <h3 style="font-size: 14pt; font-weight: bold; margin-bottom: 15pt; color: #2d3748;">
                ${index + 1}. ${escapeHtml(ahorro.empresa || 'Sin empresa')}
            </h3>
            
            <table style="width: 100%; border-collapse: collapse; margin-bottom: 15pt;">
                <tr>
                    <td style="width: 30%; padding: 8pt; font-weight: 600; color: #4a5568;">Producto:</td>
                    <td style="width: 70%; padding: 8pt; color: #2d3748;">${escapeHtml(ahorro.producto || 'N/A')}</td>
                </tr>
                <tr style="background-color: #ffffff;">
                    <td style="padding: 8pt; font-weight: 600; color: #4a5568;">Moneda:</td>
                    <td style="padding: 8pt; color: #2d3748;">${moneda === 'USD' ? 'USD (Dólar)' : 'EUR (Euro)'}</td>
                </tr>
                <tr>
                    <td style="padding: 8pt; font-weight: 600; color: #4a5568;">Precio Actual:</td>
                    <td style="padding: 8pt; color: #2d3748;">
                        ${precioActualOriginalFormateado}${moneda === 'USD' ? ` (≈ ${precioActualEURFormateado} EUR)` : ''}
                    </td>
                </tr>
                <tr style="background-color: #ffffff;">
                    <td style="padding: 8pt; font-weight: 600; color: #4a5568;">Precio Nuevo:</td>
                    <td style="padding: 8pt; color: #2d3748;">
                        ${precioNuevoOriginalFormateado}${moneda === 'USD' ? ` (≈ ${precioNuevoEURFormateado} EUR)` : ''}
                    </td>
                </tr>
                <tr>
                    <td style="padding: 8pt; font-weight: 600; color: #4a5568;">Unidades/Año:</td>
                    <td style="padding: 8pt; color: #2d3748;">${unidadesFormateadas} unidades</td>
                </tr>`;

                    if (moneda === 'USD' && ahorro.tasaCambio) {
                        html += `
                <tr style="background-color: #ffffff;">
                    <td style="padding: 8pt; font-weight: 600; color: #4a5568;">Tasa de Cambio:</td>
                    <td style="padding: 8pt; color: #2d3748;">1 USD = ${ahorro.tasaCambio.toFixed(4)} EUR</td>
                </tr>`;
                    }

                    html += `
            </table>
            
            <div style="background: #f0fdf4; padding: 15pt; border-radius: 8px; border: 2px solid #10b981; margin-top: 10pt;">
                <div style="font-size: 12pt; font-weight: 700; color: #166534; margin-bottom: 8pt;">💰 Ahorro Total Calculado (EUR)</div>
                <div style="font-size: 24pt; font-weight: 700; color: #166534; margin-bottom: 5pt;">${ahorroTotalFormateado}</div>
                <div style="font-size: 10pt; color: #059669;">
                    Ahorro unitario: ${ahorroUnitarioFormateado} × ${unidadesFormateadas} unidades
                </div>`;

                    if (moneda === 'USD') {
                        const ahorroTotalUSD = (precioActual - precioNuevo) * unidadesAno;
                        const ahorroTotalUSDFormateado = new Intl.NumberFormat('en-US', {style: 'currency', currency: 'USD'}).format(ahorroTotalUSD);
                        html += `
                <div style="font-size: 10pt; color: #059669; margin-top: 5pt;">
                    Original: ${ahorroTotalUSDFormateado} USD
                </div>`;
                    }

                    html += `
            </div>
        </div>`;
                });

                html += `
    </div>`;
                return html;
            }

            // NUEVOS COCHES - sección agrupada
            if (appData.nuevosCoches && appData.nuevosCoches.length > 0) {
                html += generarSeccionNuevosCoches(appData.nuevosCoches);
            }

            // AHORROS CONSEGUIDOS - sección agrupada
            if (appData.ahorros && appData.ahorros.length > 0) {
                html += generarSeccionAhorros(appData.ahorros);
            }

            // Cierre del documento
            html += `
    <div style="page-break-before: always; text-align: center; padding: 30pt 0; color: #718096;">
        <p>Fin del informe</p>
        <p style="font-size: 9pt; margin-top: 10pt;">Generado: ${new Date().toLocaleString('es-ES')}</p>
    </div>
</body>
</html>`;

            // Crear blob y descargar
            const blob = new Blob([html], { type: 'application/msword' });
            const fileName = `informe_seguimiento_${new Date().toISOString().split('T')[0]}.doc`;
            
            downloadFile(blob, fileName);
        }
        
        function downloadFile(blob, fileName) {
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = fileName;
            a.click();
            URL.revokeObjectURL(url);
        }
        
        // ========== SPLASH SCREEN FUNCTIONS ==========
        
        function initSplashScreen() {
            // Verificar si hay parámetro URL para DESACTIVAR splash
            const urlParams = new URLSearchParams(window.location.search);
            const skipSplash = urlParams.get('nosplash') === '1';
            
            console.log('🚀 Splash Screen Debug:', {
                skipSplash: skipSplash,
                willShow: !skipSplash
            });
            
            if (!skipSplash) {
                showSplash();
            } else {
                console.log('⏭️ Splash omitido por parámetro URL');
            }
        }
        
        async function showSplash() {
            console.log('🎬 Mostrando splash screen...');
            const splash = document.getElementById('splashScreen');
            
            if (!splash) {
                console.error('❌ No se encontró el elemento splashScreen');
                return;
            }
            
            splash.style.display = 'flex';
            
            // Generar partículas
            generateParticles();
            
            // Cargar datos del JSON para calcular estadísticas reales
            try {
                const response = await fetch('datos.json');
                const datos = await response.json();
                
                // Aplicar textos modificados (como en loadData)
                const textosModificados = JSON.parse(localStorage.getItem('textos_modificados_automechanika') || '{}');
                datos.reuniones.forEach(item => {
                    if (textosModificados[item.id]) {
                        Object.assign(item, textosModificados[item.id]);
                    }
                });
                datos.adicional.forEach(item => {
                    if (textosModificados[item.id]) {
                        Object.assign(item, textosModificados[item.id]);
                    }
                });
                
                // Aplicar seguimiento (para contar estados correctamente)
                const seguimientoData = JSON.parse(localStorage.getItem('seguimiento_v2_automechanika') || '{}');
                datos.reuniones.forEach(item => {
                    if (seguimientoData[item.id]) {
                        item.seguimiento = seguimientoData[item.id];
                    }
                });
                datos.adicional.forEach(item => {
                    if (seguimientoData[item.id]) {
                        item.seguimiento = seguimientoData[item.id];
                    }
                });
                
                // Aplicar fotos borradas
                const deletedPhotosData = JSON.parse(localStorage.getItem('deleted_photos_automechanika') || '{}');
                datos.reuniones.forEach(item => {
                    if (deletedPhotosData[item.id] && deletedPhotosData[item.id].length > 0) {
                        const deletedIndices = deletedPhotosData[item.id];
                        if (!item.fotos || !Array.isArray(item.fotos)) item.fotos = [];
                        item.fotos = item.fotos.filter((foto, idx) => !deletedIndices.includes(idx));
                    }
                });
                datos.adicional.forEach(item => {
                    if (deletedPhotosData[item.id] && deletedPhotosData[item.id].length > 0) {
                        const deletedIndices = deletedPhotosData[item.id];
                        if (!item.fotos || !Array.isArray(item.fotos)) item.fotos = [];
                        item.fotos = item.fotos.filter((foto, idx) => !deletedIndices.includes(idx));
                    }
                });
                
                // Calcular estadísticas reales (ahora con localStorage aplicado)
                const numEmpresas = datos.reuniones.length + datos.adicional.length;
                const numReuniones = datos.reuniones.length;
                const numOportunidades = [...datos.reuniones, ...datos.adicional].filter(item => (item.departamento || 'Lizarte') === 'Innovación').length;
                
                // Contar fotos totales (después de filtrar borradas)
                let numFotos = 0;
                datos.reuniones.forEach(item => {
                    numFotos += (item.fotos || []).length;
                    numFotos += (item.fotos_extra || []).length;
                });
                datos.adicional.forEach(item => {
                    numFotos += (item.fotos || []).length;
                    numFotos += (item.fotos_extra || []).length;
                });
                
                // Calcular ahorro total desde localStorage o appData
                let ahorroTotal = 0;
                let ahorros = [];
                
                // Primero intentar desde appData (si está disponible)
                if (appData && appData.ahorros && appData.ahorros.length > 0) {
                    console.log('💰 Ahorros encontrados en appData:', appData.ahorros.length);
                    ahorros = appData.ahorros;
                } else {
                    // Si no hay en appData, intentar desde localStorage
                    const ahorrosData = localStorage.getItem('ahorros_automechanika');
                    console.log('💰 Datos de ahorros en localStorage:', ahorrosData ? 'Existen' : 'No existen');
                    
                    if (ahorrosData) {
                        try {
                            ahorros = JSON.parse(ahorrosData);
                            console.log('💰 Ahorros cargados desde localStorage:', ahorros.length);
                        } catch (error) {
                            console.error('❌ Error parseando ahorros desde localStorage:', error);
                        }
                    }
                }
                
                if (ahorros && ahorros.length > 0) {
                    try {
                        console.log('💰 Ahorros parseados:', ahorros.length, 'items');
                        
                        // Convertir ahorros en USD a EUR si es necesario
                        const conversionPromises = ahorros.map(async (item, idx) => {
                            const moneda = item.moneda || 'EUR';
                            console.log(`💰 Ahorro ${idx + 1}:`, { moneda, precioActual: item.precioActual, precioNuevo: item.precioNuevo, unidadesAno: item.unidadesAno });
                            
                            if (moneda === 'USD' && (!item.precioActualEUR || item.precioActualEUR === 0)) {
                                // Convertir a EUR si no está convertido
                                console.log(`💰 Convirtiendo ahorro ${idx + 1} de USD a EUR...`);
                                const tasaCambio = await obtenerTasaCambioUSD();
                                item.precioActualEUR = parseFloat(item.precioActual || 0) * tasaCambio;
                                item.precioNuevoEUR = parseFloat(item.precioNuevo || 0) * tasaCambio;
                                item.tasaCambio = tasaCambio;
                                console.log(`✅ Ahorro ${idx + 1} convertido:`, { precioActualEUR: item.precioActualEUR, precioNuevoEUR: item.precioNuevoEUR, tasaCambio });
                            } else if (moneda === 'EUR') {
                                // Si es EUR, usar valores originales si no hay valores EUR guardados
                                if (item.precioActualEUR === undefined || item.precioActualEUR === null) {
                                    item.precioActualEUR = parseFloat(item.precioActual || 0);
                                }
                                if (item.precioNuevoEUR === undefined || item.precioNuevoEUR === null) {
                                    item.precioNuevoEUR = parseFloat(item.precioNuevo || 0);
                                }
                            }
                        });
                        
                        // Esperar a que todas las conversiones se completen
                        await Promise.all(conversionPromises);
                        
                        // Calcular total en EUR
                        ahorros.forEach((item, idx) => {
                            const precioActualEUR = item.precioActualEUR !== undefined && item.precioActualEUR !== null ? item.precioActualEUR : parseFloat(item.precioActual || 0);
                            const precioNuevoEUR = item.precioNuevoEUR !== undefined && item.precioNuevoEUR !== null ? item.precioNuevoEUR : parseFloat(item.precioNuevo || 0);
                            const unidadesAno = parseFloat(item.unidadesAno || 0);
                            const ahorroUnitarioEUR = precioActualEUR - precioNuevoEUR;
                            const ahorroItem = ahorroUnitarioEUR * unidadesAno;
                            console.log(`💰 Ahorro ${idx + 1} calculado:`, { precioActualEUR, precioNuevoEUR, unidadesAno, ahorroUnitarioEUR, ahorroItem });
                            ahorroTotal += ahorroItem;
                        });
                        
                        console.log('💰 Ahorro total calculado:', ahorroTotal);
                    } catch (error) {
                        console.error('❌ Error calculando ahorros:', error);
                    }
                } else {
                    console.log('⚠️ No hay ahorros en localStorage');
                }
                
                console.log('📊 Estadísticas calculadas:', {
                    empresas: numEmpresas,
                    reuniones: numReuniones,
                    fotos: numFotos,
                    oportunidades: numOportunidades,
                    ahorroTotal: ahorroTotal
                });
                
                // Iniciar animación de estadísticas con números reales después de 3 segundos
                setTimeout(() => {
                    animateStats(numEmpresas, numReuniones, numFotos, numOportunidades, ahorroTotal);
                }, 3000);
                
            } catch (error) {
                console.error('❌ Error cargando datos para splash:', error);
                // Fallback a números por defecto si hay error
                setTimeout(() => {
                    animateStats(36, 25, 80, 14, 0);
                }, 3000);
            }
            
            console.log('✨ Splash screen activado correctamente');
        }
        
        function generateParticles() {
            const container = document.getElementById('particlesContainer');
            const particleCount = 60;
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 8 + 's';
                particle.style.animationDuration = (Math.random() * 4 + 6) + 's';
                container.appendChild(particle);
            }
        }
        
        function animateStats(numEmpresas = 36, numReuniones = 25, numFotos = 80, numOportunidades = 14, ahorroTotal = 0) {
            const stats = [
                { id: 'stat1', target: numEmpresas, duration: 1500 },
                { id: 'stat2', target: numReuniones, duration: 1500 },
                { id: 'stat3', target: numFotos, duration: 1500 },
                { id: 'stat4', target: numOportunidades, duration: 1500 }
            ];
            
            stats.forEach((stat, index) => {
                setTimeout(() => {
                    animateNumber(stat.id, stat.target, stat.duration);
                }, index * 400);
            });
            
            // Animar el ahorro (valor monetario) después de las otras estadísticas
            setTimeout(() => {
                console.log('💰 Llamando animateAhorro con valor:', ahorroTotal);
                animateAhorro('stat5', ahorroTotal, 1500);
            }, stats.length * 400);
        }
        
        function animateAhorro(elementId, target, duration) {
            const element = document.getElementById(elementId);
            if (!element) {
                console.error('❌ No se encontró el elemento:', elementId);
                return;
            }
            
            console.log('💰 Animando ahorro:', { elementId, target, duration, tipo: typeof target });
            
            // Asegurar que target sea un número válido
            const targetNum = parseFloat(target) || 0;
            console.log('💰 Target numérico:', targetNum);
            
            // Asegurar que el valor inicial sea 0
            element.textContent = formatearMoneda(0);
            
            // Si el target es 0 o muy pequeño, mostrar directamente
            if (targetNum <= 0) {
                console.log('⚠️ Ahorro total es 0 o negativo, mostrando 0,00 €');
                element.textContent = formatearMoneda(0);
                return;
            }
            
            const start = 0;
            const increment = targetNum / (duration / 16);
            let current = start;
            
            console.log('💰 Iniciando animación desde', start, 'hasta', targetNum, 'con incremento', increment);
            
            const timer = setInterval(() => {
                current += increment;
                if (current >= targetNum) {
                    current = targetNum;
                    clearInterval(timer);
                    const ahorroFormateado = formatearMoneda(targetNum);
                    element.textContent = ahorroFormateado;
                    console.log('✅ Ahorro animado completado:', ahorroFormateado);
                    element.classList.add('glow');
                    setTimeout(() => element.classList.remove('glow'), 500);
                } else {
                    const ahorroFormateado = formatearMoneda(current);
                    element.textContent = ahorroFormateado;
                }
            }, 16);
        }
        
        function animateNumber(elementId, target, duration) {
            const element = document.getElementById(elementId);
            const start = 0;
            const increment = target / (duration / 16);
            let current = start;
            
            const timer = setInterval(() => {
                current += increment;
                if (current >= target) {
                    current = target;
                    clearInterval(timer);
                    element.classList.add('glow');
                    setTimeout(() => element.classList.remove('glow'), 500);
                }
                element.textContent = Math.floor(current);
            }, 16);
        }
        
        
        function autoResizeTextarea(textarea) {
            // Resetear altura para calcular correctamente
            textarea.style.height = 'auto';
            
            // Calcular altura necesaria
            const scrollHeight = textarea.scrollHeight;
            const minHeight = 40; // min-height del CSS
            
            // Detectar si es un campo de texto largo usando clase o atributo onchange
            const isLongTextField = textarea.classList.contains('auto-resize-textarea') ||
                                   textarea.classList.contains('long-text-field') ||
                                   (textarea.getAttribute('onchange') && 
                                   (textarea.getAttribute('onchange').includes("'comments'") ||
                                    textarea.getAttribute('onchange').includes("'notas'") ||
                                    textarea.getAttribute('onchange').includes("'oportunidad'")));
            
            // Para campos de texto largos, no aplicar límite máximo
            if (isLongTextField) {
                // Ajustar completamente al contenido sin límite
                textarea.style.height = Math.max(scrollHeight, minHeight) + 'px';
                textarea.style.overflowY = 'hidden'; // Sin scroll, todo visible
            } else {
                // Para otros campos, mantener el límite de 400px
                const maxHeight = 400;
            if (scrollHeight > minHeight) {
                textarea.style.height = Math.min(scrollHeight, maxHeight) + 'px';
            } else {
                textarea.style.height = minHeight + 'px';
            }
            
            // Si el contenido excede max-height, mostrar scroll
            if (scrollHeight > maxHeight) {
                textarea.style.overflowY = 'auto';
            } else {
                textarea.style.overflowY = 'hidden';
                }
            }
        }
        
        function addAutoResizeToAllTextareas() {
            document.querySelectorAll('textarea').forEach(textarea => {
                // Aplicar resize inicial
                autoResizeTextarea(textarea);
                
                // Añadir evento input para resize dinámico
                textarea.addEventListener('input', function() {
                    autoResizeTextarea(this);
                });
                
                // También resize cuando cambia el contenido programáticamente
                textarea.addEventListener('change', function() {
                    autoResizeTextarea(this);
                });
            });
        }

        function closeSplash() {
            console.log('🚪 Cerrando splash screen...');
            const splash = document.getElementById('splashScreen');
            splash.classList.add('fade-out');
            
            setTimeout(() => {
                splash.style.display = 'none';
                // NO guardamos en localStorage para que se muestre cada vez
                console.log('✅ Splash cerrado - Se mostrará de nuevo en la próxima visita');
            }, 1000);
        }
        
        // Modificar el event listener para incluir splash
        window.addEventListener('DOMContentLoaded', function() {
            loadData();
            initSplashScreen();
        });
    </script>
</body>
</html>
```
