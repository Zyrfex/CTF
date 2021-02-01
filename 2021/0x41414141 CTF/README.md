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

