
# 0xL4ughCTF

Vous trouverez ci-dessous mes solutions pour ce CTF.  
  
Le flag a le format suivant :
```
0xL4ugh{[A-Za-z0-9_]*}
```

## Misc

### Sanity Check (50)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0xL4ughCTF/Misc/Sanity%20Check/Sanity%20Check.png" alt="Sanity Check" align="center">
</p>

Un petit tour sur le serveur Discord :

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0xL4ughCTF/Misc/Sanity%20Check/Discord.png" alt="Discord" align="center">
</p>

Et voici notre flag :
```
0xL4ugh{welc0m3_t0_Our_Firs7_CTF}
```

### 1990 (100)

<p align="center">
  <img src="https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0xL4ughCTF/Misc/1990/1990.png" alt="1990" align="center">
</p>

Le fichier de l'épreuve est ici : [1990.zip](https://raw.githubusercontent.com/Zyrfex/CTF/main/2021/0xL4ughCTF/Misc/1990/1990.zip)

L'écoute du fichier WAV nous permet d'obtenir une piste : la composition de numéros sur un clavier de téléphone.

J'utilise le site [Detect DTMF Tones](http://dialabc.com/sound/detect/) et j'obtiens la chaîne de caractères suivantes :
```
66#666#8#33#888#33#777#999#8#44#444#66#4#666#66#7777#2#6#33#9#2#999#
```
