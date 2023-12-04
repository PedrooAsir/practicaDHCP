# Practica DHCP - Maquina Virtual

## 1. Instalar paquete isc-dhcp-server

Empezamos instalando el servicio DHCP con **“apt-get install isc-dhcp-server -y”**.

Una vez completada la instalación, iniciamos el servicio DHCP y habilitamos para que se inicie al reiniciar el sistema con el siguiente comando: 
```
→ “systemctl start isc-dhcp-server” 
→ “systemctl enable isc-dhcp-server”
```

## 2. Editar para una configuración básica /etc/dhcp/dhcpd.conf

Nos movemos a *"etc"* y pondremos el comando (con nano obviamente): **“/etc/dhcp/dhcpd.conf”** y cambiaremos / pondremos lo siguiente:

- Por el principio hay que comentar 2 líneas donde se encuentran en el bloque de “option”, ya que por defecto estarán descomentadas.

- Más para abajo, hay una línea “authoritative;” que aparece por defecto comentada, hay que descomentarla.


Continuamente, configuraremos las siguientes características con una subred específica, configuración de DNS y puerta de enlace:

Puedes especificar cómo el servidor DHCP debe asignar direcciones IP y otros parámetros de configuración a los clientes en la red. Puedes especificar las direcciones IP de los servidores DNS que los clientes utilizarán para resolver nombres de dominio. Esto es crucial para permitir que los dispositivos en la red resuelvan nombres de host en direcciones IP. Por ejemplo el DNS de google.

Se configura tambien la puerta de enlace del router para que los clientes puedan utilizar.

Configuramos la duración del arrendamiento para las direcciones IP asignadas a los clientes. Estos valores determinan cuánto tiempo un cliente puede retener la dirección IP antes de tener que renovarla.

Una vez configurado este archivo, para aplicar los cambios hacemos un **"sudo systemctl restart isc-dhcp-server"**

