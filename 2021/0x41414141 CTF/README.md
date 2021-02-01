# 0x41414141 CTF

Vous trouverez ci-dessous mes solutions pour ce CTF.  
  
Le flag a le format suivant :
```
flag{[A-Za-z0-9_]*}
```

Dans un premier temps, pour s'inscrire, il faut trouver un code.

Je trouve celui-ci dans le logo du site :

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0x41414141%20CTF/Inscription/CTF3.gif" alt="Logo" align="center">
</p>

Avec la commande suivante :

```bash
strings CTF3.gif | awk 'length($0)>9' | sort -u
```

Je récupère la châine suivante :

```
;secret: 100110010011
```

Ce code binaire est converti en décimal via le site suivant : https://www.binary-code.org/binary/16bit/0000100110010011/

Ce qui me permet d'obtenir le code pour m'inscrire : **2451**

## Blockchain

### Sanity Check (238)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0x41414141%20CTF/Blockchain/Sanity%20Check/sanity_check.png" alt="Sanity Check" align="center">
</p>

Le fichier de l'épreuve est disponible ici : [chall.sol](https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0x41414141%20CTF/Blockchain/Sanity%20Check/chall.sol)

J'affectue mes recherches sur le site [Etherscan](https://www.rinkeby.io).

Je trouve rapidement la transaction suivante :

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0x41414141%20CTF/Blockchain/Sanity%20Check/etherscan.png" alt="Transaction" align="center">
</p>

Que je décode via [CyberChef - The Cyber Swiss Army Knife](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')&input=MHg2MDgwNjA0MDUyMzQ4MDE1NjEwMDEwNTc2MDAwODBmZDViNTA2MTAxMTI4MDYxMDAyMDYwMDAzOTYwMDBmM2ZlNjA4MDYwNDA1MjM0ODAxNTYwMGY1NzYwMDA4MGZkNWI1MDYwMDQzNjEwNjAyODU3NjAwMDM1NjBlMDFjODA2M2I2MjdjZjNiMTQ2MDJkNTc1YjYwMDA4MGZkNWI2MDMzNjBhNTU2NWI2MDQwODA1MTYwMjA4MDgyNTI4MzUxODE4MzAxNTI4MzUxOTE5MjgzOTI5MDgzMDE5MTg1MDE5MDgwODM4MzYwMDA1YjgzODExMDE1NjA2YjU3ODE4MTAxNTE4MzgyMDE1MjYwMjAwMTYwNTU1NjViNTA1MDUwNTA5MDUwOTA4MTAxOTA2MDFmMTY4MDE1NjA5NzU3ODA4MjAzODA1MTYwMDE4MzYwMjAwMzYxMDEwMDBhMDMxOTE2ODE1MjYwMjAwMTkxNTA1YjUwOTI1MDUwNTA2MDQwNTE4MDkxMDM5MGYzNWI2MDQwODA1MTgwODIwMTkwOTE1MjYwMWE4MTUyN2Y2NjZjNjE2NzdiMzE3NDVmMzE3MzVmNmE3NTczMzc1Zjc0NjgzMzVmNzM3NDQwNzI3NDdkMDAwMDAwMDAwMDAwNjAyMDgyMDE1MjkwNTZmZWEyNjQ2OTcwNjY3MzU4MjIxMjIwMjgyM2YzNDY0ZDMzODkzNDJhYjY1MThiYjc3YmI0NmFhY2Y2YzdmYjJiYWFjM2I2NTkzZTU5MTc2NTdmOGEzMzY0NzM2ZjZjNjM0MzAwMDYwYzAwMzM) :

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0x41414141%20CTF/Blockchain/Sanity%20Check/flag.png" alt="Flag" align="center">
</p>

Et voilà le flag :

```
flag{1t_1s_jus7_th3_st@rt}
```

### Secure Enclave (427)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0x41414141%20CTF/Blockchain/Secure%20Enclave/secure_enclave.png" alt="Secure Enclave" align="center">
</p>

Sur le même principe, je trouve la transaction :

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0x41414141%20CTF/Blockchain/Secure%20Enclave/secure_enclave_rinkeby.png" alt="Rinkeby" align="center">
</p>

Et je décode son contenu :

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0x41414141%20CTF/Blockchain/Secure%20Enclave/decode.png" alt="Décodage" align="center">
</p>

Et voilà le flag :

```
flag{3v3ryth1ng_1s_BACKD00R3D_0020}
```

## Misc

### Optimizer (325)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0x41414141%20CTF/Misc/Optimizer/optimizer.png" alt="Optimizer" align="center">
</p>

J'ai développé le petit programme suivant en Python :

```python
#!/usr/bin/env python3

from pwn import *
import re

ip = "207.180.200.166"
port = 9660
reg1 = r"([0-9]+)"

def getInvCount(arr, n):
    inv_count = 0
    for i in range(n):
        for j in range(i + 1, n):
            if (arr[i] > arr[j]):
                inv_count += 1
    return inv_count 

r = remote(ip, port)

# Traitement du niveau 1
r.recvuntil("level 1: tower of hanoi\n")
print("---------- TRAITEMENT DU NIVEAU 1 ----------")
while True:
	r1 = r.recvline().decode("utf-8")
	if r1 == "> level 2 : merge sort, give me the count of inversions\n":
		break;
	print("Reçu : %s" % r1[:-1])
	re1 = re.findall(reg1, r1)
	if re1:
		c1 = pow(2, len(re1)) - 1
		print("Envoyé : %s" % c1)
		r.sendline(str(c1))
	else:
		print("L'expression régulière ne fonctionne pas !")
		exit

# Traitement du niveau 2
print("---------- TRAITEMENT DU NIVEAU 2 ----------")
while True:
	r2 = r.recvline().decode("utf-8")
	print("Reçu : %s" % r2[:-1])
	re2 = re.findall(reg1, r2)
	if re2:
		tab = []
		for i in range(len(re2)):
                	tab.append(int(re2[i]))
		c2 = getInvCount(tab, len(tab))
		print("Envoyé : %s" % c2)
		r.sendline(str(c2))
	else:
		print("L'expression régulière ne fonctionne pas !")
		exit
```

Il me permet d'obtenir la chaîne suivante :

```
> you won here's your flag flag{g077a_0pt1m1ze_3m_@ll}
```

Et le flag :

```
flag{g077a_0pt1m1ze_3m_@ll}
```
