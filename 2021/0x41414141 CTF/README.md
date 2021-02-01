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
