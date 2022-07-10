# 1. videoconvert-in-serverless-lambda

El backend en este repositorio es una aplicación que esta construida con **AWS S3, MediaConvert, Lambda,** y su funcionalidad principal es transcodificar un video en diferentes formatos.

Cabe aclarar que esta aplicacion esta construida sobre serverless y es altamente escalable.

## 2. Flujo de la aplicación.

- El usuario carga un video directamente al buckert S3
- Al estar cargado el video se dispara un trigger.
- A la lambda le llega un evento con información sobre el video que se cargo.
- Al ejecutarse la lambda, se le envia un job al servicio AWS MediaConvert para que sepa que hacer. 
- El servicio AWS MediaConvert recibe el job con el tipo de conversión que debe hacer y donde debe dejar los videos con los nuevos formatos, para este caso son tres (3) formatos que vamos a manejar con diferentes resoluciones, tasa de bit, etc.
- Luego de eso se enviar lso video al bucket de salida, este proceso puede tardar minutos o horas dependiendo de la calidad, duración u otras caracteristicas del video.
- Al final del flujo se dejan los tres (3) videos en el bucket S3 con las especificaciones que se le indico desde la lambda.

![](resources/diagram.png)

## 2. Colocando todo en marcha.

Voy a asumir que ya tienes NPM y Node js instalado en tu maquina, vamos a proceder a instalar Serverless Framework.

Serverless Framework es una herramienta de linea de comando que te permite desarrollar y supervizar facilmente aplicaciones serverless.

Para instalar solo tienes que ejecutar el siguiente comando:

> npm install -g serverless

Ya teniendo servlerless instalado, procede a clonar este repositorio y te ubicas dentro de la carpeta del mismo.

