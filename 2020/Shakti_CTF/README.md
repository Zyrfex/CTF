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

Après avoir téléchargé le fichier [run](https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Reversing/Just-Run-It!/run), on lui donne le droit d'exécution :
```
chmod +x run
```

Et on le lance avec la commande suivante :
```
./run
```

Et on récupère le flag :
```
shaktictf{and_that's_how_you_run_a_linux_binary!}
```

### PYthn (100 - Easy)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Reversing/PYthn/PYthn.png" alt="PYthn" align="center">
</p>

Après avoir récupére le fichier [PYthn.py](https://github.com/Zyrfex/CTF/raw/main/2020/Shakti_CTF/Reversing/PYthn/PYthn.py), une analyse rapide du code nous permet de déterminer que la fonction **fuN()** n'est pas utilisée.

On utilise les fonctions dans le sens inverse pour récupérer notre flag :
```python
print("Le flag est : " + Fun(FuN(Q)))
```

L'exécution du code ci-dessus nous donne le flag :
```
shaktictf{G00d!_c0nTinUe_Expl0r1nG_Mor3}
```

## Pwn

### Connect (50)

<p align="center">
  <img src="https://github.com/Zyrfex/CTF/blob/main/2020/Shakti_CTF/images/connect.png" alt="Connect" align="center">
</p>

On se connecte avec netcat :
```
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
