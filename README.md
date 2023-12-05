# Practica DHCP - Maquina Virtual

## 1. Instalar paquete isc-dhcp-server.

Empezamos instalando el servicio DHCP con **“apt-get install isc-dhcp-server -y”**.

Una vez completada la instalación, iniciamos el servicio DHCP y habilitamos para que se inicie al reiniciar el sistema con el siguiente comando: 
```
→ “systemctl start isc-dhcp-server” 
→ “systemctl enable isc-dhcp-server”
```

## 2. Editar para una configuración básica /etc/dhcp/dhcpd.conf.

Nos movemos a *"etc"* y pondremos el comando (con nano obviamente): **“/etc/dhcp/dhcpd.conf”** y cambiaremos / pondremos lo siguiente:

- Por el principio hay que comentar 2 líneas donde se encuentran en el bloque de “option”, ya que por defecto estarán descomentadas.

- Más para abajo, hay una línea “authoritative;” que aparece por defecto comentada, hay que descomentarla.


Continuamente, configuraremos las siguientes características con una subred específica, configuración de DNS y puerta de enlace:

Puedes especificar cómo el servidor DHCP debe asignar direcciones IP y otros parámetros de configuración a los clientes en la red. Puedes especificar las direcciones IP de los servidores DNS que los clientes utilizarán para resolver nombres de dominio. Esto es crucial para permitir que los dispositivos en la red resuelvan nombres de host en direcciones IP. Por ejemplo el DNS de google.

Se configura tambien la puerta de enlace del router para que los clientes puedan utilizar.

Configuramos la duración del arrendamiento para las direcciones IP asignadas a los clientes. Estos valores determinan cuánto tiempo un cliente puede retener la dirección IP antes de tener que renovarla.

Una vez configurado este archivo, para aplicar los cambios hacemos un **"sudo service isc-dhcp-server restart"**

## 3. Editar para configurar la interfaz de red /etc/Default isc-dchp-server.

En **“/etc/default/isc-dhcp-server”** hay que modificar una cosilla, en la línea de INTERFACESv4 hay que poner el adaptador enp0s8.

- Para comprobar si hicimos todo correctamente, haremos los comandos:
```
“sudo service isc-dhcp-server restart” 
“sudo service isc-dhcp-server status”. 
```
En su estado debe salirnos en Verde.

## 4. Declarar una subnet 172.16.0.0/16.

En el archivo que explicamos pasos atras (**“/etc/dhcp/dhcpd.conf”**), en el codigo/script lo pondremos de esta manera en este bloque de codigo del archivo:

```
subnet 172.16.0.0 netmask 255.255.0.0 {
    range 172.16.0.25 172.16.0.200;  # Rango de direcciones IP disponibles
    option routers 172.16.0.1;  # Puerta de enlace (router)
    option subnet-mask 255.255.0.0;
    option broadcast-address 172.16.0.255;
    option domain-name-servers 8.8.8.8, 8.8.4.4;  # Servidores DNS de Google
    option domain-name "pedroserverpracticaSRI";  # Nombre de dominio
}
```

Para aplicar los cambios: **"sudo service isc-dhcp-server restart"**

## 5. Arranca el servicio con systemctl.

Pondremos **sudo systemctl start isc-dhcp-server**.

Para asegurarnos de que el servicio DHCP se inicie automáticamente al arrancar el sistema, puedes habilitarlo con: **"sudo systemctl enable isc-dhcp-server"**

*Cabe recalcar que en nuestro caso al tener una versión mas antigua de Ubuntu, lo haríamos con el comando "service".*

## 6. Comprueba el servicio con "systemctl status".

Simplemente despues de aplicar los cambios con un "restart", haremos un "**sudo systemctl status isc-dhcp-server**"

Con el service sería similar: **"sudo service isc-dhcp-server status"**

Si nos aparece en verde, es que todo está en funcionamiento y correcto.

## 7. Prueba con el cliente que se le asigna un ip en el rango.

Una vez configurado el DHCP, todos los archivos explicados anteriormente, con un "**ip a**" podemos ver las interfaces con sus respectivas caracteristicas (nosotros queremos ver la IP asignada.) En nuestro caso, trabajamos con "enp0s8", por lo cual podemos ver que tiene asignada una IP por el servidor DHCP. 

- En nuestro caso, la IP que asignamos es: 172.16.0.25.

## 8. Declarar una asignación por mac fija a 172.16.0.5.