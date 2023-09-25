echo "# SRI" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/CarlosAlvarezDiaz/SRI.git
git push -u origin main

Descarga la imagen 'httpd' y comprueba que está en tu equipo.
      $ docker pull httpd
        Using default tag: latest
        latest: Pulling from library/httpd
        Digest: sha256:5123fb6e039b83a4319b668b4fe1ee04c4fbd7c4c8d1d6ef843e8a943a9aed3f
        Status: Image is up to date for httpd:latest
        docker.io/library/httpd:latest
Crea un contenedor con el nombre 'asir_httpd'.
  
Mapea el puerto 80 del contenedor con el puerto 8000 de tu máquina.
Utiliza bind mount para que el directorio del apache2 'htdocs' este montado un directorio que tu elijas.

Realiza un 'hola mundo' en html y comprueba que accedes desde el navegador.

Crea un volumen para este mismo fin.

Crea un contenedor 'asir_web1' que use este volumen para el 'htdocs'
Utiliza Code para hacer un hola mundo en html
Crea otro contenedor 'asir_web2' con el mismo volumen y a otro puerto, por ejemplo 9080.
Comprueba que los dos servidores 'sirven' la misma página, es decir, cuando consultamos en el navegador:
        http://localhost:9080 
        http://localhost:8000
Tienen que salir la misma página web
