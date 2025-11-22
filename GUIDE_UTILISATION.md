# Guide Rapide d'Utilisation

## 🚀 Démarrage Rapide

### 1️⃣ Ouvrir le Simulateur
- Double-cliquez sur `scheduling-simulator-professional.html`
- Ou ouvrez-le dans votre navigateur préféré

### 2️⃣ Générer des Tâches
```
┌─────────────────────────────────┐
│ Nombre de tâches : [4] ▼       │
│                                  │
│ ☐ Deadlines contraintes (D < T) │
│ ☐ Forcer U > 1                  │
│ ☐ Forcer U < 1                  │
│                                  │
│ [Générer les tâches]            │
└─────────────────────────────────┘
```

### 3️⃣ Lancer la Simulation
- Cliquez sur **"Démarrer la simulation"**
- Les 3 algorithmes s'exécutent simultanément

### 4️⃣ Observer les Résultats
- **Barres de couleur** = exécution des tâches
- **⊗ orange** = préemption
- **Rouge** = deadline ratée
- **⚡ bleu** = tâche en cours d'exécution

---

## 📊 Interpréter les Bornes d'Ordonnançabilité

### Scénario 1 : Tous Verts ✅
```
Fixed Priority (RM):   ✓ Ordonnançable
SJF Préemptif:         ✓ Ordonnançable  
EDF:                   ✓ Ordonnançable
```
**Signification :** Configuration idéale, tous les algorithmes devraient réussir.

---

### Scénario 2 : Fixed Priority Rouge ⚠️
```
Fixed Priority (RM):   ✗ Non garanti (U > 75.7%)
SJF Préemptif:         ✓ Ordonnançable
EDF:                   ✓ Ordonnançable
```
**Signification :** 
- Fixed Priority **peut** rater des deadlines
- Mais ce n'est **pas garanti** qu'il rate
- C'est juste qu'on ne peut **pas garantir** qu'il réussisse
- SJF et EDF devraient réussir

---

### Scénario 3 : EDF Rouge avec D < T 🔴
```
Fixed Priority (RM):   ✗ Non garanti
SJF Préemptif:         ✓ Ordonnançable
EDF:                   ✗ Non ordonnançable
                       Densité (Δ): 159.0%
                       ⚠️ D < T : Δ > 1
```
**Signification :**
- **Deadlines contraintes** activées (D < T)
- Même si U < 100%, **Δ > 100%**
- EDF **ratera forcément** des deadlines
- C'est **mathématiquement impossible** de tout ordonnancer

**Solution :** Décochez "D < T" pour avoir D = T

---

### Scénario 4 : Tous Rouges (Surcharge) ❌
```
Utilisation: 125.4%

Fixed Priority (RM):   ✗ Non garanti
SJF Préemptif:         ✗ Non ordonnançable
EDF:                   ✗ Non ordonnançable
```
**Signification :**
- **Surcharge** du système (U > 100%)
- **Impossible** d'ordonnancer
- Le CPU n'a **pas assez de temps**
- Tous les algorithmes **rateront** des deadlines

---

## 🎯 Cas d'Utilisation Typiques

### 🧪 Test 1 : Voir la Préemption
**Objectif :** Observer beaucoup de préemptions (symboles ⊗)

**Configuration :**
1. Nombre de tâches : 4-5
2. ☐ Deadlines contraintes (D < T)
3. ☐ Forcer U > 1
4. ☑ Forcer U < 1

**Résultat attendu :**
- Fixed Priority : 0 symboles ⊗ (non préemptif)
- SJF : 20-30 symboles ⊗ (très préemptif)
- EDF : 10-20 symboles ⊗ (préemption stratégique)

---

### 🧪 Test 2 : Système Critique (D < T)
**Objectif :** Voir l'impact des deadlines contraintes

**Configuration :**
1. Nombre de tâches : 4
2. ☑ Deadlines contraintes (D < T)
3. ☐ Forcer U > 1
4. ☐ Forcer U < 1

**Résultat possible :**
- U = 97.9% < 100% ✓
- Δ = 159% > 100% ✗
- EDF rate des deadlines malgré U < 1

**Explication :**
- Avec D < T, le test change
- Ce n'est plus U ≤ 1, mais Δ ≤ 1
- C'est plus restrictif !

---

### 🧪 Test 3 : Surcharge Volontaire
**Objectif :** Voir l'effet domino sur EDF

**Configuration :**
1. Nombre de tâches : 4
2. ☐ Deadlines contraintes (D < T)
3. ☑ Forcer U > 1
4. ☐ Forcer U < 1

**Résultat attendu :**
- U > 100%
- Toutes les bornes rouges
- Beaucoup de barres rouges (deadlines ratées)
- EDF montre "l'effet domino" : une fois qu'une deadline est ratée, les suivantes le sont aussi

---

### 🧪 Test 4 : Comparaison Optimale
**Objectif :** Comparer les algorithmes dans des conditions idéales

**Configuration :**
1. Nombre de tâches : 4
2. ☐ Deadlines contraintes (D < T)
3. ☐ Forcer U > 1
4. ☑ Forcer U < 1

**Résultat attendu :**
- U ≈ 70-90%
- Toutes les bornes vertes
- 0 deadline ratée
- Différences visibles :
  - Fixed Priority : Exécution par priorité stricte
  - SJF : Beaucoup de changements (tâches courtes d'abord)
  - EDF : Exécution par deadline (optimal)

---

## 🎨 Comprendre la Légende Visuelle

### Couleurs des Tâches
- 🔵 **Bleu** = τ1
- 🟢 **Vert** = τ2
- 🟣 **Violet** = τ3
- 🩵 **Cyan** = τ4
- 🩷 **Rose** = τ5

### Symboles
- **▲** (noir, vers le haut) = Arrivée du job (période)
- **▼** (rouge, vers le bas) = Deadline
- **⊗** (orange) = Préemption (tâche interrompue)
- **⚡** (bleu) = Tâche en cours d'exécution
- **✕** (rouge) = Deadline ratée
- **|** (rouge vertical) = Temps actuel

### Barres d'Exécution
- **Couleur normale** = Exécution avant la deadline ✅
- **Rouge** = Exécution après la deadline ❌
- **Bordure pointillée orange** = Segment préempté
- **Halo bleu** = En cours d'exécution

---

## 🔧 Contrôles de la Simulation

### Boutons Principaux
- **Générer les tâches** : Crée un nouveau jeu de tâches aléatoires
- **Démarrer la simulation** : Lance l'exécution
- **Pause** : Met en pause (apparaît après démarrage)
- **Reprendre** : Continue après pause
- **Réinitialiser** : Remet à zéro

### Vitesse de Simulation
- **0.05 unités** de temps par step
- **50ms** entre chaque step
- **≈ 20 steps/seconde**

---

## 📈 Statistiques Affichées

Pour chaque algorithme, en bas du diagramme :

```
Jobs terminés : 11/17
En attente : 2
Deadlines ratées : 1
```

**Signification :**
- **11/17** = 11 jobs complétés sur 17 générés
- **En attente : 2** = 2 jobs arrivés mais pas encore commencés
- **Deadlines ratées : 1** = 1 job a dépassé sa deadline

---

## 💡 Astuces

### ✅ Conseil 1 : Commencer Simple
- Décochez toutes les options
- Cochez "Forcer U < 1"
- Générez 3 tâches
- Tout devrait être vert et sans erreur

### ✅ Conseil 2 : Observer les Différences
- Lancez la simulation
- Cliquez sur "Pause" à mi-parcours
- Comparez les 3 diagrammes :
  - Lequel a le plus de ⊗ ?
  - Lequel a le moins de rouge ?
  - Lequel utilise le mieux le CPU ?

### ✅ Conseil 3 : Tester les Limites
- Cochez "D < T" ET "Forcer U < 1"
- Régénérez plusieurs fois
- Observez quand Δ > 100%
- Voyez EDF échouer malgré U < 100%

### ✅ Conseil 4 : Vérifier la Cohérence
- Si une borne dit "✓ Ordonnançable"
- Mais que vous voyez du rouge
- C'est qu'il y a un bug !
- (Sauf pour Fixed Priority où "Non garanti" ≠ "Ratera forcément")

---

## 🐛 Problèmes Courants

### ❓ "EDF rate des deadlines avec U = 85%"
**Réponse :** Vérifiez si "D < T" est coché. Si oui, regardez Δ (densité). Si Δ > 100%, c'est normal.

### ❓ "Fixed Priority dit 'Non garanti' mais réussit"
**Réponse :** C'est normal ! La borne RM est un test **suffisant** mais pas **nécessaire**. Si U > borne RM, on ne peut pas garantir, mais ça peut quand même marcher.

### ❓ "Je ne vois pas de préemptions (⊗)"
**Réponse :** 
1. Vérifiez que vous regardez SJF ou EDF (pas Fixed Priority)
2. Régénérez les tâches (aléatoire)
3. Assurez-vous d'avoir au moins 4 tâches

### ❓ "Tout est rouge !"
**Réponse :** U > 100%. Décochez "Forcer U > 1" et régénérez.

---

## 📞 Support

**En cas de problème :**
1. Ouvrez la console JavaScript (F12)
2. Vérifiez les erreurs
3. Rafraîchissez la page (F5)
4. Consultez `CORRECTIONS_ET_AMELIORATIONS.md`

---

**Bon ordonnancement ! 🚀**
