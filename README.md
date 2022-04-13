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

## Trame ethernet
| adresse MAC dst | adresse MAC source | Taille de la trame/EtherType	| Data | FCS |
| :-: | :-: | :-: | :-: | :-: |

## Trame ethernet modifiée
| adresse MAC dst | adresse MAC source | Tag (inséré) | Taille de la trame/EtherType	| Data | FCS (modifié) |
| :-: | :-: | :-: | :-: | :-: | :-: |

*_Le champ FCS est recalculé après l'insertion de la balise de VLAN._

## Contenu du champ "Tag:IEEE 802.1Q"
| TPID (16 bits) | TCI (16 bits) |
| :-: | :-: |

## Tag protocol identifier, TPID
```
Les 16 premiers bits sont utilisés pour identifier le protocole de la balise insérée. Dans le cas de la balise 802.1Q la valeur
de ce champ est fixée à 0x8100.
```

## Contenu du champ TCI (Tag control information)
| Priority (3 bits) | CFI (1 bit) | Vlan ID, VID (12 bits) |
| :-: | :-: | :-: |

## Priorité ( PCP : Priority Code Point )
Ce champ de 3 bits fait référence au standard IEEE 802.1p. Sur 3 bits on peut coder 8 niveaux de priorité de 0 à 7. Ces 8 niveaux sont utilisés pour fixer une priorité aux trames d'un VLAN relativement aux autres VLAN. La notion de priorité dans les VLAN (niveau 2) est indépendante des mécanismes de priorité IP (niveau 3).

## Canonical Format Identifier, CFI
Ce champ codé sur 1 bit assure la compatibilité entre les adresses MAC Ethernet et Token Ring. Un commutateur Ethernet fixera toujours cette valeur à 0. Si un port Ethernet reçoit une valeur 1 pour ce champ, alors la trame ne sera pas propagée puisqu'elle est destinée à un port «sans balise» (untagged port).

## VLAN Id, VID
Ce champ de 12 bits sert à identifier le virtual lan (VLAN) auquel appartient la trame. Il est possible de coder 4094 VLAN (de 1 à 4094) avec ce champ. La valeur "0" signifie qu'il n'y a pas de VLAN, et la valeur 4095 est réservée. Les valeurs 1002 à 1005 sont réservées pour des protocoles de niveau 2 différents d'Ethernet.
