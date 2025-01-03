# Subnetting

## IPv4 Address classes
```
Class   Prefix Length   First Octet Numeric Range
A       /8              0-127
B       /16             128-191
C       /24             192-223
```

## IANA

* The IANA (internet assigned numbers authority) assigns IPv4 addresses/networks to companies based on their size
* A very large company would receive class A or B network, while a small company would receive class C.
* This system led to wasted IP addresses
![alt text](image-1.png)
* A point to point network (between routers) would be assigned 256 addresses, but only need four.

## CIDR - Classess Inter-Domain Routing

* With CIDR, the requirements for class A being /8, B /16 and C /24 were removed, allowing large networks to be split into smaller ones allowing greater efficiency. The smaller networks are called subnetworks/subnets.

Number of usable addresses:
```
2^n - 2 = useable addresses
where n is the number of host bits
```
For example, /25:
```
11001011.00000000.01110001.00000000
203     .0       .113     .0
11111111.11111111.11111111.10000000 (/25)
255     .255     .255     .128
There are 7 host bits, so 2^7 - 2 = 126 useable addresses
```

## /31 - Point to point networks

for the network `203.0.133.0/31`, there is the ip range `203.0.113.0` to `203.0.113.1` (two addresses). In binary:
```
11001011.00000000.011110001.00000000
11001011.00000000.011110001.00000001
```
In a point to point network, there is no need for a network address or broadcast address, so the only two addresses could be assigned to the two interfaces on the routers.

![alt text](image-2.png)

## /32

The entire address is the network, there are 0 host bits and there is -1 useable addresses. They can be used for networks to specific hosts.

## CIDR Notation

![alt text](image-3.png)

## Example

![alt text](image-4.png)

* We need 47 addresses per subnet
* 47 * 4 = 118  addresses needed.
* 192.168.1.0/24 is a class C network, which can accomodate up to 256 addresses.
* We need four equal size subnets, with enough room for 45 hosts
```
/30 -> 2 host bits -> 2^2-2 = 2 useable addresses
/29 -> 3 host bits -> 2^3-2 = 6 useable addresses
/28 -> 4 host bits -> 2^4-2 = 14 useable addresses
/27 -> 5 host bits -> 2^5-2 = 30 useable addresses
/26 -> 6 host bits -> 2^6-2 = 62 useable addresses
```

Subnet 1 is `192.168.1.0/26`, to find the next subnet we get the broadcast address of S1 and find the next address from that.

```
11000000.10101000.00000001.00000000 - Address
11111111.11111111.11111111.11000000 - Net mask
11000000.10101000.00000001.00111111 - Broadcast
11000000.10101000.00000001.01000000 - Next address
192     .168     .1       .64
```
So subnet 2 is `192.168.1.64/26`. Similarly, the next useable address after that is:
```
11000000.10101000.00000001.10000000
192     .168     .1       .128

then...
11000000.10101000.00000001.11000000
192     .168     .1       .192
```

So the four subnets are:
```
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```