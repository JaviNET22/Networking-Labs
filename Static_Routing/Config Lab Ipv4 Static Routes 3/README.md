# Config Lab IPv4 Static Routes 3

## Objetivo

Configurar rutas estáticas IPv4 en tres routers Cisco para permitir la comunicación entre redes que no están directamente conectadas.

## Topología

![Topología](topology.png)

## Direccionamiento

### Redes

| Red | Máscara |
|---------------------|-----------------|
| 10.1.87.0/25 | 255.255.255.128 |
| 10.1.1.128/25 | 255.255.255.128 |
| 10.1.88.128/25 | 255.255.255.128 |
| 10.1.89.0/25 | 255.255.255.128 |
| 172.16.0.0/23 | 255.255.254.0 |
| 172.16.2.0/23 | 255.255.254.0 |

### Interfaces

| Dispositivo | Interfaz | IP | Descripción |
|-------------|----------|-------------------|-------------|
| R1 | g0/0 | 10.1.87.1/25 | to LAN |
| R1 | g0/1 | 10.1.1.129/25 | to R2 |
| R1 | g0/2 | 10.1.88.129/25 | to R3 |
| R2 | g0/0 | 172.16.2.1/23 | to LAN |
| R2 | g0/1 | 172.16.0.2/23 | to R3 |
| R2 | g0/2 | 10.1.1.130/25 | to R1 |
| R3 | g0/0 | 10.1.89.1/25 | — |
| R3 | g0/1 | 10.1.88.130/25 | to R1 |
| R3 | g0/2 | 172.16.0.1/23 | — |

## Configuración realizada

### Configuración de interfaces

#### R1

```bash
Router(config)#hostname R1
!
R1(config)#int g0/0
R1(config-if)#ip address 10.1.87.1 255.255.255.128
R1(config-if)#desc ## to LAN ##
R1(config-if)#no shutdown
!
R1(config-if)#int g0/2
R1(config-if)#ip address 10.1.88.129 255.255.255.128
R1(config-if)#desc ## to R3 ##
R1(config-if)#no shutdown
!
R1(config)#int g0/1
R1(config-if)#ip address 10.1.1.129 255.255.255.128
R1(config-if)#desc ## to R2 ##
R1(config-if)#no shutdown
```

#### R2

```bash
Router(config)#hostname R2
!
R2(config)#int g0/1
R2(config-if)#ip address 172.16.0.2 255.255.254.0
R2(config-if)#desc ## to R3 ##
R2(config-if)#no shutdown
!
R2(config-if)#int g0/2
R2(config-if)#ip address 10.1.1.130 255.255.255.128
R2(config-if)#desc ## to R1 ##
R2(config-if)#no shutdown
!
R2(config-if)#int g0/0
R2(config-if)#ip address 172.16.2.1 255.255.254.0
R2(config-if)#desc ## to LAN ##
R2(config-if)#no shutdown
```

#### R3

```bash
Router(config)#hostname R3
!
R3(config)#int g0/1
R3(config-if)#ip address 10.1.88.130 255.255.255.128
R3(config-if)#desc ## to R1 ##
R3(config-if)#no shutdown
!
R3(config-if)#int g0/0
R3(config-if)#ip address 10.1.89.1 255.255.255.128
R3(config-if)#no shutdown
!
R3(config-if)#int g0/2
R3(config-if)#ip address 172.16.0.1 255.255.254.0
R3(config-if)#no shutdown
```

### Rutas estáticas

#### R1

```bash
R1(config)#ip route 10.1.89.0 255.255.255.128 g0/2 10.1.88.130
R1(config)#ip route 172.16.2.0 255.255.254.0 g0/1 10.1.1.130
```

#### R2

```bash
R2(config)#ip route 10.1.87.0 255.255.255.128 g0/2 10.1.1.129
R2(config)#ip route 10.1.89.0 255.255.255.128 g0/1 172.16.0.1
```

#### R3

```bash
R3(config)#ip route 10.1.87.0 255.255.255.128 g0/1 10.1.88.129
R3(config)#ip route 172.16.2.0 255.255.254.0 g0/2 172.16.0.2
```

## Verificación

### Pruebas

- No se ha realizado ninguna prueba

## Problemas encontrados

Ningun problema encontrado.

## Aprendizajes

| Campo       | Valor               |
| ----------- | ------------------- |
| Dificultad  | ⭐☆☆☆☆            |
| Tecnologías |   Cisco IOS     |
| Software    | Cisco Packet Tracer |
| Estado      | ✅ Completado        |

