# modulo7_cloud_laboratorio_ejercicio2

1. Instalamos gh-pages en nuestro proyecto y declaramos los scripts necesarios para hacer la build y el deploy:

![scripts](https://github.com/user-attachments/assets/41acd91d-28c8-434a-9f76-6b7cc575ad67)

2. Creamos el workflow dentro .github/workflows/cd.yml en la raiz de nuestro proyecto con el fin de automatizar el proceso de deploy una vez que hagamos un push.
  Este archivo se encarga:
  -  Chequea nuestro repositorio para que el workflow pueda acceder a él.
  -  Almacena la clave privada de ssh la cual se encuentra en nuestra configuracion de github y la pasa a un archivo de nuestra instacia de linux para luego usarla
  -  Le dice a git el nombre y el email con el que se tiene que autentificar, ya que luego necesitaremos credenciales para realizar el deploy
  -  Realiza un npm install
  -  Genera la build de la aplicacion
  -  Realiza el deploy de la build. Para ello se autentifica mediante ssh con nuestro repo, crea la rama gh-pages, sube la build y a continuacion ejecuta un actions que acaba generando el deploy.
Todo ello aprovechando los comandos que hemos declarado en nuestro package.json, los cuales la instancia de linux tiene acceso.

![imagen](https://github.com/user-attachments/assets/3f42b1e0-4c31-49b8-b1eb-16123fdae309)

3. En nuestro proyecto creamos la clave ssh con el siguiente comando: 
  ssh-keygen -m PEM -t rsa -C "cd-user@my-app.com"

4. Añadimos la clave publica a nuestro repo de github, para ello nos vamos a la siguiente ventana:
   Repo > Settings > Deploy keys > Add deploy key
   
![imagen](https://github.com/user-attachments/assets/8e6b6787-3240-4993-a2b3-318dbdb259e1)

5. Añadimos la clave privada como un secret a nuestro github:
   Repo > Settings > Secrets and variables > Actions > New repository secret
   
![imagen](https://github.com/user-attachments/assets/e2e7e4d0-baee-41d7-8e05-658edf89cdeb)

Una vez añadida la eliminamos de nuestro proyecto.

6. Cuando añadamos cambios sobre nuestra rama main, se ejecutará tanto el workflow "cd" con sus actions como el action de gh-pages:

 ![imagen](https://github.com/user-attachments/assets/c2cf4b20-f1fe-4b31-b950-89e6c2b4732f)
 
 ![imagen](https://github.com/user-attachments/assets/3894579a-01e7-4bf4-97cf-e5b1e0aa7ba2)

Url despliegue:
https://oskweb.github.io/modulo7_cloud_laboratorio_ejercicio2/#/orders


