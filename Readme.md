echo "# SRI" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/CarlosAlvarezDiaz/SRI.git
git push -u origin main

1 Descarga la imagen 'httpd' y comprueba que está en tu equipo.
      $ docker pull httpd
        Using default tag: latest
        latest: Pulling from library/httpd
        Digest: sha256:5123fb6e039b83a4319b668b4fe1ee04c4fbd7c4c8d1d6ef843e8a943a9aed3f
        Status: Image is up to date for httpd:latest
        docker.io/library/httpd:latest
2 Crea un contenedor con el nombre 'asir_httpd'.
3 Mapea el puerto 80 del contenedor con el puerto 8000 de tu máquina.
4 Utiliza bind mount para que el directorio del apache2 'htdocs' este montado un directorio que tu elijas.

            ~$ docker run -d -p 8000:80 --name asir_httpd -v "$PWD/htdocs":/usr/local/apache2/htdocs/ httpd
                  6e72f68ec0a5ddd91300912e70dbcc5269e0eacd481fcca9abecc501e9598e73
                  
Esto crea un contenedor llamado 'asir_httpd' que utiliza la imagen 'httpd' y mapea el puerto 80 del contenedor al puerto 8000 de tu máquina. Además, monta el directorio local 'htdocs' en el directorio '/usr/local/apache2/htdocs/' dentro del contenedor.

5 Realiza un 'hola mundo' en html y comprueba que accedes desde el navegador.

      ~$ docker run --rm -v "$PWD/htdocs":/usr/local/apache2/htdocs/ httpd /bin/sh -c "echo 'Hola Mundo' > /usr/local         /apache2/htdocs/index.html"

6 Crea un volumen para este mismo fin.

      ~$ docker volume create asir_web_volume asir_web_volume
      
7 Crea un contenedor 'asir_web1' que use este volumen para el 'htdocs'

      $ docker run -d -p 8080:80 --name asir_web1 -v asir_web_volume:/usr/local/apache2/htdocs/ httpd
      ce54662785d98b9c4a4c657e59961c16b872d3cbb6690e7d6334f20be2e9ef58

      Este contenedor utilizará el volumen que creamos para el directorio 'htdocs'.

8 Crea otro contenedor 'asir_web2' con el mismo volumen y a otro puerto, por ejemplo 9080.

      $ docker run -d -p 9080:80 --name asir_web2 -v asir_web_volume:/usr/local/apache2/htdocs/ httpd
      eb99b30f8cd35770eb4d8e355c79fd12bf07c2a53217c53a271153f9b4ff9bfe

9 Comprueba que los dos servidores 'sirven' la misma página, es decir, cuando consultamos en el navegador:
        http://localhost:9080 
        http://localhost:8000
10 Tienen que salir la misma página web

                Ambas URLs deberían mostrar la misma página web "Hola Mundo", ya que ambos contenedores están                          utilizando el mismo volumen que contiene los archivos HTML.

                  Con estos pasos, has creado dos contenedores que sirven la misma página web a través de diferentes                     puertos, utilizando un volumen compartido.
