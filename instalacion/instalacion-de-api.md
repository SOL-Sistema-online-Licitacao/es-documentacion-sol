# Instalación de API

## Preparando el ambiente&#x20;

Es necesario instalar algunas herramientas. Haga clic en los enlaces a continuación para incitar a cada uno de ellos.

[![YARN](https://img.shields.io/badge/Yarn-2C8EBB.svg?style=for-the-badge\&logo=Yarn\&logoColor=white)](https://yarnpkg.com/cli/install)[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge\&logo=docker\&logoColor=white)](https://docs.docker.com/compose/install/#install-compose)[![NodeJS](https://img.shields.io/badge/node.js-%2343853D.svg?style=for-the-badge\&logo=node.js\&logoColor=white)](https://nodejs.org/en/)[![PM2](https://img.shields.io/badge/PM2-2B037A.svg?style=for-the-badge\&logo=PM2\&logoColor=white)](https://www.npmjs.com/package/pm2)

## Configuración del archivo de entorno (.env)&#x20;

Acceda al directorio raíz de la API y ejecute el siguiente comando:

```
λ docker-compose up -d
```

Cree un archivo `prod.env` en la carpeta `/env` de la API con el siguiente formato:

```
PORT=4002
NOSQL_CONNECTION_STRING=mongodb://localhost:20000/lacchain
JWT_KEY=secret_KEY
JWT_REFRESH_TOKEN_KEY=****************==
JWT_ACCESS_TOKEN_EXPIRATION=8h
JWT_REFRESH_TOKEN_EXPIRATION=7d
ENCRYPT_KEY=********-****-****-****-************
SENDGRID_EMAIL_SENDER=email@email.com
SENDGRID_API_KEY=******************

AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=******************
AWS_SECRET_ACCESS_KEY=**********/********/****

S3_BUCKET=dev-sol-app-api
S3_BUCKET_DOCUMENTS=dev-sol-app-api
S3_BUCKET_ANNOUNCEMENT_PHOTO=dev-sol-app-api                                    
```

Descrição dos parâmetros do arquivo env:&#x20;

<table><thead><tr><th width="378">Descrição</th><th>Parâmetro</th></tr></thead><tbody><tr><td>PORT</td><td>Puerto en el que se lanzará la API</td></tr><tr><td>NOSQL_CONNECTION_STRING</td><td>Cadena de conexión de la base de datos, aquí se debe agregar la ruta publicada por docker compose.</td></tr><tr><td>JWT_KEY</td><td>Clave utilizada para el cifrado JWT</td></tr><tr><td>JWT_REFRESH_TOKEN_KEY</td><td>Clave utilizada para verificar la autenticidad de los tokens de actualización de JWT</td></tr><tr><td>JWT_ACCESS_TOKEN_EXPIRATION</td><td>Tiempo de caducidad del token JWT</td></tr><tr><td>JWT_REFRESH_TOKEN_EXPIRATION</td><td>Tiempo de caducidad del token de actualización de JWT</td></tr><tr><td>ENCRYPT_KEY</td><td>Clave utilizada para el cifrado de carga útil. Debe ser generado por el usuario y debe estar de acuerdo con la interfaz.</td></tr><tr><td>SENDGRID_EMAIL_SENDER</td><td>Correo electrónico de origen para los servicios de SendGrid</td></tr><tr><td>SENDGRID_API_KEY</td><td>Clave utilizada para autenticar y autorizar el acceso a los recursos del servicio SendGrid</td></tr><tr><td>AWS_REGION</td><td>Región del servidor de AWS (Nulo si no se usa AWS)</td></tr><tr><td>AWS_ACCESS_KEY_ID</td><td>Clave de acceso de AWS</td></tr><tr><td>AWS_SECRET_ACCESS_KEY</td><td>Access Authenticator para servicios de AWS</td></tr><tr><td>S3_BUCKET</td><td>Cubo de almacenamiento de AWS (opcional, puede usar otro cubo)</td></tr><tr><td>S3_BUCKET_DOCUMENTS</td><td>Cubo de almacenamiento de AWS (opcional, puede usar otro cubo)</td></tr><tr><td>S3_BUCKET_ANNOUNCEMENT_PHOTO</td><td>Cubo de almacenamiento de AWS (opcional, puede usar otro cubo)</td></tr></tbody></table>

## Publicación de la API&#x20;

Acceda al directorio raíz de la API y ejecute el siguiente comando:

```
λ yarn publish:prod
```

Yarn creará un paquete que contendrá todo el código fuente del paquete, junto con el archivo "package.json" actualizado con la versión.

## Instalar PM2 en el servidor

&#x20;Documentación de PM2:

[https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/](https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/)

Ejecute el comando:

```
λ npm install pm2@latest -g
```

## Ejecutando PM2

Ejecute el comando:

```
λ pm2 start npm --name "sol-api-dev" -- run "start:dev"
```

## Ejecutar la semilla&#x20;

La semilla crea el usuario administrativo y una asociación.

```
λ yarn run seed
```
