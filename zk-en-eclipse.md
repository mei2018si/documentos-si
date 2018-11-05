# Apache Tomcat
Las aplicaciones ZK se despliegan en un servidor de aplicaciones Java EE (en realidad basta un contenedor de Servlets)
* Apache Tomcat9 es un contenedor de Servlets compatible con la especificación 3.0

## Descarga e instalación
* Descarga Tomcat 9 desde [https://tomcat.apache.org/download-90.cgi]
* Descomprimir servidor
```
tar xzvf apache-tomcat-9.0.12.tar.gz 
```
* Establecer usuario administrador (`tomcat` con contraseña`purple2018`)
```
cd apache-tomcat-9.0.12/
nano conf/tomcat-users.xml 
```
Añadir
```xml
...
<tomcat-users>
   ...
   <user username="tomcat" password="purple2018" roles="manager-gui,namager-script,admin-gui,admin-script"/>
</tomcat-users>
```

* Arranque y parada del servidor
Inicio manual del servidor
```
bin/startup.sh
```
Parada manual del servidor
```
bin/shutdown.sh
```

* Servidor disponible en la URL http://localhost:8080

* Despliegue de aplicaciones http://localhost:8080/manager
   1. Desde la consola de administrador

   2. Desde línea de comandos, copiando el paquete WAR en el directorio `webapps`

   Ejemplo descargar y descomprimir `zk-sandbox.war` desde [zk-8.5.0](http://https://sourceforge.net/projects/zk1/files/ZK/zk-8.5.0)
   ```
   
   mv zkoos-demo.war  webapps
   ```
   Acceder a http://localhost:8080/zk-demo

Más información: https://tomcat.apache.org/tomcat-9.0-doc/

## Integración de Tomcat en Eclipse

### Registrar Tomcat 9 como servidor de aplicacione en Eclipse
* Acceder a `Window > Preferences > Server > Runtime Environments
Add`

* Seleccionar `"Apache Tomcat v9.0"` y fijar:
     ```
     Tomcat instalation directory : [ruta a apache-tomcat-9.0.12]
     JRE:                           seleccionar el que use o dejar "workbench defualt JRE"
     ```
     
En los proyectos Eclipse de tipo Web , el servidor estará disponible en:
```Proyecto [botón derecho] > Run As > Run on Server``
(marcar `"Always use this server when running this project"` en el primer uso del servidor)


# Uso de ZK Framework en Eclipse

## Añadir arquetipos Maven de ZK Framework
* Desde `Window > Preferences > Maven > Archetypes`
  Fijar en `Add Remote Catalog`:
  ```
  Catalog file: http://mavensync.zkoss.org/maven2/
  Description:  Arquetipos ZK
  ```

## Crear con Maven un proyecto Web ZK 
* Desde `File > New > Maven Project`
   Seleccionar:
   ```
   groupId:     org.zkoss
   archetypeId: zk-archetype-webapp
   version:     8.5.0
   ```

## Importar proyectos Maven ZK en Eclipse
* Importar en Eclipse desde `File > Import > Maven > Exiting Maven Projects`

Dependiendo de la versión de Eclipse pueden ser necesarios pasos adicionales para que Eclipse reconozca el proyecto como de tipo Web y le vincule la posibilidad de ejcutarlo en un servidor de aplicaciones (con `proyecto [botón derecho] > Run As > Run on Server`)

1. Vincular "facetas" al proyecto

    * Sobre el proyecto `[botón derecho] > Properties > Project Facets` 
    * Seleccionar `"Dynamic Web Module"`, `"Java"`  y `"JavaScript"` (también `"ZK Studio Supports"` si está disponible)
    * (opcional) En la pestaña `"Runtimes"`se puede vincular el proyecto con el Servidor tomcat9)
   
   Como resultado, estará disponible `"Run As > Run on Server"`

2. Especificar cómo se realizará el empaquetado para el despliegue (indicando los ficheros del proyecto y su ubicación en el WAR final)
    * Sobre el proyecto `[botón derecho] > Properties > Deployment Assembly`

      Dejar la configuración con
          ```
          Source         		Deploy Path
          /src/main/java	    WEB-IN/classes       (seleccionar como tipo "Folder")
          /src/main/webapp	    /                  (seleccionar como tipo "Folder")
          Maven Dependencies	WEB-IN/lib           (seleccionar como "Java Build Path Entries")
          ```
       
       En `Advanced`, indicar en `Folder for deployment descriptor` el valor `/src/main/webapp`


## Instalación de ZK Studio

* Desde `Help > Eclipse Marketplace`
* Buscar `ZK Studio`
* Instalar version 2.3.0 y reiniciar Eclipse
* Requiere registro en [www.zkoos.org](http://forum.zkoss.org/account/signup/?login_provider=local) y activación 
     Desde `Window > Preferences > ZK > ZK Account > [Activate]`
     
* Se dispone de "ZUL editor", "ZK prespective" (con ZUL palette), asistentes para creación de proyectos ZK, etc

