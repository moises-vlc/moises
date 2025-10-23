## CREACIÓN DE SSH

### PASOS

**1. Configurar las dos máquinas**

Nos meteremos en confconsole en las dos máquinas, en el cliente y en el servidor, en una máquina la pondremos en dhcp y la otra en ip estática. 

En mi caso pondremos la del servidor en dhcp.


<img width="491" height="324" alt="Screenshot_20251023_082503" src="https://github.com/user-attachments/assets/2d9f771d-9ef9-4173-b710-06aca8407cc0" />


Y la del cliente en estática.

<img width="487" height="324" alt="Screenshot_20251023_082849" src="https://github.com/user-attachments/assets/bcc0c765-009e-40e0-85bb-6f29f1c25304" />

**2. Instalar y hacer que se conecten por ssh**

*En la máquina servidor*

Instalamos el servicio ssh con:

```bash
sudo apt update
sudo apt install openssh-server -y
```

Comprobamos que el servicio esté activo con:

```bash
sudo systemctl status ssh
```

Vemos nuestra dirección ip con:

```bash
ip a
```

*En la máquina cliente*

Instalamos el servicio ssh también:

```bash
sudo apt update
sudo apt install openssh-server -y
```

**3. Comprobamos que la conexión a través de ssh funciona**

```bash
ssh root@10.2.1.144
```


## CREACIÓN DE TELNET

**Instalamos telnet en el servidor** 

```bash
apt install telnetd-ssl
apt install telnetd xinetd
```

**Instalamos telnet en el cliente**

```bash
apt install telnetd
```
**Comprobación**

Pondremos telnet y nuestra ip del servidor

<img width="325" height="77" alt="Screenshot_20251023_102905" src="https://github.com/user-attachments/assets/79fc9a12-fcac-4239-9a48-92d171948253" />



