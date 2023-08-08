# Instalación de interfaz

## Preparando el ambiente&#x20;

Es necesario instalar algunas herramientas. Haga clic en los enlaces a continuación para incitar a cada uno de ellos.

[![YARN](https://img.shields.io/badge/Yarn-2C8EBB.svg?style=for-the-badge\&logo=Yarn\&logoColor=white)](https://yarnpkg.com/cli/install)[![NodeJS](https://img.shields.io/badge/node.js-%2343853D.svg?style=for-the-badge\&logo=node.js\&logoColor=white)](https://nodejs.org/en/)

## Configuración del archivo de entorno (.env)&#x20;

En el directorio `src/enviroments/` es necesario cambiar el archivo `environment.prod.ts.`

<figure><img src="../.gitbook/assets/arquivos (1).webp" alt=""><figcaption></figcaption></figure>

Cambiar parámetros:

```
encrypt_key: a mesma utiliazada na API
api server e port
```

## Publicando la interfaz con Nginx&#x20;

Acceda al directorio raíz de la API y ejecute el siguiente comando:

<pre><code><strong>λ ng build --c production
</strong></code></pre>

### Configurar nginx&#x20;

Puede verificar que nginx está funcionando con:

```
sudo systemctl restart nginx
sudo systemctl status nginx
```

### CONFIGURACIÓN NGINX&#x20;

La configuración en la sección anterior es tan simple como parece. Escuchará en el puerto HTTP 80 cualquier nombre de host que aún no haya sido interceptado. Idealmente, especifique un nombre\_servidor, agregue SSL, redirija HTTP a HTTPS.&#x20;

También puede considerar redirigir no-www a www, agregar almacenamiento en caché o incluir limitación de velocidad.&#x20;

Nginx puede hacer todas estas cosas.

```
# /etc/nginx/conf.d/mysife.conf

server {
  listen 0.0.0.0:80;
  root /srv/mysite;
  location / {
    try_files $uri $uri/ /index.html;
  }
}
```
