# Lab - Subnetting y Static Routing

## Objetivo

Implementar subnetting con máscaras /30 en una topología de 4 routers y configurar rutas estáticas para permitir la comunicación entre redes personales.

## Direccionamiento

### Subnets (WAN)

| Subnet | Network | Hosts | Broadcast |
|--------|----------------------|----------------------|----------------------|
| R1-R2 | 10.100.200.0/30 | 10.100.200.1 - 10.100.200.2 | 10.100.200.3 |
| R1-R3 | 10.100.200.4/30 | 10.100.200.5 - 10.100.200.6 | 10.100.200.7 |
| R1-R4 | 10.100.200.8/30 | 10.100.200.9 - 10.100.200.10 | 10.100.200.11 |

### Redes LAN

| Dispositivo | Red | Gateway |
|-------------|-----------------|-------------|
| R2 | 192.168.50.0/24 | 192.168.50.1 |
| R3 | 192.168.51.0/24 | 192.168.51.1 |
| R4 | 192.168.52.0/24 | 192.168.52.1 |

## Configuración realizada

### Configuración de interfaces en R2

```bash
hostname R2
int g0/0
ip address 10.100.200.2 255.255.255.252
no shutdown
!
int g0/1
ip address 192.168.50.1 255.255.255.0
no shutdown
```

### Configuración de interfaces en R3

```bash
hostname R3
int g0/0
ip address 10.100.200.6 255.255.255.252
no shutdown
!
int g0/1
ip address 192.168.51.1 255.255.255.0
no shutdown
```

### Configuración de interfaces en R4

```bash
hostname R4
int g0/0
ip address 10.100.200.10 255.255.255.252
no shutdown
!
int g0/1
ip address 192.168.52.1 255.255.255.0
no shutdown
```

### Configuración de interfaces en R1

```bash
hostname R1
int g0/0
ip address 10.100.200.1 255.255.255.252
no shutdown
!
int g0/1
ip address 10.100.200.5 255.255.255.252
no shutdown
!
int g0/2
ip address 10.100.200.9 255.255.255.252
no shutdown
```

### Rutas estáticas

#### R2

```bash
ip route 192.168.51.0 255.255.255.0 g0/0 10.100.200.1
ip route 192.168.52.0 255.255.255.0 g0/0 10.100.200.1
```

#### R3

```bash
ip route 192.168.50.0 255.255.255.0 g0/0 10.100.200.5
ip route 192.168.52.0 255.255.255.0 g0/0 10.100.200.5
```

#### R4

```bash
ip route 192.168.50.0 255.255.255.0 g0/0 10.100.200.9
ip route 192.168.51.0 255.255.255.0 g0/0 10.100.200.9
```

#### R1

```bash
ip route 192.168.50.0 255.255.255.0 g0/0 10.100.200.2
ip route 192.168.51.0 255.255.255.0 g0/1 10.100.200.6
ip route 192.168.52.0 255.255.255.0 g0/2 10.100.200.10
```

## Verificación

### Comandos ejecutados

```bash
show ip route
ping
```

### Resultados

- ✅ PC1 (R2 LAN) puede comunicarse con PC2 (R3 LAN).
- ✅ PC2 (R3 LAN) puede comunicarse con PC3 (R4 LAN).

## Problemas encontrados

Configuré mal las ip routes en R1 y las tuvé que reconfigurar 😑.

## Aprendizajes

- Subnetting con máscara /30 para enlaces punto a punto.
- Configuración de rutas estáticas en múltiples routers.
- Verificación de conectividad extremo a extremo.

## Ficha del laboratorio

| Campo       | Valor               |
| ----------- | ------------------- |
| Dificultad  | ⭐☆☆☆☆               |
| Tecnologías | Subnetting, Static Routing, Cisco IOS |
| Software    | Cisco Packet Tracer |
| Estado      | ✅ Completado        |