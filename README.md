# Projet de Thermodynamique — Relations de Maxwell

**Université Hassan Ier — FST Settat** 
**Filière :** Cycle Ingénieur Procédés et Ingénierie Chimique (PIC)

## Description

Ce projet étudie les **relations de Maxwell en thermodynamique** à travers des démonstrations mathématiques, des calculs symboliques et des simulations Python.

L'objectif est d'appliquer les relations de Maxwell à deux modèles de gaz : le gaz parfait et le gaz de Van der Waals, afin de comparer leurs propriétés thermodynamiques et de comprendre les effets des interactions moléculaires.

## Objectifs du projet

- Démontrer les quatre relations de Maxwell à partir des potentiels thermodynamiques.
- Étudier et comparer les équations d'état du gaz parfait et du gaz de Van der Waals.
- Calculer et vérifier des dérivées partielles analytiquement et numériquement.
- Étudier la variation de l'énergie interne lors d'une détente isotherme.
- Calculer la différence entre les capacités calorifiques molaires \(C_p-C_v\).
- Vérifier une seconde relation de Maxwell à pression constante.
- Tracer des graphiques et interpréter les résultats physiques.

## Technologies utilisées

- **Python** : langage de programmation.
- **NumPy** : calculs numériques.
- **SymPy** : dérivations symboliques.
- **Matplotlib** : visualisation graphique.

## Conditions de simulation

Les simulations sont réalisées à une température de **320 K**, pour une mole de fluide et des volumes molaires compris entre \(5\times10^{-4}\) et \(5\times10^{-3}\ \mathrm{m^3/mol}\).

Le modèle de Van der Waals utilise les paramètres pédagogiques suivants :

- Constante des gaz parfaits : \(R=8.314462618\ \mathrm{J/(mol\cdot K)}\)
- Paramètre d'attraction moléculaire : \(a=0.364\ \mathrm{Pa\cdot m^6/mol^2}\)
- Paramètre de volume moléculaire : \(b=4.267\times10^{-5}\ \mathrm{m^3/mol}\)

La condition \(v>b\) doit être respectée pour le modèle de Van der Waals.

## Organisation du projet

Le projet comprend les démonstrations théoriques, les calculs manuels, un script Python commenté, les simulations numériques, les graphiques comparatifs et une conclusion scientifique.

## Installation et exécution

1. Installer Python.
2. Installer les bibliothèques nécessaires :

   ```bash
   pip install numpy sympy matplotlib
   ```

3. Ouvrir le repository dans Visual Studio Code.
4. Exécuter le script principal :

   ```bash
   python main.py
   ```

## Résultats attendus

Le projet permet de comparer les deux modèles, de vérifier les relations thermodynamiques par le calcul symbolique et numérique, et d'étudier l'influence des paramètres de Van der Waals sur la pression, l'énergie interne et les capacités calorifiques.

## Auteur et référence

Projet d'application réalisé dans le cadre du module de Thermodynamique, Cycle Ingénieur PIC, FST Settat.

**Référence du cours :** Pr. BAKHER Zine Elabidine — *Thermodynamique, Chapitre 2 : Systèmes fermés à composition constante*, 9 octobre 2026.

