
### Componentes
 - AddChequeraComponent: Componente dialog que permitirá agregar chequeras en base a un usuario y/o cuenta de banco.
 - DeleteComponent: Componente dialog que permitirá eliminar chequeras que se encuentren en el estado de “En proceso”.
 - DeleteChequeraComponent: Componente dialog que permitirá eliminar chequeras que se encuentren en el estado de “En proceso”.
 - EditChequeraComponent:  Componente dialog que permitirá eliminar chequeras que se encuentren en el estado de “En proceso”.
 - Gestion: Componente dialog que permitirá eliminar chequeras que se encuentren en el estado de “En proceso”.
 - AlertComponent: Componente para gestionar los mensajes de alert del sistema.

### AddChequeraComponent
Hooks para el manejo del estados del component autocomplete

![imagen](https://user-images.githubusercontent.com/64711241/204117580-20772be0-2f6b-4c68-8030-2242f88fb7e6.png)




## Error conexion a  base de datos del Backend para versiones posteriores de JDK 8
###### La base de datos de 172.16.0.19,45250 usa un formato tls1.0 desactualizado que  el JDK bloquea, para poder correr bien la app hay que modificar el archivo:  \jdk-11.0.12\conf\security\java.security
![imagen](https://user-images.githubusercontent.com/21285164/148012801-3c1bfed2-8ff5-4ffe-9d20-7b6235813445.png)

###### y cambiar
- jdk.tls.disabledAlgorithms=SSLv3, TLSv1, TLSv1.1, RC4, DES, MD5withRSA
![imagen](https://user-images.githubusercontent.com/21285164/148012863-b3a4ba79-f7b5-4820-aeb2-665f6925b6d8.png)

###### por:
- jdk.tls.disabledAlgorithms=SSLv3, RC4, DES, MD5withRSA, \
    DH keySize < 1024, EC keySize < 224, 3DES_EDE_CBC, anon, NULL, \
    include jdk.disabled.namedCurves
 ![imagen](https://user-images.githubusercontent.com/21285164/148013011-e1414f8f-2232-46c1-b15b-fa713fb6979f.png)

### Conexion a Filezila
- username: ftpsinaf
- password:!Ftp4lb#2021
![imagen](https://user-images.githubusercontent.com/21285164/148013616-9f5f808c-8948-4c13-acdb-a0cfaa3db162.png)


### SQL Server
- 172.16.0.19,45250
- username: slacunza
- password:Slacunza123$

## Deploy
### Frontend
- ng build --configuration=production --base-href /AlbumMultimedia/
    - Se genera en la carpeta del front dist/ que copie a la carpeta deploy/frontend

### backend
- mvn clean package
    - Se generar el archivo backendAlbumMultimedia.war en la carpeta del backend que copie a la carpeta deploy/bakend

### Conectarse a la virtual
- ssh inacif@172.16.1.152 -p 22443
    - la password es: 4lbina#2021
- su -
    - la password del root: $4lb1n4#2021
   
#### Copiar el repo
- cd /home/git/
- git clone https://github.com/Sharo1405/AlbumMultimedia-inacif
    - la password: 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   
    - si vencio la generas en https://github.com/settings/tokens
#### Copiar los archivos a tomcat
 - rm -R /var/lib/tomcat9/webapps/AlbumMultimedia
    - si existe eliminar el frontend anterior 
 - cp -R /home/git/AlbumMultimedia-inacif/deploy/frontend/AlbumMultimedia /var/lib/tomcat9/webapps/
    - copiar el frontend
 - cp -i /home/git/AlbumMultimedia-inacif/deploy/backend/backendAlbumMultimedia.war /var/lib/tomcat9/webapps/
    - copiar el war del backend
 - systemctl restart tomcat9
    - reiniciar tomcat9
#### Ver el log de tomcat9
 - journalctl -u tomcat9.service

#### Usuario de apache tomcat
- user: root
- password:  $4lb1n4#2021
    - las mismas que el usuario root de debian 

## Configurarion Inicial de Apache Tomcat
- apt update
- apt install tomcat9 tomcat9-admin
- systemctl enable tomcat9
    - habilitar tomcat9
    -  systemctl disable tomcat9
    -  deshabilitar tomcat9 
- ufw allow from any to any port 8080 proto tcp
    - Permitir conexiones al puerto por defecto de tomcat 
### Credenciales del usuario root de apache tomcat
- nano /etc/tomcat9/tomcat-users.xml
- Al final agregar:
    - <role rolename="admin-gui"/&gt;
    - <role rolename="manager-gui"/&gt;
    - <user username="root" password="$4lb1n4#2021" roles="admin-gui,manager-gui"/&gt;
    - </tomcat-users&gt;

- systemctl restart tomcat9
    - reiniciar tomcat 

### Erorr del tsl del backend 
- en la virtual de debian se deberia de tener instalado la version de jd8 o una version menor que no posea el error del tsl
- si no se tiene una version posterior a jdk 8 y el backend da error certificado tls en la base de datos
- editar el archivo java.security igual que en windows
- nano /etc/java-11-openjdk/security/java.security

###### y cambiar
- jdk.tls.disabledAlgorithms=SSLv3, TLSv1, TLSv1.1, RC4, DES, MD5withRSA
![imagen](https://user-images.githubusercontent.com/21285164/148012863-b3a4ba79-f7b5-4820-aeb2-665f6925b6d8.png)

###### por:
- jdk.tls.disabledAlgorithms=SSLv3, RC4, DES, MD5withRSA, \
    DH keySize < 1024, EC keySize < 224, 3DES_EDE_CBC, anon, NULL, \
    include jdk.disabled.namedCurves
 ![imagen](https://user-images.githubusercontent.com/21285164/148013011-e1414f8f-2232-46c1-b15b-fa713fb6979f.png)




     




