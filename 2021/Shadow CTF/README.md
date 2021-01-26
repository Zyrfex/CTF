# Shadow CTF

Vous trouverez ci-dessous mes solutions pour ce CTF.  
  
Le flag a le format suivant :
```
shadowCTF{[A-Za-z0-9_]+}
```

## Reverse Engineering

### Warm-up (50)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/Shadow%20CTF/Reverse%20Engineering/Warm-up/warm-up.png" alt="Warm-up" align="center">
</p>

Le fichier de l'épreuve est disponible ici : [Intro](https://github.com/Zyrfex/CTF/raw/main/2021/Shadow%20CTF/Reverse%20Engineering/Warm-up/Intro)

Je charge le programme dans [Ghidra](https://ghidra-sre.org/) et j'affiche la fonction main :
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

Je charge le programme dans [Ghidra](https://ghidra-sre.org/) et j'affiche la fonction main :
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

Je charge le programme dans [Ghidra](https://ghidra-sre.org/) et j'affiche la fonction main :
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

