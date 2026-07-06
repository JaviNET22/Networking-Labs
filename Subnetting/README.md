# Laboratorio 1 – Subnetting Tradicional

## Objetivo

Subnetting básico

### Equipos

- 1 Router (2911 o 1941)
- 3 Switches 2960
- 6 PCs

---

## Red disponible

**192.168.100.0/24**

Debes crear **3 subredes iguales**.

---

## Lo que debes calcular

1. Nueva máscara.
2. Cantidad de hosts por subred.
3. Dirección de red.
4. Primer host.
5. Último host.
6. Broadcast.

## Cálculos

![Cálculos de subredes](images/Pasted%20image%2020260706194758.png)

## Configuraciones

```bash
Router(config)#hostname R1
R1(config)#int g0/0
R1(config-if)#ip address 192.168.100.1 255.255.255.192
R1(config-if)#desc ## to SW1 ##
R1(config-if)#no shutdown
!
R1(config-if)#int g0/1
R1(config-if)#ip address 192.168.100.65 255.255.255.192
R1(config-if)#desc ## to SW2 ##
R1(config-if)#no shutdown
!
R1(config-if)#int g0/2
R1(config-if)#ip address 192.168.100.129 255.255.255.192
R1(config-if)#desc ## to SW3 ##
R1(config-if)#no shutdown
```

## Configuración de PCs

### Subnet 1 – Default gateway 192.168.100.1

![Subnet 1](images/Pasted%20image%2020260706192856.png)

### Subnet 2 – Default gateway 192.168.100.65

![Subnet 2](images/Pasted%20image%2020260706193108.png)

### Subnet 3 – Default gateway 192.168.100.129

![Subnet 3](images/Pasted%20image%2020260706193246.png)

## Ficha del laboratorio

| Campo       | Valor                                          |
| ----------- | ---------------------------------------------- |
| Dificultad  | ★★☆☆☆                                          |
| Tecnologías | Subnetting, Cisco IOS                     |
| Software    | Cisco Packet Tracer                             |
| Estado      | ✅ Completado                                   |
