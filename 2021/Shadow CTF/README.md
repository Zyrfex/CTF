# Shadow CTF

Vous trouverez ci-dessous mes solutions pour ce CTF.  
  
Le flag a le format suivant :
```
shadowCTF{[A-Za-z0-9@ _]+}
```

## Reverse Engineering

### Warm-up (50)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Warm-up/warm-up.png" alt="Warm-up" align="center">
</p>

Le fichier de l'épreuve est disponible ici : [Intro](https://github.com/Zyrfex/CTF/raw/main/2021/Shadow%20CTF/Reverse%20Engineering/Warm-up/Intro)

Je charge le programme dans [Ghidra](https://ghidra-sre.org/) et j'affiche la fonction **main** :
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Warm-up/Ghidra.png" alt="Ghidra" align="center">
</p>

Le flag sera vite trouvé :
```
shadowCTF{steppingstone}
```

### Unchallenging (100)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Unchallenging/Unchallenging.png" alt="Unchallenging" align="center">
</p>

Le fichier de l'épreuve est disponible ici : [Unchallenging](https://github.com/Zyrfex/CTF/raw/main/2021/Shadow%20CTF/Reverse%20Engineering/Unchallenging/unchallenging)

Je charge le programme dans [Ghidra](https://ghidra-sre.org/) et j'affiche la fonction **main** :
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Unchallenging/Ghidra.PNG" alt="Ghidra" align="center">
</p>

Le flag sera vite trouvé :
```
shadowCTF{Ar@b1an_night5}
```

### Key2success (200)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Key2success/Key2success.png" alt="Key2success" align="center">
</p>

Le fichier de l'épreuve est disponible ici : [Key2sucess](https://github.com/Zyrfex/CTF/raw/main/2021/Shadow%20CTF/Reverse%20Engineering/Key2success/key2sucess)

Je charge le programme dans [Ghidra](https://ghidra-sre.org/) et j'affiche la fonction **main** :
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Key2success/Ghidra.png" alt="Ghidra" align="center">
</p>

L'analyse du code nous permet de comprendre qu'il faut renseigner la phrase suivante :
```
Constant_learning_is_the_key
```

C'est ce que nous faisons :
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Key2success/Console.png" alt="Console" align="center">
</p>

Et voilà notre flag :
```
shadowCTF{Never_stop_learning}
```

### Thirsty crow (300)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Thirsty%20crow/Thirsty%20crow.png" alt="Thirsty crow" align="center">
</p>

Le fichier de l'épreuve est disponible ici : [crow.out](https://github.com/Zyrfex/CTF/raw/main/2021/Shadow%20CTF/Reverse%20Engineering/Thirsty%20crow/crow.out)

Je charge le programme dans [Ghidra](https://ghidra-sre.org/) et j'affiche la fonction **main** :
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Thirsty%20crow/Ghidra.png" alt="Ghidra" align="center">
</p>

L'analyse du code nous permet de comprendre que si nous inversons la condition du saut (JNZ en JZ soit 85 en 84), notre flag sera affiché.

C'est ce que nous faisons dans [GHex](https://wiki.gnome.org/Apps/Ghex) :
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Thirsty%20crow/GHex.png" alt="GHex" align="center">
</p>

Une fois la modification effectuée et enregistrée, nous obtenons notre flag :
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Thirsty%20crow/Console.png" alt="Console" align="center">
</p>

Le voici :
```
shadowCTF{Thirty_5ix_r0cksin_the_p0t}
```

### Vault (400)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Vault/Vault.png" alt="Vault" align="center">
</p>

Le fichier de l'épreuve est disponible ici : [vault](https://github.com/Zyrfex/CTF/raw/main/2021/Shadow%20CTF/Reverse%20Engineering/Vault/vault)

Je charge le programme dans [Ghidra](https://ghidra-sre.org/) et j'affiche la fonction **main** :
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Vault/Ghidra.png" alt="Ghidra" align="center">
</p>

Tout comme l'épreuve précédente, nous modifions la condition du saut :
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Vault/GHex.png" alt="GHex" align="center">
</p>

Une fois la modification effectuée et enregistrée, nous obtenons notre flag :
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Vault/Console.png" alt="Console" align="center">
</p>

Le voici :
```
shadowCTF{sh@d0w_reversing_rul3s}
```

## Cryptographie

### Valhalla (50)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Cryptography/Valhalla/Valhalla.png" alt="Valhalla" align="center">
</p>

Le fichier de l'épreuve est le suivant : runes.png
<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Cryptography/Valhalla/runes.png" alt="runes" align="center">
</p>

Une recherche sur Google me permet de trouver de quoi déchiffrer l'énigme de l'épreuve : [Rune](https://fr.wikipedia.org/wiki/Rune)

Voici le flag :
```
shadowCTF{odin was here}
```
