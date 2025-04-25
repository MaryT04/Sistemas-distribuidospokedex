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
una vez creada la cuenta de azure
**Paso 1: Configuración del entorno de Azure:** 
***1. Crear un grupo de recursos:***
 -    En el portal, busca  ***"Grupos de recursos"***  y haz clic en  **"+ *Crear*"**.
 -   Asigna un nombre (ej:  `Pokedex`) 
 -   Haz clic en  *****"Revisar + crear"*****  y luego en  ***"Crear"***
 
 
 ***2. **Desplegar un App Service:*****
 
 -   Busca  **"App Services"**  en el portal y haz clic en  **"+ Crear"**.
 - Configura los siguientes parámetros:
    -   **Suscripción**: Selecciona tu suscripción gratuita.
        
    -   **Grupo de recursos**:  `grupopoke`  
        
    -   **Nombre**:  `pokemon-mtg`  
        
    -   **Región**: La misma que el grupo de recursos.
        
    -   **Plan de precios**: Selecciona el plan  **F1 Free**  (gratuito).
        
-   Haz clic en  **"Revisar + crear"**  y luego en  **"Crear"**.

**Paso 2:  **Hacer Fork del Repositorio Original****
 ***1.* *Clonar el repositorio de GitHub***:Accede al repositorio original de la Pokedex
  ***2. Haz clic en el botón "Fork"*** (esquina superior derecha)
 ****3.Selecciona tu cuenta personal****  como destino del fork
    - GitHub creará una copia idéntica del repositorio en tu perfil.
    
   **Paso 3: **Desplegar la aplicación en Azure****
   
