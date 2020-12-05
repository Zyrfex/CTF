# Shakti CTF

Vous trouverez ci-dessous mes solutions pour ce CTF.  
  
Le flag a le format suivant :
```
shaktictf{[A-Za-z0-9_]*}
```

*Je n'ai pas eu le temps de rédiger la suite, l'accès aux épreuves n'est plus possible, désolé.*

## Pwn

### Connect (50 - Very Easy)

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

### Sanity Check (1 - Very Easy)
Il faut simplement se rendre sur le [Discord](https://discord.gg/gEJUZwe9ju) puis dans la catégorie "CTF INFORMATION" et enfin dans le salon "rules", on y trouve le flag :
<p align="center">
  <img src="https://github.com/Zyrfex/CTF/blob/main/2020/Shakti_CTF/images/sanity_check.png" alt="Sanity Check" align="center">
</p>
```
shaktictf{i_solemly_swear_that_me_and_my_team_are_all_women}
```
