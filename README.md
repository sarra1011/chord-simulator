# Simulateur Chord

Simulateur interactif du protocole **Chord** (table de hachage distribuée, DHT) : anneau d'identifiants SHA-1, finger tables, lookup, arrivées et départs de nœuds.

**Démo en ligne : https://sarra1011.github.io/chord-simulator/**

Aucune installation : tout tourne dans le navigateur (un seul fichier `index.html`).

## Fonctionnalités

| Bloc | Ce qu'il fait |
|---|---|
| 1. Réseau | Crée un anneau : on choisit `m` (bits) et la liste des nœuds. Un nombre est un identifiant ; un mot est haché avec SHA-1 puis réduit modulo 2^m. |
| 2. Joindre un nœud | Ajoute un nœud et surligne les finger tables modifiées. |
| 3. Lookup | Anime le trajet d'une clé saut par saut, avec l'explication de chaque étape. Compare avec la recherche classique de successeur en successeur. |
| 4. Quitter le réseau | Départ volontaire ou panne brutale, puis réparation par stabilisation. |
| 5. Clés stockées | Insère des clés, avec réplication optionnelle sur le successeur. |
| 6. Concurrence | `p` arrivées et `q` départs en même temps, puis stabilisation tour par tour. |

Autres options : mode pas à pas, réglage de la vitesse, thème clair/sombre, exemples prêts à charger (cours `m=6`, TD exercice 1 `m=7`, TD exercice 2 `m=6`).

## Utilisation rapide

1. Ouvrir la démo : elle charge l'anneau de l'exercice 2 du TD (`m = 6`).
2. Cliquer sur **Lancer le lookup** : la clé 54 est cherchée depuis N8.
3. Cliquer sur un nœud de l'anneau pour voir sa finger table.
4. Essayer **Joindre**, **Panne brutale** ou **Concurrence** et observer la stabilisation.

## Lancer en local

```bash
git clone https://github.com/sarra1011/chord-simulator.git
cd chord-simulator
# ouvrir index.html dans un navigateur
```

## Rappel de l'algorithme

- Identifiant d'un nœud ou d'une clé : `SHA-1(nom) mod 2^m`.
- Finger table de `n` : `finger[i] = successeur((n + 2^i) mod 2^m)`, pour `i = 0 … m-1`.
- Lookup : à chaque étape, le nœud transmet la requête au doigt le plus éloigné qui précède la clé. Résultat en O(log N) sauts.
- Stabilisation : `stabilize`, `notify` et `fix_fingers` réparent l'anneau après les arrivées et départs.

## Contexte

Réalisé pour le TP Chord (DHT) du cours Systèmes et Applications Répartis, ENSI, Université de la Manouba. Inspiré du travail de Montassar.

## Auteure

Sarra Bahlous, élève ingénieure en informatique (II3 ST-IoT), ENSI.
GitHub : [sarra1011](https://github.com/sarra1011)
