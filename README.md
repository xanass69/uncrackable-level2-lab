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

## Captures d'écran

### Interface
![Interface](screenshots/erreurmessage.png)

### CodeCheck JADX
![CodeCheck](screenshots/codeCheck.png)

### Native method
![Native](screenshots/codeCheckbarjava.png)

### Ghidra Function
![Ghidra](screenshots/libfoo.png)

### Verification code
![Verify](screenshots/verifycode.png)

### Secret found
![Secret](screenshots/correctsecret.png)