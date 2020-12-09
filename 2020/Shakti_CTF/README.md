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

Voici son entête, nous remarquons que les **magics bytes** sont différents 50 4B **08 09** :
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

Nous corrigeons l'entête en remplaçant 50 4B **08 09** par 50 4B **03 04** et enregistrons nos modifications :
```bash
sudo apt install hexedit
hexedit file.zip
```

L'utilisation à nouveau de la commande *unzip file.zip* nous donne encore une erreur :
```
Archive:  file.zip
  End-of-central-directory signature not found.  Either this file is not
  a zipfile, or it constitutes one disk of a multi-part archive.  In the
  latter case the central directory and zipfile comment will be found on
  the last disk(s) of this archive.
unzip:  cannot find zipfile directory in one of file.zip or
        file.zip.zip, and cannot find file.zip.ZIP, period.
```

Nous allons donc réparer le fichier avec la commande suivante :
```bash
zip -FF file.zip --out fixed.zip
```

Qui nous donne le résultat suivant :
```
Fix archive (-FF) - salvage what can
        zip warning: Missing end (EOCDR) signature - either this archive
                     is not readable or the end is damaged
Is this a single-disk archive?  (y/n): y
  Assuming single-disk archive
Scanning for entries...
 copying: flag.txt  (83 bytes)
Central Directory found...
EOCDR found ( 1    243)...
        zip warning: unexpected signature 50 4b 0e 0d on disk 0 at 662196

        zip warning: skipping this signature...
        zip warning: unexpected signature 50 4b 0e 0d on disk 0 at 5704878

        zip warning: skipping this signature...
```

Essayons de décompresser ce nouveau fichier réparé :
```
unzip fixed.zip
```

Un mot de passe nous est demandé, nous utilisons celui récupéré au début : h4ckTh35t3R30tyP35
```
Archive:  fixed.zip
[fixed.zip] flag.txt password:
  inflating: flag.txt
```

Le fichier *flag.txt* est extrait de l'archive, lisons le :
```bash
cat flag.txt
```

Nous récupérons une chaîne de caractères qui peut s'apparenter à du *base32* :
```
ONUGC23UNFRXIZT3PE2HSWKZPF4VSIK7LEYHKX3HGB2F6MLUL42DAOJVGE2TGOJYPU======
```

Essayons de la décoder :
```bash
echo "ONUGC23UNFRXIZT3PE2HSWKZPF4VSIK7LEYHKX3HGB2F6MLUL42DAOJVGE2TGOJYPU======" | base32 -d
```

Voilà notre flag :
```
shaktictf{y4yYYyyY!_Y0u_g0t_1t_409515398}
```

### Not That Easy (200 - Medium)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Not%20That%20Easy/Not%20That%20Easy.png" alt="Not That Easy" align="center">
</p>

Après avoir récupéré le fichier [network2.pcapng](https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Not%20That%20Easy/network2.pcapng), nous l'analysons dans Wireshark.

Nous utilisons la même méthode que celle utilisée dans l'épreuve **Shark on Wire** pour filtrer la conversation.

Nous constatons dans les données la présence des caractères "PNG" qui semblent nous aiguiller vers une image de ce format. 

Après avoir sélectionné la ligne dont la colonne **Length** est la plus élevée, nous faisons un clic droit sur la partie **Data** puis dans le menu nous choisissons **Exporter Paquets Octets...** :
<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Not%20That%20Easy/wireshark1.png" alt="Wireshark 1" align="center">
</p>

Nous enregistrons nos données sous le nom **image.png** :
<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Not%20That%20Easy/wireshark2.png" alt="Wireshark 2" align="center">
</p>

Nous récupérons cette image :
<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Forensics/Not%20That%20Easy/image.png" alt="image.png" align="center">
</p>

Nous voyons tout de suite qu'il s'agit d'un QRCode, nous le lisons de cette manière :
```bash
sudo apt install zbar-tools
zbarimg image.png
```

Et nous obtenons notre flag :
```
shaktictf{sh3_w4s_h0n0r3d_by_3lectr0nic_fr0nti3r_f0und4ti0n}
```

## Steganography

### Hidd3n (100 - Easy)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Steganography/Hidd3n/Hidd3n.png" alt="Hidd3n" align="center">
</p>

Il nous faut donc trouver le flag dans l'image ci-dessous : [image.jpg](https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Steganography/Hidd3n/image.jpg)
<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Steganography/Hidd3n/image.jpg" alt="image.jpg" align="center">
</p>

Dans un premier temps, nous analysons le fichier avec **exiftool** :
```bash
exiftool image.jpg
```

Celui-ci contient un commentaire encodé, surement en **base64** :
```
ExifTool Version Number         : 12.10
File Name                       : image.jpg
Directory                       : .
File Size                       : 44 kB
File Modification Date/Time     : 2020:12:04 13:43:06-05:00
File Access Date/Time           : 2020:12:04 13:43:25-05:00
File Inode Change Date/Time     : 2020:12:04 13:43:17-05:00
File Permissions                : rw-------
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Comment                         : cGFzc3BocmFzZT1qdTV0ZmluZG0z
Image Width                     : 800
Image Height                    : 600
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Image Size                      : 800x600
Megapixels                      : 0.480

```

Essayons de décoder ce commentaire avec la commande suivante :
```bash
echo "cGFzc3BocmFzZT1qdTV0ZmluZG0z" | base64 -d
```

Bingo, ce qui nous laisse penser qu'un fichier est caché dans l'image :
```
passphrase=ju5tfindm3
```

Nous allons l'extraire avec la commande :
```bash
steghide --extract -sf image.jpg -p ju5tfindm3
```

Puis lire le ficher **flag.txt** avec la commande :
```
cat flag.txt
```

Voilà notre flag :
```
"In engineering, the point is to get the job done, and people are happy to help. You should be generous with credit, and you should be happy to help others." Who am I?

Here is your flag: shaktictf{G00d!_b3st_0f_luck_f0r_th3_n3xt_chall3nge}
```

## Pwn

### Connect (50)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Pwn/Connect/Connect.png" alt="Connect" align="center">
</p>

Vous pouvez récupérer le binaire ici : [chall](https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Pwn/Connect/chall)

Nous nous connectons avec **netcat** :
```bash
nc 34.72.218.129 1111
```

Nous tapons la commande **ls** qui nous donne une liste de fichiers dans laquelle il y a un fichier **flag.txt**.

Nous tapons la commande **cat flag.txt** pour afficher le contenu du fichier :
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
