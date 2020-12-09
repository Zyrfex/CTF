# Shakti CTF

Vous trouverez ci-dessous mes solutions pour ce CTF.  
  
Le flag a le format suivant :
```
shaktictf{[A-Za-z0-9_]*}
```

*Je n'ai pas eu le temps de rédiger la suite, l'accès aux épreuves n'est plus possible, désolé.*

## Reversing

### Just-Run-It! (50 - Very Easy)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/blob/main/2020/Shakti_CTF/Reversing/Just-Run-It!/Just-Run-It!.png" alt="Just-Run-It!" align="center">
</p>

Après avoir téléchargé le fichier [run](https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Reversing/Just-Run-It!/run), nous lui donnons le droit d'exécution :
```bash
chmod +x run
```

Puis nous l'exécutons avec la commande suivante :
```bash
./run
```

Et nous récupérons le flag :
```
shaktictf{and_that's_how_you_run_a_linux_binary!}
```

### PYthn (100 - Easy)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Reversing/PYthn/PYthn.png" alt="PYthn" align="center">
</p>

Après avoir récupére le fichier [PYthn.py](https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Reversing/PYthn/PYthn.py), une analyse rapide du code nous permet de déterminer que la fonction **fuN()** n'est pas utilisée.

Nous utilisons les fonctions dans le sens inverse pour récupérer notre flag :
```python
print("Le flag est : " + Fun(FuN(Q)))
```

L'exécution du code ci-dessus nous donne le flag :
```
shaktictf{G00d!_c0nTinUe_Expl0r1nG_Mor3}
```

### Damez (100 - Easy)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Reversing/Damez/Damez.png" alt="Damez" align="center">
</p>

Après avoir récupéré l'exécutable [damez](https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Reversing/Damez/damez), nous lui donnons le droit d'exécution :
```bash
chmod +x damez
```

Et nous l'exécutons avec la commande suivante :
```bash
./damez
```

Il nous affiche le message suivant :
```
Error! file input.txt not found
```

L'exécution du programme après avoir créé un fichier **input.txt** avec n'importe quoi dedans nous donne le message suivant :
```
Try Again! :)
```

Avant d'aller plus loin, nous allons regarder si le flag peut être récupéré par le biais des chaînes de caractères présentes dans l'exécutable avec la commande suivante :
```bash
strings damez | awk 'length($0)>9'
```

Dans la liste qui s'affiche, nous trouvons notre flag :
```
shaktictf{K33p_th3_gam3_g0ing_gurl!}
```

L'analyse du code, a postériori, nous permettra de comprendre qu'il fallait que le fichier **input.txt** contienne le flag pour obtenir le message de validation :
```
You got it! Flag: shaktictf{K33p_th3_gam3_g0ing_gurl!}
```

## Forensics

### Shark on Wire (50 - Very Easy)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Shark%20on%20Wire/Shark%20on%20Wire.png" alt="Shark on Wire" align="center">
</p>

Après avoir récupéré le fichier [network1.pcapng](https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Shark%20on%20Wire/network1.pcapng), nous l'analysons dans Wireshark.

Nous allons consulter les statistiques des conversations via le menu **Statistiques** puis **Conversations**.

Dans cette nouvelle fenêtre, nous cliquons sur l'entête de la colonne **Bytes** afin que celle-ci soit classée en ordre croissant, nous effectuons un clic droit sur la dernière ligne (celle qui contient le plus de données) et dans le menu qui s'affiche, nous sélectionnons **Appliquer comme un filtre** puis **Sélectionné** et enfin **A <-> B** :

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Shark%20on%20Wire/wireshark1.png" alt="Wireshark 1" align="center">
</p>

Nous retournons dans la fenêtre principale de Wireshark où nous effectuons un clic droit sur la ligne dont la valeur de **Length** est la plus élevée (donc 529), dans le menu qui s'ouvre, nous sélectionnons **Suivre** puis **Flux TCP** :

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Shark%20on%20Wire/wireshark2.png" alt="Wireshark 2" align="center">
</p>

Nous récupérons notre flag :
```
shaktictf{wir3sh4rk_i5_ju5t_aw3s0m3}
```

### Zip Zap Zoo (100 - Easy)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Zip%20Zap%20Zoo/Zip%20Zap%20Zoo.png" alt="Zip Zap Zoo" align="center">
</p>

Après avoir téléchargé le fichier [challenge.zip](https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Zip%20Zap%20Zoo/challenge.zip), nous le décompressons avec la commande suivante :
```bash
unzip challenge.zip
```

Lors de la décompression, nous obtenons un fichier **file.zip** et un mot de passe :
```
Archive:  challenge.zip
Password:h4ckTh35t3R30tyP35
  inflating: file.zip
```

L'utilisation de la même commande sur ce nouveau fichier nous permet de constater qu'il est corrompu.  
Ce qui est confirmé par la commande suivante :
```bash
file file.zip
```

Dont voici le résultat :
```
file.zip: data
```

Alors que nous devrions avoir quelque chose de ce type :
```
challenge.zip: Zip archive data, at least v2.0 to extract
```

Dans un premier temps, regardons son entête et principalement ses **magics bytes** qui devraitent être **50 4B 03 04** :
```bash
xxd file.zip | head
```

Voici son entête où les **magics bytes** sont différents 50 4B **08 09** :
```
00000000: 504b 0809 1400 0900 0800 cb9b 8451 222d  PK...........Q"-
00000010: e8d4 5300 0000 4900 0000 0800 1c00 666c  ..S...I.......fl
00000020: 6167 2e74 7874 5554 0900 03f5 40ca 5ff5  ag.txtUT....@._.
00000030: 40ca 5f75 780b 0001 04e8 0300 0004 e803  @._ux...........
00000040: 0000 aba5 6617 c7d6 4cd2 d12c 04bc 10a3  ....f...L..,....
00000050: 1113 3fad acbe f197 6972 95dc 0fe5 9f45  ..?.....ir.....E
00000060: 2144 7180 4c58 19bb 7a49 e2ed a075 c7e9  !Dq.LX..zI...u..
00000070: 758a 9c20 3378 5072 b312 502e a047 8c98  u.. 3xPr..P..G..
00000080: 349e e77e 141e 0090 dfaf 3f6e 39de 925e  4..~......?n9..^
00000090: b18e 7c13 5a50 4b07 0822 2de8 d453 0000  ..|.ZPK.."-..S..
```

## Pwn

### Connect (50)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/blob/main/2020/Shakti_CTF/images/connect.png" alt="Connect" align="center">
</p>

On se connecte avec netcat :
```bash
nc 34.72.218.129 1111
```

On tape la commande *ls* qui nous donne une liste de fichiers dans laquelle il y a un fichier **flag.txt**.

On tape la commande *cat flag.txt* pour afficher le contenu du fichier :
```
shaktictf{w3lc0me_t0_th3_ar3na_c0mrade}
```

## Misc

### Sanity Check (1)
Il faut simplement se rendre sur le [Discord](https://discord.gg/gEJUZwe9ju) puis dans la catégorie "CTF INFORMATION" et enfin dans le salon "rules", on y trouve le flag :

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/blob/main/2020/Shakti_CTF/images/sanity_check.png" alt="Sanity Check" align="center">
</p>

```
shaktictf{i_solemly_swear_that_me_and_my_team_are_all_women}
```

## Cryptography

### 3,2,1..Go (50)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/blob/main/2020/Shakti_CTF/images/3_2_1_Go.png" alt="3,2,1..Go" align="center">
</p>

Le fichier *config.jpg* est le suivant :

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/blob/main/2020/Shakti_CTF/images/config.jpg" alt="config.jpg" align="center">
</p>

Une recherche sur Google de *Joan Clarke* me permet de trouver l'information suivante sur Wikipedia :
```
Joan Elisabeth Lowther Murray, née Clarke le 24 juin 1917 et morte le 4 septembre 1996, est une cryptologue britannique.  
Elle est principalement connue pour sa participation au décryptage de la machine Enigma qui codait les communications chiffrées du Troisième Reich.
```

L'image *config.jpg* m'a permis d'identifier le site [DCODE](https://www.dcode.fr).  
J'effectue donc une seconde recherche sur Google de *dcode enigma* et je trouve la page suivante :  
https://www.dcode.fr/chiffre-machine-enigma

Je copie/colle le texte et je configure les paramètres comme sur l'image :
```
WEQEXFTUXQHVOUFPSVLPTORHAFBQE
```

J'obtiens la phrase suivante :
```
YOUHAVECRACKEDTHEENIGMAGENIUS
```

Qui me donne le flag suivant :
```
shaktictf{you_have_cracked_the_enigma_genius}
```
