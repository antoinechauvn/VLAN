# VLAN
Notion de Réseau local Virtuel (Norme IEEE 802.1Q)

### Qu'est ce qu'un Vlan?

```
Un VLAN est ni plus ni moins qu’un réseau virtuel, orchestré par un commutateur réseau tel qu’un Switch de niveau 2 (N2 ou N3). 
```

#### Avantages:

```
-Segmentation logique du réseau afin de garantir des performances optimales.
-Gain en sécurité
-Réduction de la diffusion du traffic sur le réseau
```

### VLAN TAGGED
```
Un port de switch configuré en “tagged” signifie que l'équipement branché derrière est capable de traiter les tags 802.1q et qu'il
est configuré pour les traiter. Le port du switch envoie le trafic sans avoir retiré le tag (identifiant) du VLAN.
```

### VLAN UNTAGGED
```
Un port de switch configuré en “untagged” signifie que la notion de VLAN est totalement transparente pour l'équipement branché
derrière. C'est-à-dire qu'il ignore son VLAN de rattachement. C'est le switch qui utilise l'id VLAN associé pour son traitement
interne pour la distribution des paquets sur ses ports. Les paquets ne sont pas taggués 802.1q en entrée et en sortie des ports
du switch configurés en “untagged”.
```

