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

* Servidor disponible en la URL [http://localhost:8080](http://localhost:8080)

* Despliegue de aplicaciones 
   1. Desde la consola de administrador en [http://localhost:8080/manager](http://localhost:8080/manager)

   2. Desde línea de comandos, copiando el paquete WAR en el directorio `webapps`

Más información: https://tomcat.apache.org/tomcat-9.0-doc/

## Integración de Tomcat en Eclipse
Se requiere la edición [Eclipse IDE for Java EE Developers](https://www.eclipse.org/downloads/packages/release/2018-09/r/eclipse-ide-java-ee-developers), o instalar los correspondientes plugins en otras variantes del IDE.

### Registrar Tomcat 9 como servidor de aplicacione en Eclipse
* Acceder a `Window > Preferences > Server > Runtime Environments

* En `Add`, seleccionar `"Apache Tomcat v9.0"` y fijar:
     ```
     Tomcat instalation directory : [ruta a apache-tomcat-9.0.12]
     JRE:                           seleccionar el que use o dejar "workbench defualt JRE"
     ```

En los proyectos Eclipse de tipo Web , el servidor estará disponible desde el menú contextual del proyecto actual
```
Proyecto [botón derecho] > Run As > Run on Server
```
(marcar `"Always use this server when running this project"` en el primer uso del servidor)


# Uso de ZK Framework en Eclipse

## Añadir arquetipos Maven de ZK Framework
Necesario para poder crear proyectos ZK vacios desde Eclipse

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

Dependiendo de la versión de Eclipse pueden ser necesarios pasos adicionales para que Eclipse reconozca el proyecto como de tipo Web.
* Al reconocer el proyect ZK como de tipo Web, el IDE le vincula la posibilidad de ejcutarlo en un servidor de aplicaciones (con `proyecto [botón derecho] > Run As > Run on Server`)

En caso de que el IDE no ofrezca esa opción, es necesario especificar detalles adicionales en la configuración del proyecto. 
1. Vincular "facetas" al proyecto
    * Sobre el proyecto `[botón derecho] > Properties > Project Facets` 
    * Seleccionar las facetas`"Dynamic Web Module"`, `"Java"`  y `"JavaScript"` (también `"ZK Studio Supports"` si está disponible)
    * (opcional) En la pestaña `"Runtimes"`también se puede vincular directamente el proyecto con el Servidor Tomcat9

2. Especificar cómo se realizará el empaquetado para el despliegue (indicando los ficheros del proyecto y su ubicación en el WAR final)
    * Sobre el proyecto `[botón derecho] > Properties > Deployment Assembly`

      Dejar la configuración con
```
Source         		 Deploy Path
/src/main/java       WEB-IN/classes       (seleccionar como tipo "Folder")
/src/main/webapp     /                    (seleccionar como tipo "Folder")
Maven Dependencies   WEB-IN/lib           (seleccionar como "Java Build Path Entries")
```

       Seleccionar `Advanced` e indicar:
```
Folder for deployment descriptor: /src/main/webapp`
```

## Instalación de ZK Studio

ZK Framework ofrece el plugin para Eclipse ZK Studio, que asiste en el desarrollo de interfaces gráficos con ZK.

* Desde `Help > Eclipse Marketplace`
* Buscar `ZK Studio`
* Instalar version 2.3.0 y reiniciar Eclipse
* Al reiniciar el IDE se solicita la activación de ZK Studio
     * Requiere registro en [www.zkoos.org](http://forum.zkoss.org/account/signup/?login_provider=local)
     * Puede forzarse la activción desde `Window > Preferences > ZK > ZK Account > [Activate]`

Una vez instalado y activado ZK Studio, están disponibles:
* La prespectiva ZK (puede habilitarse en `Window > Perspectives > Open perspective > Other > ZK`)
* El "ZUL editor" (puede habilitarse sobre el editor `[boton derecho] > Open With > ZUL editor`) 
* La paleta de componentes "ZUL palette" (habilitada desde `Window > Show View > ZUL Palette`)
* Asistente para la creación de proyectos ZK nativos

