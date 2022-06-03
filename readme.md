# tips och trix

**I detta repo kan vi fylla på med våra tips och trix från våra "container workshops"**  👍😃

*Du behöver installera [Docker Desktop](https://www.docker.com/products/docker-desktop/) för att följa med i dessa övningar.*

## db's i containers för lokal utveckling

### Postgres med 'docker run'
```docker run -p 5432:5432 --name postgres -e POSTGRES_PASSWORD=hemligt -d postgres```   
detta startar en postgres instans med default användaren ``postgres`` och lösenordet ``hemligt``. 
porten 5432 inne i containern mappas till din localhost (din dators) port 5432.  

Nu kan du jobba med denna databas med DBeaver eller liknande som om den vore installerad lokalt på din dator.

läs mer här: https://hub.docker.com/_/postgres

### MSSQL med 'docker run'
```docker run --name mssql -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=BareKNuckles10" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest```  
detta startar en mssql instans med sa användaren och lösenordet BareKNuckles10. porten 1433 inne i containern mappas till din localhost på 1433.   

Nu kan du jobba md denna databas med mgmt studio eller liknande som om den vore installerad lokalt på din dator.

läs mer här: https://hub.docker.com/_/microsoft-mssql-server



**PS:** Du kan:

- lista vilka containers som körs just nu med ``docker ps``  
- stoppa en container med ``docker stop < container-namet >``  
- När du stoppat en container kan du raderad den med ``docker rm < container-namet >`` 
- se loggarna från en container med ``docker logs < container-namet >`` 
- taila logganra från en container med ``docker logs < container-namet > -f `` 

### Postgres eller MSSQL med **docker-compose** (inkl beständiga volymer (persistent data volumes))

1. navigera till ./localdb/compose
2. navigera in i foldern ``mssql`` eller ``postgres``
3. kör ```docker-compose up -d```  
Nu kör din databas med samma credentials som i docker-run-exemplet ovan fast data persisteras utanför din container. Kika på docker-compose filen i respektive folder! Notera även **restart: always**... med denna setting kommer din databas (tex) att startas automatisk med docker-desktop som i sin tur kan starta med windows...

**PS:** Du kan:
- stoppa en databas som körs med docker-compose med ``docker-compose stop``   
- du kan radera en databas INKL datavolymen med ``docker-compose down -v`` 
