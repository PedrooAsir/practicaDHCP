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
