> [!IMPORTANT]
> Este repositorio no contiene el código fuente del paquete **NPM survey-container**, sino que es una demo práctica que muestra cómo instalarlo, configurarlo y utilizarlo como dependencia en un proyecto real.
> Ambos repositorios **(desarrollo y demo)** están separados para evitar confusiones entre contribuir al paquete y simplemente consumirlo en tu proyecto.

Si estás buscando el repositorio del desarrollo del paquete, puedes encontrarlo aquí:

[![GITHUB](https://img.shields.io/badge/repositorio_de_desarrollo_de_survey_container-000000?style=for-the-badge&logo=github&logoColor=fff)](https://github.com/FernandoMejiaDev/survey-container)

[![GITHUB](https://img.shields.io/badge/Documentación-000000?style=for-the-badge&logo=github&logoColor=fff)](https://github.com/FernandoMejiaDev/Survey-Container-Documentation)

# Demo - Survey Container
Este repositorio es una **aplicación de demostración** que utiliza el paquete **NPM survey-container** como dependencia. Aquí encontrarás ejemplos claros y documentación sobre:

- Cómo instalar el paquete
- Cómo integrarlo en tu proyecto front-End
- Configuraciones necesarias en el Backend
- Base de datos

¿Qué incluye esta demo?
Esta demo fue construida utilizando el siguiente stack:

<div align="left">

![javascript](https://img.shields.io/badge/javascript-000000?style=for-the-badge&logo=javascript&logoColor=F7DF1E)
![react](https://img.shields.io/badge/react-000000?style=for-the-badge&logo=react&logoColor=61DAFB)
![tailwind](https://img.shields.io/badge/tailwind_css-000000?style=for-the-badge&logo=tailwindcss&logoColor=06B6D4)
![vite](https://img.shields.io/badge/vite-000000?style=for-the-badge&logo=vite&logoColor=646CFF)
![php](https://img.shields.io/badge/php-000000?style=for-the-badge&logo=php&logoColor=777BB4)
![mysql](https://img.shields.io/badge/mysql-000000?style=for-the-badge&logo=mysql&logoColor=4479A1)
![npm](https://img.shields.io/badge/dependencia_survey_container-000000?style=for-the-badge&logo=npm&logoColor=CB3837)

</div>

Este repositorio tiene como objetivo ayudarte a entender cómo implementar y usar el paquete **survey-container** en tu propio entorno. Toda la configuración necesaria está explicada paso a paso para que puedas adaptar esta solución a tus necesidades.

<details>
<summary>Cómo instalar el paquete</summary>

# Cómo instalar el paquete

Para instalar el paquete **survey-container**, simplemente abre tu terminal y ejecuta el siguiente comando:

```
npm i survey-container
```

Este paquete está publicado en **NPM**, donde también encontrarás esta misma documentación.

> *[NPM-survey-container](https://www.npmjs.com/package/survey-container)*

En esta demo, el paquete se instala desde la carpeta del frontend.

Entrando a la carpeta frontend

```
cd frontend
```

y instalando esta dependencia 

```
npm i survey-container
```

Una vez instalado, podrás verificar que se encuentra en tu archivo `package.json` como una dependencia, junto a su versión correspondiente. Actualmente, la versión estable más reciente es:

```
"survey-container": "^1.1.8"
```
> Asegúrate de mantener siempre el paquete actualizado a su última versión.

Esta demo se utilizó como entorno de prueba para detectar y corregir bugs en versiones anteriores del paquete.
Por ello, se recomienda **no instalar versiones antiguas**, ya que podrían contener errores que ya fueron corregidos en versiones recientes.

Una vez instalado correctamente, puedes integrarlo en el frontend de tu proyecto de **React.**
</details>

<details>
<summary>Cómo integrarlo en tu proyecto front-End</summary>

# Cómo integrarlo en tu proyecto front-End

Esta demo incluye dos páginas clave que muestran cómo integrar el paquete **survey-container:**

## Página de Métricas

Esta pantalla permite visualizar todas las encuestas disponibles en tu base de datos. En esta demo se utiliza **MySQL** como sistema de base de datos.

Puedes encontrar el código fuente de esta página en:

*[MetricsUi](https://github.com/FernandoMejiaDev/demo-survey-container/blob/main/frontend/src/components/ui/MetricsUi.jsx)*


La función principal aquí es obtener las métricas desde tu backend. Asegúrate de configurar correctamente la **URL** del `fetch`, como se muestra en el ejemplo:

`fetch("http://localhost:3000/api/metrics/metrics.php")`

cambiala por la **URL** de tú proyecto con esto te permitirá consultar y visualizar las métricas de tus encuestas o de lo contrario te mostrara el error en la consola.

![Demo-Image-1](https://github.com/FernandoMejiaDev/demo-survey-container/blob/main/readme/Readme-Image-1.png)

## Página para Contestar Encuestas

Esta es la sección que probablemente más te interesa: cómo usar el componente `SurveyWidget` que exporta el paquete.

El código de esta página se encuentra en:

*[SurveyUi](https://github.com/FernandoMejiaDev/demo-survey-container/blob/main/frontend/src/components/ui/SurveyUi.jsx)*

Aquí es donde se importa e integra el paquete **survey-container** en una aplicación real utilizando **React.**

Necesitas: 
- Importar el componente desde el paquete:
  
```
import { SurveyWidget } from "survey-container";
```

- Obtener el ID de la encuesta usando useParams():
```
const { surveyId } = useParams();
```
- Renderizar el componente `<SurveyWidget />` y pasarle los props necesarios como `surveyId`, `fetchUrl`, `responseUrl`.

## Props del componente SurveyWidget

El componente `<SurveyWidget />` acepta varios props para adaptar su comportamiento a distintos entornos y necesidades. A continuación te explicamos cada uno con base en cómo se utiliza en esta demo:

## Props utilizados en esta demo

```
<SurveyWidget
  surveyId={surveyId}
  fetchUrl="http://localhost:3000/api/surveys/survey.php?id="
  responseUrl="http://localhost:3000/api/response/postResponse.php"
  onAlert={(msg, type = "info") => {
    });
  }}
/>
```

## Explicación de cada prop

| Prop               | Tipo                               | Obligatorio | Descripción                                                                                                                                                                                                                                                                           |
| ------------------ | ---------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `surveyId`         | `string`                           | Sí        | Es el ID de la encuesta que quieres mostrar. En esta demo se obtiene desde la URL usando `useParams()`.                                                                                                                                                                               |
| `fetchUrl`         | `string`                           | Sí      | Es la URL base para hacer la solicitud **GET** y obtener los datos de la encuesta. Por ejemplo: `http://localhost:3000/api/surveys/survey.php?id=`. Se añadirá automáticamente el `surveyId` al final.                               |
| `responseUrl`      | `string`                           | Sí      | Es la URL donde se envían las respuestas con una solicitud **POST**.                                                                                                                                          |
| `onAlert`          | `(message: string, type?: string)` | No        | Función que se ejecuta para mostrar una alerta dependiendo del estado de la encuesta (error, éxito, advertencia). Puedes personalizarla como quieras (modal, toast, etc.). En esta demo se usa la librería *[react-toastify](https://fkhadra.github.io/react-toastify/introduction)*. |
| `apiUrl`           | `string`                           | No        | Si prefieres una URL base en lugar de `fetchUrl` o `responseUrl` individuales, puedes usar este prop como raíz para los endpoints `/surveys` y `/responses`. No se usa en esta demo.                                                                                                  |
| `onSubmit`         | `(responses) => Promise<void>`     | No        | Si quieres manejar tú mismo el envío de respuestas, puedes pasar tu propia función `onSubmit`. Si no se define, se hará un POST automáticamente a `responseUrl`.                                                                                                                      |
| `loadingText`      | `string`                           | No        | Texto que se muestra mientras la encuesta está cargando. Por defecto: `"Cargando encuesta..."`.                                                                                                                                                                                       |
| `submitButtonText` | `string`                           | No        | Texto del botón de envío. Por defecto: `"Enviar respuestas"`.                                                                                                                                                                                                                         |
| `className`        | `string`                           | No        | Clase CSS personalizada para aplicar estilos adicionales al contenedor del widget.                                                                                                                                                                                                    |

## ¿Por qué usar onAlert?

`onAlert` es muy útil si quieres notificar al usuario cuando:

- No ha respondido todas las preguntas (`warning`)
- Las respuestas se enviaron correctamente (`success`)
- Ocurrió un error al enviar (`error`)

En la demo se usó así, con `react-toastify`:

```
 onAlert={(msg, type = "info") => {
          toast(msg, {
            type,
            position: "top-right",
            autoClose: 3000,
            hideProgressBar: false,
            closeOnClick: true,
            pauseOnHover: true,
            draggable: true,
          });
        }}
      />
      <ToastContainer
        position="top-right"
        autoClose={3000}
        hideProgressBar={false}
      />
```
Pero puedes usar cualquier otra solución como **modals, alerts, banners, etc.**

Si todo está correctamente configurado, deberías ver en pantalla el contenido completo de la encuesta.  
En la demo, por ejemplo, se muestra una encuesta con preguntas sobre **Git** como referencia visual.

En los ejemplos proporcionados dentro del código y el **README**, verás URLs con **localhost**. Estas se usan únicamente para mostrar de forma clara cómo debe estructurarse cada endpoint.  

En tu propio proyecto puedes **(y se recomienda)** utilizar **variables de entorno** para manejar estas rutas y no exponerlas directamente en el código.

![Demo-Image-2](https://github.com/FernandoMejiaDev/demo-survey-container/blob/main/readme/Readme-Image-2.png)
</details>

<details>
<summary>Configuraciones necesarias en el Backend</summary>   

# Configuraciones necesarias en el Backend

## ¿Cómo funciona este paquete?
El paquete **survey-container** no es un paquete que funciona de forma independiente; requiere que tu proyecto tenga un backend funcional. Aunque el componente del frontend puede instalarse con NPM y usarse directamente en una app React, es obligatorio tener previamente configurado el backend para que funcione correctamente.

> Por eso **se recomienda primero preparar el backend antes de instalar la dependencia survey-container. Esto evitará errores, confusiones o que la encuesta no se muestre**.

## Tecnologías utilizadas en esta demo

Para esta demo se ha utilizado un backend en **PHP** puro junto con **MySQL.** Puedes usar cualquier tecnología backend que desees, pero este README explicará la configuración tal y como se muestra en la demo con **PHP puro.**

> no se utilizó Laravel ya que se trata de una demo simple que busca enseñar el uso del paquete.

## Configura tu base de datos

Debes crear una base de datos **MySQL, SQLite, postgresQL** y conectar tu backend a ella. En el ejemplo de esta demo se usa **MySQL**, puedes ver cómo se hace en el archivo:

*[config.php](https://github.com/FernandoMejiaDev/demo-survey-container/blob/main/backend/config.php)*

**Utiliza las variables de entorno por motivos de seguridad.**

## Archivos importantes del backend

En la carpeta `backend/` encontrarás:

- `config.php`: conexión a la base de datos.
- `composer.json` y `composer.lock`: archivos de configuración de Composer (por si deseas instalar librerías).
- Carpeta `api/`: contiene todas las rutas que el Frontend usará para comunicarse con el backend.

## Estructura de la carpeta api / configuración

Dentro de la carpeta `api/` se encuentran los archivos **PHP** necesarios para gestionar las encuestas, preguntas, respuestas y métricas. A continuación se muestra un resumen de su estructura:

```
api/
├── metrics/    
│   └── metrics.php           // Obtiene todas las encuestas
├── questions/    
│   └── questions.php         // Obtiene las preguntas de una encuesta
├── response/    
│   ├── getResponse.php       // Obtiene las respuestas
│   └── postResponse.php      // Guarda las respuestas
└── surveys/    
    ├── create.php            // Crea una nueva encuesta
    └── survey.php            // Obtiene una encuesta por ID
```

## Uso de metrics.php

El archivo *[metrics.php](https://github.com/FernandoMejiaDev/demo-survey-container/blob/main/backend/api/metrics/metrics.php)* es fundamental, ya que se encarga de traer todas las encuestas desde la base de datos para ser mostradas en el Frontend.

Si estás usando **PHP**, puedes copiar el código directamente, ya que está preparado para funcionar con la estructura esperada por este paquete.

> Más adelante en este README se explicarán las tablas necesarias en la base de datos para que todo funcione correctamente.

Si estás usando otro stack (por ejemplo, Express.js, Django, Laravel, etc.), puedes adaptar el comportamiento de estos archivos según tu tecnología.

# Nota importante
Aunque puedes copiar directamente los archivos **PHP** para facilitar la integración, **es necesario contar con ciertas tablas específicas en tu base de datos para que todo funcione correctamente.** Estas se detallan más adelante en el **README.**

</details>

<details>
<summary>Base de datos</summary>

# Base de datos

En este proyecto se utiliza **MySQL**, y dentro de la carpeta `database/` se incluye un archivo llamado *[schema.sql](https://github.com/FernandoMejiaDev/demo-survey-container/blob/main/database/schema.sql)* que contiene todas las instrucciones necesarias para crear las tablas requeridas.


Si planeas clonar o adaptar este proyecto, puedes usar directamente el archivo *[schema.sql](https://github.com/FernandoMejiaDev/demo-survey-container/blob/main/database/schema.sql)* o copiar el siguiente código **SQL** para crear las tablas:

```
CREATE TABLE IF NOT EXISTS Survey (
  id VARCHAR(36) PRIMARY KEY,
  qualification VARCHAR(255) NOT NULL
);

CREATE TABLE IF NOT EXISTS Question (
  id VARCHAR(36) PRIMARY KEY,
  text TEXT NOT NULL,
  surveyId VARCHAR(36),
  FOREIGN KEY (surveyId) REFERENCES Survey(id) ON DELETE CASCADE
);

CREATE TABLE IF NOT EXISTS Response (
  id VARCHAR(36) PRIMARY KEY,
  content TEXT NOT NULL,
  questionId VARCHAR(36),
  FOREIGN KEY (questionId) REFERENCES Question(id) ON DELETE CASCADE
);

```

Estas tablas representan:

- `Survey`: Almacena las encuestas creadas.
- `Question`: Contiene las preguntas asociadas a cada encuesta.
- `Response`: Guarda las respuestas enviadas por los usuarios.

Ruta del archivo **SQL**:

*[schema.sql](https://github.com/FernandoMejiaDev/demo-survey-container/blob/main/database/schema.sql)*

</details>

<div align="left">

[![NPM](https://img.shields.io/static/v1?message=Paquete-NPM&logo=NPM&label=&color=CD3E3D&logoColor=white&labelColor=&style=for-the-badge)](https://www.npmjs.com/package/survey-container)
[![GITHUB](https://img.shields.io/static/v1?message=Repositorio-de-desarrollo-de-survey-container&logo=Github&label=&color=22262A&logoColor=white&labelColor=&style=for-the-badge)](https://github.com/FernandoMejiaDev/survey-container)
[![WORDPRESS](https://img.shields.io/static/v1?message=página-de-documentación&logo=WordPress&label=&color=1790c8&logoColor=white&labelColor=&style=for-the-badge)](https://surveycontainer.wordpress.com/)

</div>

---
