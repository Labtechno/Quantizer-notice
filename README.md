# Quantizer Kassutronics · Manuel d’utilisation en français

**Étape 1 · Analyse et sommaire proposés à la validation.** Ce projet documente le module Eurorack à deux canaux pour un lecteur qui découvre la quantification. Le périmètre couvre les cartes 1.1 et 1.2 assemblées. La notice utilisateur porte elle-même le numéro 1.1. Le code étudié correspond au firmware v1.0.2. Ces trois numérotations désignent des objets différents.

## Ce que fait le module

Un oscillateur commandé en tension (VCO) produit le son. Son entrée de hauteur au standard 1 V/oct fait monter la note d’une octave quand la tension augmente de 1 V. Une octave comprend douze demi-tons, donc un demi-ton vaut 1/12 V, soit environ 83,3 mV. La note entendue à 0 V dépend de l’accord du VCO. Si on l’accorde en do, le repère 0 de la couronne se lit comme un do.

Le Quantizer reçoit une tension de commande (CV) et choisit une hauteur parmi les notes autorisées. En mode par défaut, il choisit la plus proche. Une montée continue du CV peut ainsi produire un escalier de notes. Avec seulement 0, 4 et 7 allumés et un VCO accordé en do, on peut entendre do, mi et sol se succéder. Les deux canaux ont leurs propres connexions et partagent la sélection de notes.

## Façade et commandes

- **Couronne** — Douze poussoirs lumineux représentent les douze demi-tons, du sommet vers la droite. En jeu normal, une touche allumée autorise cette note dans toutes les octaves. Un appui inverse son état. La gamme à l’initialisation est majeure (0, 2, 4, 5, 7, 9, 11). Au redémarrage, le module rappelle l’état mémorisé.
- **Rangée de fonctions**, de gauche à droite — Maison/Shift pour sortir d’un menu ou accéder aux fonctions secondaires, rotation antihoraire/descente d’octave, rotation horaire/montée d’octave, disquette pour charger une gamme (Shift + disquette pour enregistrer).
- **Deux groupes de quatre prises** — Pour chaque canal, Trig reçoit le signal de déclenchement, Gate envoie la commande d’articulation, In reçoit la tension à quantifier et Out fournit la hauteur au VCO. Chaque Gate dispose d’un témoin dédié. Les deux prises centrales A et B reçoivent les CV de modulation.
- **Réglages physiques** — Aucun potentiomètre en façade. Les trois ajustables RV1, RV2 et RV3 sur la carte servent à la calibration. La notice illustrera les touches et voyants du Quantizer et indiquera les réglages des autres modules selon leur rôle dans le patch.

| Shift + touche de la couronne | Fonction accessible en jeu normal |
|---|---|
| 0 | Choisir la durée du Gate |
| 1 | Placer la rotation de gamme sur le repère choisi |
| 2 / 3 | Transposer les deux canaux / ajouter une transposition au canal 2 |
| 4 / 5 | Décaler les entrées des deux canaux / ajouter un décalage au canal 2 |
| 6 | Jouer les deux sorties comme un clavier CV |
| 7 | Basculer entre staccato et legato |
| 8 | Choisir la règle de quantification |
| 9 | Régler le retard de lecture après Trig |
| 10 / 11 | Affecter ou désactiver l’entrée CV A / B |

## Jeu, rythme et mémoire

| Fonction | Effet pratique |
|---|---|
| Jeu libre et jeu déclenché | En jeu libre, le canal suit les changements de hauteur et émet un Gate lors d’un changement de note. Avec Trig, un front montant commande la lecture du CV. Entre deux déclenchements la hauteur est tenue. |
| Trois règles | **Nearest** produit la note autorisée la plus proche. **Skip** ignore un demi-ton exclu et son Gate dans l’usage décrit par la notice. **Equally distributed** répartit l’octave d’entrée en zones de même largeur. Avec quatre notes, chacune occupe 0,25 V. Une probabilité égale suppose une source répartie uniformément sur l’octave. |
| Rotation, décalage, transposition | La rotation déplace les notes autorisées sur la couronne. Le décalage (*Offset*) s’ajoute à la tension **avant** le choix de la note. La transposition (*Transpose*) déplace le résultat **après** ce choix. Le réglage supplémentaire du canal 2 permet notamment de créer un intervalle entre deux voix alimentées par le même CV. |
| Gate | Douze durées nominales, d’environ 1 ms à 2 s. En staccato, une brève coupure sépare deux articulations. En legato, un Gate encore haut peut se prolonger. Le retard de Trig, réglable de 0 à 11 ms nominaux, sert quand le séquenceur envoie l’impulsion avant la stabilisation de sa hauteur. |
| Clavier | En mode clavier, une touche de la couronne joue la même note aux deux sorties. Les deux flèches changent l’octave. Ce mode fournit une référence pour accorder deux VCO. |
| CV A et B | Rotation, transposition, décalage, rappel de gamme et, dans le firmware étudié, durée du Gate. Pour une modulation de hauteur individuelle, A agit sur le canal 1 et B sur le canal 2. Le rappel de gamme parcourt les cases par demi-tons et revient à la case 0 à +1 V. Pour désactiver A, entrer dans son menu puis rappuyer sur sa touche. Même geste pour B. |
| Mémoire | Douze cases utilisateur, initialement vides. Une case contient le motif de gamme tel qu’il est tourné lors de la sauvegarde. La sauvegarde automatique de l’état de travail est distincte, environ 10 s après une manipulation qui arme sa minuterie. Voir la réserve sur le legato. |

## Installation et limites établies

| Donnée | Valeur ou consigne issue du dépôt |
|---|---|
| Façade | 10 HP de largeur. Le plan donne 50,5 × 128,5 mm. |
| Alimentation | +12 V et −12 V. Consommation typique de 70 mA sur +12 V et 30 mA sur −12 V. |
| Nappe côté module | J4, deux rangées de cinq broches. 1–2 au −12 V, 3–8 à la masse, 9–10 au +12 V. La photo arrière de la révision 1.1 montre STRIPE du côté « − ». La vue de carte 1.2 porte les marquages −12, GND et +12. Illustrer le branchement hors tension en suivant les repères du module et du bus. |
| Chemin de hauteur | Plage typique annoncée de ±5,33 V pour In, A, B et les sorties de hauteur Out. Pas nominal de 83,3 mV. Hystérésis typique de 10 mV et échantillonnage de 4,8 kHz par canal. |
| Signaux de rythme | Seuil de Trig décrit comme inférieur à 1 V. Niveau haut de Gate d’environ 9 V. |
| Calibration | Mode clavier et voltmètre continu. RV2 règle le zéro de la sortie gauche, RV1 l’échelle à +5 V, RV3 le zéro de la sortie droite. Vérifications complémentaires à −5 V et sur les deux canaux. |
| Cartes DIY | Sur 1.1, l’auteur documente un possible court-circuit fugitif du +12 V à la masse lors du branchement ou retrait d’un câble Trig et donne une modification recommandée. La 1.2 intègre la correction. La documentation 1.2B précise aussi que D6 doit être omise sur toutes les révisions. Une protection contre l’inversion dépend donc du montage réel. |

## Sommaire proposé et illustrations

| Chapitre | Contenu et planches prévues |
|---|---|
| 1. D’une tension à une mélodie | CV, hauteur, VCO, octave, demi-ton, gamme, note de référence. Courbe continue et escalier sur le même axe, clavier et tensions relatives pour un VCO accordé en do. |
| 2. Lire la façade | Vue de face SVG numérotée, légende des 16 touches, des 10 prises et des deux témoins. Vue 3D schématique pour repérer façade, cartes et alimentation. |
| 3. Installer le module | Identifier la révision, prévoir la place et le courant, reconnaître J4 et le −12 V, brancher hors tension. Vues arrière orientées et encadré spécifique à la 1.1. |
| 4. Entendre ses premières notes en cinq minutes | LFO lent vers In 1, Out 1 vers V/oct du VCO, chemin audio du VCO vers l’écoute. Départ en jeu libre, sélection de trois notes, résultat audible et témoin Gate. |
| 5. Construire une gamme à l’oreille | Activer, retirer, retrouver la majeure, réduire à un accord, tourner d’un demi-ton, placer la rotation. Couronne et clavier côte à côte, avant/action/après. |
| 6. Donner un rythme aux notes | Jeu libre, front montant, maintien entre deux Trig, Gate vers enveloppe, staccato et legato, durée et retard de lecture. Chronogrammes alignés sur la même impulsion. |
| 7. Choisir la règle de quantification | Comparer Nearest, Skip et Equally distributed avec la même gamme et la même tension d’entrée. Tracer Out et Gate, y compris lors d’une note rejetée. |
| 8. Jouer deux voix et les accorder | Mode clavier, changement d’octave, accord de deux VCO. Rotation, Offset, Transpose et réglages du canal 2. Comparer un décalage avant quantification à une quinte fixe après quantification. |
| 9. Piloter le module par CV | Affecter et désactiver A/B, moduler les hauteurs, la rotation, la durée du Gate ou le rappel des gammes. Montrer le geste, les voyants et la destination. |
| 10. Mémoriser et rappeler | Sauver, charger, annuler, identifier une case occupée, rappeler par CV et retrouver l’état du module après extinction. Distinguer le contenu d’une case et celui de la sauvegarde automatique. |
| 11. Carnet de patchs | LFO mélodique, tension aléatoire tenue par un Sample & Hold, séquenceur non quantifié avec Trig, transposition par CV, harmonisation à deux VCO, progression par rappel de gammes. Un câblage complet et un résultat à écouter pour chaque exemple. |
| 12. Dépanner et vérifier la justesse | Aucune note audible, hauteur figée, note précédente au déclenchement, gamme inattendue, décalage constant ou écart qui grandit avec l’octave. Arbre de diagnostic, puis calibration au multimètre en annexe technique. |
| Annexes | Caractéristiques et limites, aide-mémoire Shift, glossaire, sources et points à confirmer. Fiches vierges avec couronne, réglages, connexions, conditions de départ et notes d’écoute. |

La version HTML prévue sera un fichier autonome, avec CSS et SVG intégrés. La scène 3D illustrera les relations mécaniques documentées. Chaque manipulation aura ses vues avant/action/après et chaque patch distinguera hauteur, déclenchement et audio par le tracé et la légende. Le PDF imprimable sera préparé après validation de l’HTML complet.

## Sources primaires

- [Dossier Quantizer du dépôt Kassutronics, révision consultée](https://github.com/kassu/kassutronics/tree/d977ae3f548837fe81dcc37031e4a6732b055f11/documentation/Quantizer)
- [Manuel utilisateur 1.1, p. 1–7](https://github.com/kassu/kassutronics/blob/d977ae3f548837fe81dcc37031e4a6732b055f11/documentation/Quantizer/Quantizer_User_Manual_1.1.pdf)
- [Sérigraphie de façade 1.1](https://github.com/kassu/kassutronics/blob/d977ae3f548837fe81dcc37031e4a6732b055f11/documentation/Quantizer/QuantizerPanel_1.1.ai)
- [Guide de montage 1.1B, notamment p. 2, 5 et 8–9](https://github.com/kassu/kassutronics/blob/d977ae3f548837fe81dcc37031e4a6732b055f11/documentation/Quantizer/Quantizer_Build_Docs_1.1B.pdf) et [photo arrière de J4, repère STRIPE](https://github.com/kassu/kassutronics/blob/d977ae3f548837fe81dcc37031e4a6732b055f11/documentation/Quantizer/Build%20Photos/IMG_1561.jpg)
- [Guide de montage 1.2B, caractéristiques p. 2, calibration p. 7, cartes et schémas p. 10–13, commentaires et dimensions p. 14–17](https://github.com/kassu/kassutronics/blob/d977ae3f548837fe81dcc37031e4a6732b055f11/documentation/Quantizer/Quantizer_Build_Docs_1.2B.pdf)
- [Firmware officiel référencé par le README, version v1.0.2](https://github.com/kassu/KassutronicsQuantizer/tree/86de512046274b94288ac69af0ff0d4394856bb6/KassutronicsQuantizer) et [précision de l’auteur sur la désactivation des entrées CV](https://github.com/kassu/KassutronicsQuantizer/issues/4)

[Points à confirmer avant publication](notes/points-a-confirmer.md)
