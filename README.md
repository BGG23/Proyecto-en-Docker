###### Autores: Francisco José Almansa Martínez, Belén Gamero García y Marc Sancho Santandreu

# Despliegue del Proyecto en Docker

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

## Resultado del Docker-Compose
![image](https://user-images.githubusercontent.com/91566044/172071617-769e9023-6378-46ff-8770-f7a613e13077.png)

![image](https://user-images.githubusercontent.com/91566044/172071576-672c1ab7-a88d-4ffc-89c2-66107d619c64.png)

![image](https://user-images.githubusercontent.com/91566044/172071425-5286eb54-0695-430c-89a2-2b014504f445.png)

[DockerHub](https://hub.docker.com/r/marcsancho00/pokemon)
