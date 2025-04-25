**🌍CONTEXTO DE PROYECTO**

La **PokeDex** es una aplicación desarrollada por **Pueblo Paleta Inc.** que permite a los usuarios explorar información detallada sobre diferentes especies de Pokémon, incluyendo sus características, habilidades, estadísticas y evoluciones. Esta herramienta está diseñada para ser accesible desde cualquier dispositivo, ofreciendo una experiencia interactiva y visualmente atractiva.

🎯**Objetivo de despliegue**

Desplegar la **PokeDex** en un entorno cloud público (**Azure**) de manera segura, escalable y accesible.

**🔧 Requisitos Previos**
 1. cuenta de azure
 2. cuenta de GitHub 
 3. codigo fuente de pokedex
 
 
*Luego de conocer que es pokedex, el objetivo principal y algunos de los requisitos necesarios para llevar a cabo la realizacion del proyecto.Miremos los pasos a seguir para culminar con éxito*

## **🚀Paso a paso para desplegar en Azure**

### *1. Hacer Fork del Código Fuente Original.*

Antes de desplegar la aplicación, es necesario hacer un **fork** del repositorio original proporcionado por el profesor. Esto nos permitirá tener una copia propia del proyecto en GitHub, la cual podremos conectar directamente con Azure.

#### 📥 Fuente Oficial del Código

Repositorio original del profesor:  
[https://github.com/rcuello/ac4dem1a](https://github.com/rcuello/ac4dem1a)

Ruta específica del proyecto dentro del repositorio:  
`./sistemas-distribuidos/poke-dex-lab/source/pokedex-angular`

----------

#### 🧭 Pasos para realizar el Fork correctamente

1.  Ve al repositorio del profesor:  
    👉 [https://github.com/rcuello/ac4dem1a](https://github.com/rcuello/ac4dem1a)
    
2.  Haz clic en el botón **Fork** para crear una copia del repositorio en tu cuenta de GitHub.
    
3.  Una vez realizado el fork, ingresa a tu nueva copia en tu perfil de GitHub.
    
4.  Dirígete a la carpeta específica del proyecto que se desea desplegar:  
    `sistemas-distribuidos/poke-dex-lab/source/pokedex-angular`
   
       *Copia localmente esa carpeta (`pokedex-angular`) y crea un nuevo repositorio en GitHub que contenga únicamente ese código.*
       
***2.  Crear un grupo de recursos.🗂️***
 -    En el portal azure, busca  ***"Grupos de recursos"***  y haz clic en  **"+ *Crear*"**.
 -   Asigna un nombre (ej:  `grupopoke`) 
 -   Haz clic en  *****"Revisar + crear"*****  y luego en  ***"Crear"***
 
***3. Crear una App Web (App Service)🌐***
-   En el buscador, escribe **"App Services"**.
    
-   Haz clic en **Crear** > **Web App**.
    
-   Llena el formulario:
    
    -   **Suscripción**: Azure for Students
        
    -   **Grupo de recursos**: `grupopoke`
        
    -   **Nombre de la app**: `pokemon-mtg` (esto será parte de la URL final)
        
    -   **Publicar**: Código
        
    -   **Pila de ejecución**: HTML (o Node.js si fuera necesario)
        
    -   **Región**: la misma que el grupo de recursos
        
-   En "Plan de App Service", selecciona el plan gratuito (F1).
    
-   Haz clic en **Revisar y crear** > **Crear**.

***4. Configurar el Despliegue desde GitHub  ⚙️🚀***

1.  Una vez creada la app, ve al recurso `pokemon-mtg` desde el portal.
    
2.  En el menú lateral, haz clic en **Deployment Center**.
    
3.  Fuente: **GitHub**
    
4.  Organización: tu usuario
    
5.  Repositorio: tu fork del PokeDex
    
6.  Rama: `main` o la que estés usando
    
7.  Tipo de construcción: **HTML (sin build automation)**
    
8.  Confirma y guarda los cambios.
### *5. Verificar el Despliegue✅*
1.  Espera unos minutos mientras Azure clona y despliega tu repositorio.
    
2.  Cuando el despliegue finalice, haz clic en el enlace de la app (algo como `https://pokemon-mtg.azurewebsites.net`)
    
3.  Verifica que la aplicación cargue correctamente.
### *6. Encabezados de Seguridad.🔐*

  *Al desplegar la aplicación por primera vez, se detectó que **faltaban encabezados de seguridad importantes** como `Content-Security-Policy`, `X-Frame-Options`, `HSTS`, etc.*
    
-   Al realizar un escaneo en [securityheaders.com](https://securityheaders.com), la aplicación obtuvo una calificación de **C**, e detectó que **faltaban encabezados de seguridad importantes** como `Content-Security-Policy`, `X-Frame-Options`, `HSTS`, lo cual era insuficiente según los requisitos del caso de uso.Para solucionar esto y tener un nuevo resultado en cuanto a seguridad fue necesario seguir los siguientes pasos:

### *1. Crear el archivo de configuración para encabezados.*

#### Opción usada: `staticwebapp.config.json` **(aplicable para apps estáticas o configuraciones personalizadas en Azure)**

-   Se creó un archivo llamado `staticwebapp.config.json` en la raíz del proyecto.
Este archivo contiene directivas de encabezados HTTP a nivel global y se ve así:


**{*
  "globalHeaders": {
    "Content-Security-Policy": "default-src 'self' https://pokeapi.co; connect-src *; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; img-src * data:; font-src 'self' https://fonts.gstatic.com;",
    "X-Frame-Options": "DENY",
    "Permissions-Policy": "geolocation=(), camera=(), microphone=()",
    "Strict-Transport-Security": "max-age=63072000; includeSubDomains; preload"
  },
  "navigationFallback": {
    "rewrite": "/index.html"
  }
}*
### ¿Qué hace cada encabezado?📝

Se añadieron encabezados HTTP clave para mejorar la seguridad. El `Content-Security-Policy` limita las fuentes desde las que se puede cargar contenido, reduciendo el riesgo de ataques XSS. El `X-Frame-Options` evita que la app sea embebida en iframes, protegiendo contra clickjacking. Con `Permissions-Policy` se desactivan funciones como geolocalización, cámara y micrófono que no son necesarias. Finalmente, `Strict-Transport-Security` obliga al navegador a usar HTTPS en todas las visitas futuras, lo cual fortalece la seguridad general de las conexiones.
### *2. Subir el archivo al Repositorio.*

-   Se agregó `staticwebapp.config.json` al directorio raíz del proyecto.
    
-   Se hizo commit y push al repositorio para que Azure lo detectara automáticamente en el despliegue.
- ### ***3. Verificar en Azure.✅***

-   Una vez desplegada la nueva versión, se reinició manualmente la app desde el portal de Azure para asegurar que tomara los nuevos headers.
    
-   Se verificó que los encabezados estuvieran activos usando herramientas como:
    
    -   Las herramientas de desarrollador del navegador (pestaña _Network_ > _Headers_)
    -   
## ***RESULTADOS DE SEGURIDAD🔐***

   - **La aplicación ahora incluye encabezados de seguridad críticos.**
    
-   **Se volvió a escanear en [securityheaders.com](https://securityheaders.com) y se obtuvo una calificación de** **A**.**
        
   
##  ***RESULTADOS DE LA APLICACION🌐.***

**-   La aplicación PokeDex está accesible desde una URL pública de Azure.**
    
**-   Se despliega automáticamente desde GitHub.**
    
**-   El sitio cumple con estándares básicos de seguridad según el escaneo de SecurityHeaders.**


## *****CONCLUSION CASO DE ESTUDIO POKEDEX**🔚*** 

**El proyecto logró desplegar exitosamente la aplicación PokeDex en Azure, integrando buenas prácticas de seguridad y automatización mediante GitHub. Se mejoró la calificación de seguridad y se garantizó el acceso público, cumpliendo con los requisitos técnicos del caso de uso.**



   
   



