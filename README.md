###### Autores: Francisco José Almansa Martínez, Belén Gamero García y Marc Sancho Santandreu

# Despliegue del Proyecto en Docker

## [DockerHub](https://hub.docker.com/r/marcsancho00/pokemon)

## Docker-Compose
Tenemos que realizar un archivo **.yml** para hacer el Docker-Compose.

<sup> Resultado: </sup>

```
version: '3.3'
services:
  db:
    image: mysql:8.0
    volumes:
      - ./test:/var/lib/mysql
      - ./BD:/docker-entrypoint-initdb.d
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: pokedexdb
      MYSQL_USER: fran
      MYSQL_PASSWORD: 123456Fran
    ports:
      - 3307:3306
  phpmyadmin:
    depends_on:
      - db
    image: phpmyadmin/phpmyadmin
    ports:
      - '8081:80'
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: root
  web:
    depends_on:
      - db
    image: tomcat:10.0
    volumes:
      - ./PokemonFBM.war:/usr/local/tomcat/webapps/PokemonFBM.war
    ports:
      - '8080:8080'
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: pokedexdb
      MYSQL_USER: fran
      MYSQL_PASSWORD: 123456Fran
```

## Procedimiento a realizar

Empezamos clonando el proyecto a nuestra carpeta <br>
![image](https://user-images.githubusercontent.com/91566044/172072376-181eee78-b6ae-495f-8b32-5298884d747b.png)

Se realiza el docker-compose <br>
![image](https://user-images.githubusercontent.com/91566044/172072393-51a61bdd-a57f-4127-92f2-f52c314951b7.png)

Vemos como una vez finalizado el docker-compose, ya estan iniciados los contenedores <br>
![image](https://user-images.githubusercontent.com/91566044/172072464-e1cb48df-6cf4-4484-a292-fcc4eb4834a6.png)

Y si vamos a http://localhost:8080/PokemonFBM podemos encontrar la pagina
![image](https://user-images.githubusercontent.com/91566044/172072509-8a769e58-749c-4381-b28e-294804ecbe52.png)

![image](https://user-images.githubusercontent.com/91566044/172071617-769e9023-6378-46ff-8770-f7a613e13077.png)

![image](https://user-images.githubusercontent.com/91566044/172071576-672c1ab7-a88d-4ffc-89c2-66107d619c64.png)

![image](https://user-images.githubusercontent.com/91566044/172071425-5286eb54-0695-430c-89a2-2b014504f445.png)
