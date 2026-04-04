# Uncrackable Level 2 - Reverse Engineering Lab

## Description

Ce laboratoire documente l'analyse complète de l'application Android **Uncrackable Level 2**, un challenge de reverse engineering issu de l'OWASP Mobile Security Testing Guide (MSTG). L'objectif était de retrouver le secret caché dans l'application en analysant son code Java et sa bibliothèque native.

**Secret trouvé :** `Thanks for all the fish`

---

## Outils utilisés

- **JADX** - Décompilation du code Java
- **Ghidra** - Reverse engineering du code natif
- **ADB** - Installation et test de l'application
- **Python** - Décodage du secret

---

## Méthodologie

### Analyse de l'interface

L'application affiche une interface simple avec un champ de texte et un bouton "VERIFY". Toute saisie incorrecte affiche un message d'erreur, confirmant qu'une logique de comparaison existe.

## Captures d'écran

### 1. Interface de l'application (message d'erreur)
<img width="200" height="383" alt="erreurmessage" src="https://github.com/user-attachments/assets/4fa94e66-2f39-4f91-8faf-c58c4ffbd894" />

### 2. CodeCheck dans JADX
<img width="533" height="227" alt="codeCheck" src="https://github.com/user-attachments/assets/a469ca17-c271-4c86-99de-eff72f15430f" />

### 3. Méthode native bar() dans JADX
<img width="902" height="206" alt="codeCheckbarjava" src="https://github.com/user-attachments/assets/275dcc95-3aa3-4e74-9373-2f9b09664cf2" />

### 4. Fonction native dans Ghidra
<img width="670" height="472" alt="libfoo" src="https://github.com/user-attachments/assets/f0185138-1115-4625-a3f7-33c2af073146" />

### 5. Code de vérification
<img width="617" height="218" alt="verifycode" src="https://github.com/user-attachments/assets/187556e5-8e3d-45d6-add8-f224b4898254" />

### 6. Secret trouvé
<img width="186" height="371" alt="correctsecret" src="https://github.com/user-attachments/assets/99a3da5f-11f3-41e8-8491-83eb6c13a739" />

### Décompilation avec JADX

L'analyse du code Java décompilé révèle que `MainActivity` récupère la saisie utilisateur et l'envoie à la classe `CodeCheck` :

```java
// MainActivity.java
public void verify(View view) {
    String input = this.editText.getText().toString();
    if (this.m.a(input)) {
        Toast.makeText(this, "Success!", 1).show();
    } else {
        Toast.makeText(this, "Something's wrong...", 1).show();
    }
}
