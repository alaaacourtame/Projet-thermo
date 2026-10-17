# ÉTAPE 1 — RETROUVER LES QUATRES RELATIONS DE MAXWELL



# ÉTAPE 2 — CONSTRUIRE LES DEUX ÉQUATIONS D'ÉTATS 



# 'import' permet d'importer une bibliothèque (une boîte à outils) pour utiliser ses fcts
# 'as np' crée un raccourci : au lieu d'écrire "numpy.fonction", on écrira "np.fonction"
import numpy as np

R = 8.314462618  # Constante des gaz parfaits
a = 0.364        # Constante 'a' de Van der Waals
b = 4.267e-5     # Constante 'b' de Van der Waals 

# FONCTION GAZ PARFAIT
# 'def' signifie "définition" permet de créer une fct qui réalise un calcul précis
# 'p_ideal(T, v)' est le nom de la fonction. Entre parenthèses, on met les "paramètres" ici T et v
def p_ideal(T, v):

    # 'return' signifie "retourner" ou "renvoyer"
    #  Renvoie le résultat calculé par la fct pour pouvoir le réutiliser 
    # 'return R*T/v' renvoie la pression du gaz parfait
    return R*T/v

# FONCTION VAN DER WAALS
# Création d'une deuxième fonction nommée 'p_vdw'
def p_vdw(T, v):

    # 'if' signifie "si", permet de vérifier une condition
    # 'np.any(...)' vérifie si au moins une valeur est vraie(respecte la condition donnée)
    # 'np.asarray(v)' transforme v en tableau NumPy pour pouvoir travailler avec une ou plusieurs valeurs
    # '<= b' vérifie si le volume est plus petit ou égal à 'b'
    if np.any(np.asarray(v) <= b):

        # 'raise' signifie "lever" (une erreur)
        # 'ValueError' est le type d'erreur
        # 'raise ValueError' affiche une erreur et arrête le calcul si une valeur ne respecte pas la condition demandée
        # Si le volume est <= b, le programme s'arrête net et affiche ce texte en rouge
        raise ValueError("Le volume doit etre superieur a b")
    
    # Si la condition du 'if' est fausse (donc v > b), le programme ignore l'erreur ci-dessus 
    # 'return' renvoie le résultat de la formule de Van der Waals
    return R*T/(v-b) - a/v**2

# On donne des valeurs numériques à T et v pour faire les calculs
T = 320.0
v = 1.0e-3

# 'print' affiche le texte et le résultat dans le terminal 
# On "appelle" la fonction p_ideal en lui donnant T et v 
# Le résultat renvoyé par 'return' est récupéré ici, puis divisé par 1e5 (pour convertir en bar)
print("Gaz parfait (bar) :", p_ideal(T,v)/1e5)
print("Van der Waals (bar) :", p_vdw(T,v)/1e5)



# ÉTAPE 3 — DÉRIVEÉ SYMBOLIQUEMENT ET VÉRIFIER NUMÉRIQUEMENT



# On importe SymPy, la bibliothèque pour faire des maths avec des lettres
import sympy as sp

# 'sp.symbols' crée des variables symboliques pour écrire des formules mathématiques 
# On crée Ts, vs, Rs, aa, bb
# 'positive=True' dit à l'ordinateur que ces lettres sont positives 
Ts, vs, Rs, aa, bb = sp.symbols("T v R a b", positive=True)

# On écrit la formule de Van der Waals
P = Rs*Ts/(vs-bb) - aa/vs**2

# 'sp.diff' calcule la dérivée d'une expression 
# On dérive P par rapport à Ts
dP_dT = sp.diff(P, Ts)
# On dérive P par rapport à vs 
dP_dv = sp.diff(P, vs)

# 'sp.simplify' simplifie une expression mathématique 
print("dP/dT =", sp.simplify(dP_dT))
print("dP/dv =", sp.simplify(dP_dv))

# Pour la différence finie (h = 0.01)
h = 0.01

# Calcul numérique (avec les vraies valeurs) de la dérivée
# On utilise la formule de la différence finie centrée : [P(T+h) - P(T-h)] / (2*h)
# On appelle notre fonction python p_vdw créée à l'étape 2.
dP_dT_num = (p_vdw(T+h,v)-p_vdw(T-h,v))/(2*h)

# Calcul de la dérivée exacte (théorique) avec les valeurs numériques
dP_dT_exact = R/(v-b)

# 'abs()' donne la valeur absolue d'un nombre (pour calculer l'erreur)
# L'erreur relative est : |valeur numérique - valeur exacte| / |valeur exacte|
erreur = abs(dP_dT_num-dP_dT_exact)/abs(dP_dT_exact)

print("Derivee numerique :", dP_dT_num)
print("Erreur relative :", erreur)



# ÉTAPE 4 — APPLICATION DE MAXWELL À L'ÉNERGIE INTERNE



v1 = 1.0e-3
v2 = 2.0e-3

# Application directe de la formule mathématique intégrée : Delta U = a*(1/v1 - 1/v2)
delta_U_vdw = a*(1/v1 - 1/v2)

# Pour un gaz parfait, Delta U = 0
delta_U_ideal = 0.0

print("Delta U Van der Waals (J/mol) :", delta_U_vdw)



# ÉTAPE 5 — RELATION DE MAYER GÉNÉRALISÉE : C p − C v



# On crée une nouvelle fonction 'cp_moins_cv_vdw' qui prend T et v
def cp_moins_cv_vdw(T, v):

    # Calcul intermédiaire de la dérivée partielle de P par rapport à T
    dptd = R/(v-b)

    # Calcul intermédiaire de la dérivée partielle de P par rapport à v
    dpdv = -R*T/(v-b)**2 + 2*a/v**3
    
    # 'np.isclose' vérifie si une valeur est proche d'une autre valeur , avec une certaine tolérance (presque égale à 0 , avec une tolérance 'atol')
    # C'est une sécurité : si dpdv est proche de 0, la formule mathématique va planter (car on divise par dpdv à la fin)
    if np.any(np.isclose(dpdv, 0, atol=1e-12)):

        # Si c'est le cas, on lève une erreur pour arrêter le programme
        raise ValueError("Derivee en volume proche de zero")
        
    # 'return' renvoie le résultat final de la formule de Mayer
    return -T*dptd**2/dpdv

# Affichage : pour un gaz parfait, Cp - Cv = R
print("Cp-Cv ideal :", R)

# Affichage : on appelle notre fonction avec nos valeurs T et v
print("Cp-Cv VdW :", cp_moins_cv_vdw(T,v))



# ÉTAPE 6 — VÉRIFIER UNE SECONDE RELATION DE MAXWELL AVEC G



# On utilise les dérivées symboliques calculées à l'étape 3
# On calcule le quotient -dP_dT/dP_dv de manière symbolique 
dvdT_P = sp.simplify(-dP_dT/dP_dv)

# '.subs()' est une méthode de SymPy qui signifie "substituer":remplace les variables symboliques par des valeurs données
# Ici, on dit : "Remplace la lettre Ts par le nombre T, vs par v, Rs par R, etc"
valeur = dvdT_P.subs({Ts:T, vs:v, Rs:R, aa:a, bb:b})

# 'float()' convertit une valeur en nombre décimal
print("(dv/dT)P :", float(valeur))

# La relation de Maxwell donne (dS/dP)T = -(dv/dT)P, donc on ajoute un signe moins
print("(dS/dP)T :", -float(valeur))



# ÉTAPE 7 — GRAPHIQUES, SYNTHÈSE ET INTERPRÉTATION



# On importe la partie graphique de Matplotlib
import matplotlib.pyplot as plt

# 'np.linspace(début, fin, nombre)' crée une série de valeurs régulièrement espacées (tableau de 250 valeurs réparties uniformément entre 5e-4 et 5e-3) 
#  C'est ce qui va servir d'axe X pour le graphique
volumes = np.linspace(5e-4, 5e-3, 250)

# 'plt.plot(X, Y, label="...")' trace la courbe avec les volumes en X et la pression en Y (divisée par 1e5 pour être en bar)
plt.plot(volumes, p_ideal(T,volumes)/1e5, label="Gaz parfait")

# On trace la courbe de Van der Waals
plt.plot(volumes, p_vdw(T,volumes)/1e5, label="Van der Waals")

# 'plt.xlabel' nomme l'axe X et 'plt.ylabel' nomme l'axe Y
plt.xlabel("Volume molaire (m3/mol)")
plt.ylabel("Pression (bar)")

# 'plt.title' ajoute un titre au graphique
plt.title("Isotherme a T = 320 K")

# 'plt.grid(True)' affiche une grille 
plt.grid(True)

# 'plt.legend()' affiche la légende 
plt.legend()

# 'plt.tight_layout()' ajuste la disposition du graphique
plt.tight_layout()

# 'plt.show()' affiche le graphique
plt.show()