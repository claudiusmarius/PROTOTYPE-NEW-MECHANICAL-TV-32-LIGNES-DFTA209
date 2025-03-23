# PROTOTYPE-NEW-MECHANICAL-TV-32-LIGNES-DFTA209



Ce depository a pour but de recenser tous les schémas pré validés pour la TV définitive.

1 > SynchrDISC :

https://youtu.be/teULYgM-BcQ

J'ai décidé d'utiliser une boucle à verrouillage de phase (PLL) CD4046).

Le signal optique reçu à travers les 32 trous de synchronisation situés en périphérie du DISC par la photo diode IR BPV23F est remis en forme et en phase grâce au transistor mosfet canl N Q8 (BS170) la photo diode est branchée en inverse elle se sature en présence d'un rayonnement infrarouge, le signal remis en forme est disponible sur le drain de Q8. Cette excellente remise en forme est nécessaire au bon fonctionnement du PLL (U10).

Ce signal remis en forme est nommé PULSESDISC, c'est lui qu'il faudra synchroniser avec les tops de synchro ligne en agissant sur le moteur DC M3.

PULSESDISC est présenté sur la pin 3 de U10 (COMP/IN).

Ce signal de synchro ligne (issu du signal de vidéo composite) est présenté sur la pin 14 de U10 (SIGNAL/IN)

Le PLL (U10) va comparer ces 2 signaux est envoyé un signal de sortie sur sa pin 13 (PHASE/COMP/II/OUT) cette sortie sera soit à l'état HAUT, BAS ou HI pour venir charger, décharger ou bloquer C5 via la résistance R28) et donc venir driver le moteur DC.

L'ensemble R30, R31 et P5 via contribuer à cette chaine de réglage, en intervenant sur P5 nous pouvons décaler l'image vers la gauche ou la droite afin de bien l'aligner avec le scanning lamp. Les valeurs de ces résistances ont été optimisées pour avoir l'image centrée avec la curseur de P5 au centre. Ces valeurs sont idéales pour le mosfet Q4 042N03L, il est possible qu'elles doivent être revues pour un autre mosfet.

Ce mosfet est monté sur un petit dissipateur qui pourra être monté directement sur PCB, il est légérement tiède. (Attention de ne pas avoir un boitier trop petit ou trop hermétique dans le projet final afin d'éviter une motée en température). Pour information la consommation du moteur est de quelques centaines de mA.

On peut remarquer la présence de R10 de R34 de 10 ohms 10W , elle permet de ne pas laisser à Q4 toute la dissipation de puissance à évacuer.

La diode D8 est optionnelle c'est une diode de roue libre (donc branchée en inverse) si le moteur DC est un moteur à balais, ce qui n'est pas le cas ici, notre moteur étant un moteur à aimants permanents XD-3420 DC 12V 3500rpm.

2 > SignauxVidéoLTSPICE

https://youtu.be/oKlO-2Si9WA

Le signal doit d'abord être mis à niveau : on le polarise à mi VCC par les 2 résistances par R69 et 73 (1M) puis nous faisons transiter le signal par un ampli suiveur U23.1, RP11 permet de l'atténuer si nécessaire, puis on aligne ce signal sur le 0V grâce au DC restorer U23.2.

Ensuite nous venons extraire les tops de synchro en inversant leur phase (on passe d'un puis de synchro à un top de synchro) et leur niveau. U23.3 est monté en comparateur.

Nous venons via le soustracteur U23.4 enlever le top de synchro du signal vidép composite la hauteur de synchro est ajustée par le potentiomètre RP9 le seuil de comparaison pour l'extraction des tops de synchro est à un niveau légérement inférieur, ce qui nous permet de n'utilser qu'un seul potentiomètre pour les 2 seuils.

Ensuite gràace à ce nouveau signal vidéo nous venons commander en courant le groupement de LEDs (3 fois 4)  dans le circuit source les diodes D13 et D14 permettent d'aporter une correcton gamma.
Cette commande en courant est principalement opérée grace à U15.1 et Q11.
RP10 a pour rôle de modifier le courant dans les LEDs c'est le réglage de luminosité.

