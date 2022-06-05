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
      - /opt/test:/var/lib/mysql
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



