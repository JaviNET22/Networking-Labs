# Config Lab IPv4 Static Routes 2

## Objetivo

Configurar rutas estáticas en cuatro routers Cisco para permitir la comunicación entre cuatro subredes distintas a través de un switch de capa 2.

## Topología

![Topología](topology.png)

## Direccionamiento

| Dispositivo | Interfaz | IP | Descripción |
|-------------|----------|----------------|-------------|
| R1 | g0/2 | 192.168.100.1/26 | ## to PC0 ## |
| R1 | g0/1 | 172.16.100.1/24 | ## to SW5 ## |
| R2 | g0/2 | 192.168.100.65/26 | ## to PC1 ## |
| R2 | g0/1 | 172.16.100.2/24 | ## to SW5 ## |
| R3 | g0/2 | 192.168.100.129/26 | ## to PC2 ## |
| R3 | g0/1 | 172.16.100.3/24 | ## to SW5 ## |
| R4 | g0/2 | 192.168.100.193/26 | ## to PC3 ## |
| R4 | g0/1 | 172.16.100.4/24 | ## to SW5 ## |

### Subredes

| Subred | Rango |
|-------------|----------------|
| 192.168.100.0/26 | PC0 |
| 192.168.100.64/26 | PC1 |
| 192.168.100.128/26 | PC2 |
| 192.168.100.192/26 | PC3 |
| 172.16.100.0/24 | Enlace a SW5 |

## Configuración realizada

### Configuración básica de interfaces

```cmd
R1
R1(config)#int g0/2
R1(config-if)#ip address 192.168.100.1 255.255.255.192
R1(config-if)#desc ## to PC0 ##
R1(config-if)#no shutdown
!
R1(config-if)#int g0/1
R1(config-if)#ip address 172.16.100.1 255.255.255.0
R1(config-if)#desc ## to SW5 ##
R1(config-if)#no shutdown
```

```cmd
R2
R2(config)#int g0/2
R2(config-if)#ip address 192.168.100.65 255.255.255.192
R2(config-if)#desc ## to PC1 ##
R2(config-if)#no shutdown
!
R2(config-if)#int g0/1
R2(config-if)#ip address 172.16.100.2 255.255.255.0
R2(config-if)#desc ## to SW5 ##
R2(config-if)#no shutdown
```

```cmd
R3
R3(config)#int g0/2
R3(config-if)#ip address 192.168.100.129 255.255.255.192
R3(config-if)#description ## to PC2 ##
R3(config-if)#no shutdown
!
R3(config-if)#int g0/1
R3(config-if)#ip address 172.16.100.3 255.255.255.0
R3(config-if)#description ## to SW5 ##
R3(config-if)#no shutdown
```

```cmd
R4
R4(config)#int g0/2
R4(config-if)#ip address 192.168.100.193 255.255.255.192
R4(config-if)#description ## to PC3 ##
R4(config-if)#no shutdown
!
R4(config-if)#int g0/1
R4(config-if)#ip address 172.16.100.4 255.255.255.0
R4(config-if)#description ## to SW5 ##
R4(config-if)#no shutdown
```

### Rutas estáticas

```cmd
R1
R1(config)#ip route 192.168.100.64 255.255.255.192 g0/1 172.16.100.2
R1(config)#ip route 192.168.100.128 255.255.255.192 g0/1 172.16.100.3
R1(config)#ip route 192.168.100.192 255.255.255.192 g0/1 172.16.100.4
```

```cmd
R2
R2(config)#ip route 192.168.100.0 255.255.255.192 g0/1 172.16.100.1
R2(config)#ip route 192.168.100.128 255.255.255.192 g0/1 172.16.100.3
R2(config)#ip route 192.168.100.192 255.255.255.192 g0/1 172.16.100.4
```

```cmd
R3
R3(config)#ip route 192.168.100.0 255.255.255.192 g0/1 172.16.100.1
R3(config)#ip route 192.168.100.64 255.255.255.192 g0/1 172.16.100.2
R3(config)#ip route 192.168.100.192 255.255.255.192 g0/1 172.16.100.4
```

```cmd
R4
R4(config)#ip route 192.168.100.0 255.255.255.192 g0/1 172.16.100.1
R4(config)#ip route 192.168.100.64 255.255.255.192 g0/1 172.16.100.2
R4(config)#ip route 192.168.100.128 255.255.255.192 g0/1 172.16.100.3
```

## Verificación


### Pruebas

- ✅ PC0 (192.168.100.0/26) puede alcanzar PC1 y PC2.
- ✅ PC1 (192.168.100.64/26) puede alcanzar PC3.

## Problemas encontrados

Pensaba que no tenía que configurar las static routes ya que pensaba que el switch iba a redigir el tráfico solo, pero estaba equivocado🫠.

## Aprendizajes

| Campo       | Valor               |
| ----------- | ------------------- |
| Dificultad  | ⭐☆☆☆☆               |
| Tecnologías | IPv4, Rutas estáticas, Cisco IOS |
| Software    | Cisco Packet Tracer |
| Estado      | ✅ Completado        |
