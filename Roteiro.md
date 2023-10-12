# Subredes
$$
\begin{align*}
\hline
&\text{Primeira subrede: 2 bits - 2 (4) endereços}\\
&\tt{192.168.10.0/30}\quad\text{máscara: \tt{255.255.255.252}}\\
&\tt{192.168.10.3/30}\\
\hline
&\text{Segunda subrede: 2 bits - 2 (4) endereços}\\
&\tt{192.168.10.4/30}\quad\text{máscara: \tt{255.255.255.252}}\\
&\tt{192.168.10.7/30}\\
\hline
&\text{Terceira subrede: 2 bits - 2 (4) endereços}\\
&\tt{192.168.10.8/30}\quad\text{máscara: \tt{255.255.255.252}}\\
&\tt{192.168.10.11/30}\\
\hline
&\text{Quarta subrede: 2 bits - 2 (4) endereços}\\
&\tt{192.168.10.12/30}\quad\text{máscara: \tt{255.255.255.252}}\\
&\tt{192.168.10.15/30}\\
\hline
&\text{Quinta subrede: 2 bits - 2 (4) endereços}\\
&\tt{192.168.10.16/30}\quad\text{máscara: \tt{255.255.255.252}}\\
&\tt{192.168.10.19/30}\\
\hline
&\text{Sexta subrede: 2 bits - 2 (4) endereços}\\
&\tt{192.168.10.20/30}\quad\text{máscara: \tt{255.255.255.252}}\\
&\tt{192.168.10.23/30}\\
\hline
&\text{Sétima subrede (IPv6): 2 bits - 2 (4) endereços}\\
&\tt{2001:cafe:db:1::1/64}\\
&\tt{2001:cafe:db:1::2/64}\\
\end{align*}
$$

# Tabela Relacional
| IOS | Roteador | Interface | Endereço |
|:--: | :--: | :--: | :--: |
| Cisco | R1 | f0/0 | 192.168.10.1/30 |
| Mikrotik | R6 | e0 | 192.168.10.2/30  |
|||||
| Cisco | R1 | e1/2 | 192.168.10.5/30 |
| Cisco | R4 | e1/2 | 192.168.10.6/30 |
|||||
| Cisco | R1 | e1/1 | 192.168.10.9/30 | 
| Cisco | R3 | e1/1 | 192.168.10.10/30 |
|||||
| Cisco | R3 | e1/3 | 192.168.10.13/30 |
| Cisco | R4 | e1/3 | 192.168.10.14/30 |
|||||
| Cisco | R3 | e1/2 | 192.168.10.17/30 | 
| Cisco | R2 | e1/2 | 192.168.10.18/30 |
|||||
| Cisco | R2 | f0/0 | 192.168.10.21/30 |
| Mikrotik | R5 | e0 | 192.168.10.22/30 | 
|||||
| Cisco | R1 | e1/0 | 2001:cafe:db:1::1/64 |
| Cisco | R2 | e1/0 | 2001:cafe:db:1::2/64 |


# Comandos
## Roteador R1
```bash
configure terminal

interface f0/0
ip address 192.168.10.1 255.255.255.252
no shutdown
exit

interface e1/2
ip address 192.168.10.5 255.255.255.252
no shutdown
exit

interface e1/1
ip address 192.168.10.9 255.255.255.252
no shutdown
exit

ipv6 unicast-routing
interface e1/0
ipv6 enable
ipv6 address 2001:cafe:db:1::1/64
no shutdown
exit

exit
wr
```

- **TODO:** Túnel!

## Roteador R2
```bash
configure terminal

interface e1/2
ip address 192.168.10.18 255.255.255.252
no shutdown
exit

interface f0/0
ip address 192.168.10.21 255.255.255.252
no shutdown
exit

ipv6 unicast-routing
interface e1/0
ipv6 enable
ipv6 address 2001:cafe:db:1::2/64
no shutdown
exit

exit
wr
```

- **TODO:** Túnel!

## Roteador R3
```bash
configure terminal

interface e1/1
ip address 192.168.10.10 255.255.255.252
no shutdown
exit

interface e1/3
ip address 192.168.10.13 255.255.255.252
no shutdown
exit

interface e1/2
ip address 192.168.10.17 255.255.255.252
no shutdown
exit

exit
wr
```

## Roteador R4
```bash
configure terminal

interface e1/2
ip address 192.168.10.6 255.255.255.252
no shutdown
exit

interface e1/3
ip address 192.168.10.14 255.255.255.252
no shutdown
exit

exit
wr
```

## Roteador R5
```bash
admin

ip address add address=192.168.10.22/30 interface=ether1
```

## Roteador R6
```bash
admin

ip address add address=192.168.10.2/30 interface=ether1
```