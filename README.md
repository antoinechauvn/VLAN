# VLAN
Notion de Réseau local Virtuel (Norme IEEE 802.1Q)

### Qu'est ce qu'un Vlan?

```
Un VLAN est ni plus ni moins qu’un réseau virtuel, orchestré par un commutateur réseau tel qu’un Switch
de niveau 2(N2 ou N3). 
```

#### Avantages:

```
-Segmentation logique du réseau afin de garantir des performances optimales.
-Gain en sécurité
-Réduction de la diffusion du traffic sur le réseau
```

### VLAN TAGGED
```
Un port de switch configuré en “tagged” signifie que l'équipement branché derrière est capable de traiter
les tags 802.1q et qu'il est configuré pour les traiter. Le port du switch envoie le trafic sans avoir
retiré le tag (identifiant) du VLAN.
```
![VLAN-TAG](https://user-images.githubusercontent.com/83721477/163259378-64dc352d-6dec-45d4-b7fe-56f502a2c605.jpg)

1. Un hôte enverra une trame sans balise
2. La trame entre dans un port non balisé sur le commutateur 1, configuré avec le VLAN 10 dans ce cas. Le commutateur ajoute la balise VLAN à la trame
3. Le commutateur 1 détermine que le port 2 doit envoyer cette trame au commutateur 2. Il s'agit d'un port étiqueté, il vérifie donc que le VLAN 10 est autorisé sur ce port. Si c'est le cas, il laisse la balise intacte et envoie la trame. Si le VLAN 10 n'est pas autorisé, il abandonne la trame
4. Le commutateur 2 reçoit la trame sur le port étiqueté 1. Ce commutateur détermine également si le VLAN 10 est autorisé sur ce port et le supprime si ce n'est pas le cas. Le commutateur 2 détermine que le port 2 doit envoyer la trame
5. Étant donné que le port 2 est un port non étiqueté, il supprime l'étiquette de la trame, puis l'envoie
6. L'hôte B reçoit la trame non étiquetée

### VLAN UNTAGGED
```
Un port de switch configuré en “untagged” signifie que la notion de VLAN est totalement transparente pour l'équipement branché
derrière. C'est-à-dire qu'il ignore son VLAN de rattachement. C'est le switch qui utilise l'id VLAN associé pour son traitement
interne pour la distribution des paquets sur ses ports. Les paquets ne sont pas taggués 802.1q en entrée et en sortie des ports
du switch configurés en “untagged”.
```
![VLAN-UNTAG](https://user-images.githubusercontent.com/83721477/163259255-0c950335-c1be-402e-81b2-0b53b510f231.jpg)
1. L'hôte A envoie le trafic au commutateur. Le trafic n'a pas de balise VLAN
2. La trame est reçue sur le port 1 du commutateur. Il s'agit d'un port non balisé, configuré avec l'ID VLAN 10. Le commutateur insère ensuite la balise VLAN dans la trame
3. Le commutateur détermine que la trame doit être transférée hors du port 2. Il s'agit également d'un port non balisé, donc la balise VLAN est retirée de la trame
4. L'hôte B reçoit la trame non étiquetée normalement

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
