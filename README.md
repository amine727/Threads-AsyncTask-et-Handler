# LAB 8 — Threads, AsyncTask et Handler


##  Objectif du laboratoire

Ce laboratoire a pour objectif de comprendre la différence entre **UI Thread** et **Worker Thread** dans Android, et d'apprendre à exécuter des tâches longues sans bloquer l'interface utilisateur.

Concepts étudiés :

* UI Thread vs Worker Thread
* Création d’un **Thread** avec `Runnable`
* Mise à jour de l’interface avec `runOnUiThread()`, `Handler` ou `View.post()`
* Utilisation de **AsyncTask** avec progression
* Éviter les erreurs classiques (UI bloquée, mise à jour de l’UI hors thread principal)

#  Fonctionnalités de l'application

L'application contient :

* Un **TextView** pour afficher le statut
* Une **ProgressBar** horizontale
* Un **ImageView**
* Trois boutons :

1. **Charger image (Thread)**
2. **Calcul lourd (AsyncTask)**
3. **Afficher Toast**

---

#  Fonctionnement

## 1️⃣ Charger image (Thread)

Ce bouton lance un **Worker Thread** qui simule un chargement d’image.

Le thread effectue un traitement en arrière-plan puis met à jour l’interface avec :

```java
runOnUiThread()
```

Cela permet d’éviter l’erreur Android :

```
Only the original thread that created a view hierarchy can touch its views
```

---

## 2️⃣ Calcul lourd (AsyncTask)

Le bouton lance une **AsyncTask** qui simule un calcul long.

Les étapes :

* `onPreExecute()` → initialise la ProgressBar
* `doInBackground()` → exécute le calcul en arrière-plan
* `publishProgress()` → met à jour la progression
* `onPostExecute()` → affiche le résultat final

La **ProgressBar progresse de 0 à 100**.

---

## 3️⃣ Afficher Toast

Ce bouton affiche un **Toast** :

```java
Toast.makeText(this,"UI réactive",Toast.LENGTH_SHORT).show();
```

Le Toast doit apparaître **même pendant un traitement**, ce qui prouve que **l’interface utilisateur reste réactive**.


#  Tests réalisés

### Test 1 — Chargement avec Thread

Cliquer sur :

```
Charger image (Thread)
```

Résultat attendu :

```
Statut : image chargée (Thread)
```

Pendant le chargement, le bouton **Afficher Toast** doit toujours fonctionner.

---

### Test 2 — Calcul avec AsyncTask

Cliquer sur :

```
Calcul lourd (AsyncTask)
```

Résultat attendu :

* La **ProgressBar va de 0 à 100**
* Le statut affiche :

```
Statut : calcul terminé résultat = ...
```

---

# 📸 Résultats de l'application

### Chargement image avec Thread

<img width="456" height="1037" alt="1" src="https://github.com/user-attachments/assets/38fafbff-acd8-45da-9084-b8e6c62a5285" />

---

### Calcul avec AsyncTask

<img width="410" height="1054" alt="2" src="https://github.com/user-attachments/assets/ec425e02-60d2-40e5-9fea-79c6fcbc33ad" />




#  Conclusion

Ce laboratoire montre comment :

* éviter de bloquer l’interface Android
* exécuter des tâches lourdes en arrière-plan
* mettre à jour l’UI correctement

Les **Threads** et **AsyncTask** permettent de garder une **application fluide et réactive**.
