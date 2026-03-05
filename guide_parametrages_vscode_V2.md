# Guide pas-à-pas : Installation et configuration VSCode pour XML/XSLT

## L3 information-documentation

> **⏳ Durée estimée :** 45-60 minutes  
> **🟢 Niveau :** Débutant  
> **Systèmes :** 🪟 Windows / 🍎 Mac

---

## 📋 Vue d'ensemble

À la fin de ce guide, vous aurez :

* ✅ VSCode installé et configuré
* ✅ Java et Saxon opérationnels
* ✅ Les extensions nécessaires
* ✅ Un projet d'exemple fonctionnel
* ✅ Votre première transformation XSLT réussie

---

## Partie 1 : Installation de Visual Studio Code

### Étape 1.1 : Télécharger VSCode

**🪟 Windows :**

1. Ouvrez votre navigateur web
2. Allez sur : `https://code.visualstudio.com/download` [🌐](https://code.visualstudio.com/download)
3. La page détecte automatiquement votre système d'exploitation
4. Cliquez sur le grand bouton bleu **"Download for Windows"**
5. Le fichier `VSCodeUserSetup-x64-1.xx.x.exe` se télécharge

> **💡 Astuce :** Si vous préférez une version portable (sans installation), cliquez sur "Other downloads" et choisissez le fichier `.zip`

**🍎 Mac :**

1. Même site : `https://code.visualstudio.com/download` [🌐](https://code.visualstudio.com/download)
2. Cliquez sur **"Download for Mac"**
3. Le fichier `VSCode-darwin-universal.zip` se télécharge

---

### Étape 1.2 : Installer VSCode

**🪟 Windows :**

1. Double-cliquez sur le fichier téléchargé `VSCodeUserSetup-x64-x.xx.x.exe`
2. Une fenêtre de sécurité Windows peut apparaître : cliquez sur **"Oui"**
3. Acceptez le contrat de licence : cochez "J'accepte..." puis **"Suivant"**
4. Laissez le dossier d'installation par défaut : **"Suivant"**
5. **Important :** À l'écran "Tâches supplémentaires", cochez :
   * ☑️ Ajouter l'action "Ouvrir avec Code" au menu contextuel
   * ☑️ Ajouter à PATH (très important !)
6. Cliquez sur **"Suivant"** puis **"Installer"**
7. Attendez la fin de l'installation (30 secondes environ)
8. Cochez "Lancer Visual Studio Code" puis **"Terminer"**

> **⚠️ Faites attention à :** Bien cocher "Ajouter à PATH" - c'est essentiel pour que VSCode fonctionne correctement

**🍎 Mac :**

1. Ouvrez le fichier `.zip` téléchargé (il se décompresse automatiquement)
2. Glissez l'icône **"Visual Studio Code"** dans le dossier **Applications**
3. Ouvrez le Finder → Applications
4. Double-cliquez sur **"Visual Studio Code"**
5. Une alerte de sécurité apparaît : cliquez sur **"Ouvrir"**

---

### Étape 1.3 : Premier démarrage de VSCode

VSCode s'ouvre. Vous voyez :

1. **À gauche :** Une barre verticale avec 5 icônes (Explorateur, Recherche, Contrôle de code source, Exécuter, Extensions)
2. **Au centre :** Une page d'accueil avec "Get Started" et des raccourcis
3. **En bas :** Une barre bleue (barre d'état)

> **💡 Astuce :** Si l'interface est en anglais et que vous voulez le français, cf. [Partie 2, Étape 2.3]

---

## Partie 2 : Installation des extensions

### Étape 2.1 : Ouvrir le gestionnaire d'extensions

1. Dans la barre latérale gauche, cliquez sur l'icône **Extensions** (4ème icône, elle ressemble à 4 petits carrés)

   * Raccourci clavier : `Ctrl+Shift+X` (Windows) ou `Cmd+Shift+X` (Mac)
2. Un panneau s'ouvre sur la gauche avec :

   * En haut : une barre de recherche "Rechercher des extensions dans..."
   * En dessous : la liste des extensions installées (vide pour l'instant)

> **💡 Astuce :** Vous pouvez aussi taper `Ctrl+Shift+X` directement, c'est plus rapide !

---

### Étape 2.2 : Installer "XML Tools"

1. Dans la barre de recherche des extensions, tapez : `XML Tools`
2. Trouvez **"XML Tools"** avec :

   * Nom : **XML Tools**
   * Auteur : **Josh Johnson**
   * Description : "XML Formatting, XQuery, and XPath Tools for Visual Studio Code"
3. Cliquez sur cette extension
4. Un panneau de détails s'ouvre à droite
5. Cliquez sur le bouton bleu **"Install"** (Installer)
6. Attendez quelques secondes
7. Le bouton devient **"Disable"** (Désactiver) - c'est normal, l'extension est installée !

> **💡 Pourquoi cette extension ?** XML Tools gère tout ce dont vous avez besoin : validation XML, formatage, XPath ET transformations XSLT, le tout avec une configuration ultra-simple !

> **⚠️ Erreur courante :** Si vous ne voyez pas l'extension, vérifiez que vous avez bien tapé "XML Tools" dans la recherche et qu'internet fonctionne

---

### Étape 2.3 : Installer "French Language Pack" (optionnel)

**Si vous voulez VSCode en français :**

1. Dans la barre de recherche des extensions, tapez : `French Language`
2. Trouvez **"French Language Pack for Visual Studio Code"**

   * Auteur : **Microsoft**
   * Logo : Drapeau français
3. Cliquez dessus puis sur **"Install"**
4. Une fois installé, une notification apparaît en bas à droite :

   * **"Would you like to change VS Code's UI language to French and restart?"**
   * Cliquez sur **"Yes"** (ou "Oui")
5. VSCode redémarre automatiquement
6. L'interface est maintenant en français !

> **💡 Astuce :** Vous pouvez changer de langue plus tard via `Ctrl+Shift+P` → "Configure Display Language"

---

### Étape 2.4 : Vérifier les extensions installées

1. Dans le panneau Extensions (toujours ouvert)
2. En haut de la barre de recherche, effacez votre recherche
3. Vous voyez maintenant vos extensions installées :
   * ✅ XML Tools (Josh Johnson)
   * ✅ French Language Pack for Visual Studio Code (si installé)

> **💡 Astuce :** Vous pouvez désactiver temporairement une extension avec le bouton "Désactiver" si besoin

---

## Partie 3 : Installation de Java (Zulu JDK)

### Étape 3.1 : Télécharger Zulu JDK

**🪟 Windows :**

1. Ouvrez votre navigateur
2. Allez sur : `https://www.azul.com/downloads/?package=jdk` [🌐](https://www.azul.com/downloads/?package=jdk)
3. Sur la page, configurez les filtres :

   * **Java Version :** Sélectionnez **Java 17 (LTS)**
   * **Operating System :** Sélectionnez **Windows**
   * **Architecture :** Sélectionnez **x86 64-bit**
   * **Java Package :** Sélectionnez **JDK**
4. Descendez dans la liste des téléchargements
5. Cherchez la ligne avec le format **".zip"** (pas .msi, pas .exe)
6. Cliquez sur le bouton **".zip"** pour télécharger
7. Le fichier `zulu17.xx.xx-ca-jdk17.x.x-win_x64.zip` se télécharge

> **⚠️ Faites attention à :** Bien télécharger le fichier **.zip** (version portable), pas le .msi

**🍎 Mac :**

1. Même site : `https://www.azul.com/downloads/?package=jdk` [🌐](https://www.azul.com/downloads/?package=jdk)
2. Configurez les filtres :

   * **Java Version :** **Java 17 (LTS)**
   * **Operating System :** **macOS**
   * **Architecture :** **ARM 64-bit** (si Mac M1/M2/M3) ou **x86 64-bit** (si Mac Intel)
   * **Java Package :** **JDK**
3. Téléchargez le fichier **.dmg** ou **.zip** selon votre préférence

---

### Étape 3.2 : Installer Java

**🪟 Windows :**

1. Allez dans votre dossier Téléchargements
2. Trouvez le fichier `zulu17.xx.xx-ca-jdk17.x.x-win_x64.zip`
3. **Faites un clic droit** dessus → **"Extraire tout..."**
4. Choisissez un emplacement simple, par exemple :

   * `C:\Outils\jdk17`
   * Ou si vous utilisez un autre disque : `D:\Outils\jdk17`
5. Cliquez sur **"Extraire"**
6. Un dossier se crée avec un sous-dossier `zulu17.xx.xx-ca-jdk17.x.x-win_x64`

> **💡 Astuce :** ⚠️ Notez bien le chemin complet. Vous en aurez besoin plus tard !

**Pour simplifier, renommez le dossier :**

* Avant : `C:\Outils\zulu17.52.17-ca-jdk17.0.12-win_x64`
* Après : `C:\Outils\jdk17`

> **💡 Alternative :** Vous pouvez aussi garder le nom complet (ex: `zulu-jdk17.0.17`) pour suivre précisément la version installée. Dans ce cas, utilisez ce nom exact dans votre `settings.json` :
>
> ```
> "java.home": "C:/Outils/zulu-jdk17.0.17"
> ```

**🍎 Mac :**

1. Si fichier **.dmg** :

   * Double-cliquez dessus
   * Suivez l'assistant d'installation
   * Java s'installe dans `/Library/Java/JavaVirtualMachines/`
2. Si fichier **.zip** :

   * Décompressez-le
   * Placez le dossier dans un endroit accessible, par exemple :
   * `/Users/votrenom/Outils/jdk17`

> **💡 La vérification de Java se fera en Partie 5, une fois le fichier `settings.json` créé — c'est nécessaire pour que le terminal VSCode puisse trouver Java.**

---

## Partie 4 : Installation de Saxon

### Étape 4.1 : Télécharger Saxon

1. Ouvrez votre navigateur
2. `https://www.saxonica.com/download/java.xml` [🌐](https://www.saxonica.com/download/java.xml)
3. Sur la page, cherchez la section **"Saxon-HE"** (Home Edition)
4. Cliquez sur le lien de téléchargement pour la dernière version

   * Par exemple : **"Saxon-HE 12.9"**
5. Vous arrivez sur SourceForge
6. Le téléchargement du fichier **`SaxonHE12-9J.zip`** commence automatiquement
7. Si ce n'est pas le cas, cliquez sur le bouton vert **"Download"**

> **💡 Astuce :** Saxon fonctionne de la même façon sur Windows et Mac (c'est un fichier Java)

---

### Étape 4.2 : Installer Saxon

**🪟 Windows et 🍎 Mac (même procédure) :**

1. Allez dans votre dossier Téléchargements
2. Trouvez le fichier `SaxonHE12-9J.zip`
3. **Décompressez-le** (clic droit → Extraire)
4. Dans le dossier décompressé, vous trouvez plusieurs fichiers
5. **Cherchez le fichier** : `saxon-he-12.9.jar`
6. **Copiez ce fichier** dans un endroit simple :
   * Windows : `C:\Outils\saxon-he-12.9.jar`
   * Mac : `/Users/votrenom/Outils/saxon-he-12.9.jar`

> **💡 Organisation alternative :**
> Vous pouvez aussi créer un sous-dossier pour mieux organiser vos outils :
>
> * 🪟 Windows : `C:\Outils\SaxonHE12-9J\saxon-he-12.9.jar`
> * 🍎 Mac : `/Users/votrenom/Outils/SaxonHE12-9J/saxon-he-12.9.jar`
>
> ⚠️ Dans ce cas, utilisez le chemin complet dans `settings.json` :
>
> ```
> "saxon.jar.path": "C:/Outils/SaxonHE12-9J/saxon-he-12.9.jar"
> ```

> **⚠️ Faites attention à :** Ne prenez QUE le fichier `.jar`, pas tout le dossier. Saxon est un fichier unique !

> **💡 La vérification de Saxon se fera en Partie 5, une fois le fichier `settings.json` créé — c'est nécessaire pour que le terminal VSCode puisse trouver Java et Saxon.**

---

## Partie 5 : Créer votre premier projet

### Étape 5.1 : Créer la structure du projet

1. Sur votre ordinateur, créez un dossier pour vos projets XML :

   * 🪟 Windows : `C:\MesProjets\ProjetXML1`
   * 🍎 Mac : `/Users/votrenom/MesProjets/ProjetXML1`
2. Dans VSCode, cliquez sur **"Fichier"** → **"Ouvrir le dossier..."**
3. Naviguez jusqu'à votre dossier `ProjetXML1`
4. Cliquez sur **"Sélectionner un dossier"**

VSCode affiche maintenant votre projet dans l'explorateur de fichiers (à gauche).

> **💡 Astuce :** Vous pouvez aussi glisser-déposer le dossier directement sur l'icône VSCode

---

### Étape 5.2 : Créer la structure .vscode

1. Dans l'explorateur de fichiers VSCode (à gauche), faites un **clic droit** sur la zone vide
2. Choisissez **"Nouveau dossier"**
3. Tapez exactement : `.vscode` (avec le point au début !)
4. Appuyez sur **Entrée**

> **⚠️ Faites attention à :** Le point au début est OBLIGATOIRE ! C'est `.vscode` pas `vscode`

Un nouveau dossier `.vscode` apparaît dans l'arborescence.

---

### Étape 5.3 : Créer le fichier settings.json

1. **Clic droit** sur le dossier `.vscode`
2. Choisissez **"Nouveau fichier"**
3. Tapez : `settings.json`
4. Appuyez sur **Entrée**

Le fichier s'ouvre dans l'éditeur (au centre).

5. **Copiez-collez** ce contenu COMPLET (en ADAPTANT les chemins selon votre installation) :

**🪟 Pour Windows :**

```
{
  "java.home": "C:/Outils/jdk17",
  "saxon.jar.path": "C:/Outils/saxon-he-12.9.jar"
}
```

**🍎 Pour Mac :**

```
{
  "java.home": "/Users/votrenom/Outils/jdk17",
  "saxon.jar.path": "/Users/votrenom/Outils/saxon-he-12.9.jar"
}
```

6. **Sauvegardez** : `Ctrl+S` (Windows) ou `Cmd+S` (Mac)

> **⚠️ TRÈS IMPORTANT :**
>
> * Remplacez `votrenom` par votre vrai nom d'utilisateur (Mac uniquement)
> * Vérifiez que les chemins correspondent à VOS dossiers
> * Pour Windows, utilisez des `/` (slashes) pas des `\` (backslashes)
> * Vérifiez les guillemets : `"` (pas `'`)
> * Le chemin `java.home` pointe vers le **dossier** JDK (pas vers java.exe)

> **💡 Configuration ultra-simple !** Seulement 2 lignes suffisent avec l'extension XML Tools. C'est tout ce dont vous avez besoin pour faire fonctionner les transformations XSLT.

---

### ⚠️ Configuration spéciale pour disques externes/portables avec 🪟 WINDOWS

**Si votre projet ou VSCode est sur un disque externe (D:, E:, G:, clé USB, SSD portable) :**

Il pourrait (ou pas !) y avoir des problèmes de permissions avec PowerShell. Ajoutez cette configuration au début de votre `settings.json` :

**🪟 Pour Windows avec disque externe :**

```
{
  "terminal.integrated.profiles.windows": {
    "PowerShell": {
      "source": "PowerShell",
      "icon": "terminal-powershell",
      "_comment": "chemin path à adapter ci dessous",
      "path": "C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe"
    }
  },
  "terminal.integrated.defaultProfile.windows": "PowerShell",
  
  "java.home": "G:/Outils/jdk17",
  "saxon.jar.path": "G:/Outils/saxon-he-12.9.jar"
}
```

> **💡 Astuce :** Remplacez `G:/` par la lettre de VOTRE disque (D:, E:, F:, etc.)

**Et lancez VSCode en mode administrateur :**

1. Clic droit sur le raccourci VSCode → **Propriétés**
2. Onglet **"Compatibilité"**
3. Cochez **"Exécuter ce programme en tant qu'administrateur"**
4. Cliquez sur **OK**

> **⚠️ Pourquoi ?** Les disques externes ont parfois des restrictions de permissions. Cette configuration + le mode administrateur résolvent ces problèmes.

---

### Étape 5.4 : Vérifier Java et Saxon

> **⚠️ Cette étape nécessite que le fichier `settings.json` soit créé et sauvegardé (étape 5.3).**

**Ouvrez un terminal dans VSCode :**

* Menu **"Terminal"** → **"Nouveau terminal"**
* Ou raccourci : `Ctrl+ù` (ou `` Ctrl+` ``)

Un panneau s'ouvre en bas de VSCode.

#### Vérifier Java

**🪟 Windows :** tapez la commande suivante (en adaptant le chemin) :

```
C:\Outils\jdk17\bin\java.exe -version
```

**🍎 Mac :** tapez :

```
/Users/votrenom/Outils/jdk17/bin/java -version
```

Ou si installation via .dmg :

```
/Library/Java/JavaVirtualMachines/zulu-17.jdk/Contents/Home/bin/java -version
```

Appuyez sur **Entrée**. Vous devez voir s'afficher :

```
openjdk version "17.0.xx"
OpenJDK Runtime Environment Zulu...
```

> **⚠️ Erreur courante :** Si vous voyez "java n'est pas reconnu...", vérifiez le chemin dans `settings.json`. Utilisez l'explorateur de fichiers pour confirmer que `java.exe` existe bien dans le dossier `bin`.

#### Vérifier Saxon

**🪟 Windows :** tapez :

```
C:\Outils\jdk17\bin\java.exe -jar C:\Outils\saxon-he-12.9.jar
```

**🍎 Mac :** tapez :

```
/Users/votrenom/Outils/jdk17/bin/java -jar /Users/votrenom/Outils/saxon-he-12.9.jar
```

Appuyez sur **Entrée**. Vous devez voir :

```
Saxon-HE 12.9 from Saxonica
Usage: see http://www.saxonica.com/documentation/...
```

> **✅ Si vous voyez ces deux messages, Java et Saxon fonctionnent correctement !**

> **⚠️ Erreur courante :** Si vous voyez "Error: Unable to access jarfile", vérifiez le chemin du fichier `.jar` dans `settings.json`.

> **💡 Astuce :** Si tout fonctionne, notez les chemins exacts quelque part — vous en aurez besoin si vous recréez le projet sur un autre ordinateur.

---

### Étape 5.5 : Créer le fichier tasks.json

1. **Clic droit** sur le dossier `.vscode`
2. **"Nouveau fichier"**
3. Tapez : `tasks.json`
4. Appuyez sur **Entrée**

Le fichier s'ouvre.

5. **Copiez-collez** ce contenu COMPLET :

```
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Transformer XML vers HTML",
      "type": "shell",
      "command": "${config:java.home}/bin/java",
      "args": [
        "-jar",
        "${config:saxon.jar.path}",
        "-s:${file}",
        "-xsl:${input:xslFile}",
        "-o:${fileDirname}/${fileBasenameNoExtension}_resultat.html"
      ],
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "presentation": {
        "reveal": "always",
        "panel": "new"
      },
      "problemMatcher": []
    }
  ],
  "inputs": [
    {
      "id": "xslFile",
      "type": "promptString",
      "description": "Nom du fichier XSLT (ex: catalogue.xsl)",
      "default": "${fileBasenameNoExtension}.xsl"
    }
  ]
}
```

6. **Sauvegardez** : `Ctrl+S` ou `Cmd+S`

> **💡 Ce que fait ce fichier :** Il configure une tâche qui vous permettra de transformer vos fichiers XML en HTML d'un simple raccourci clavier !

> **🔍 Notez les différences :**
>
> * La commande utilise `${config:java.home}/bin/java` (qui récupère le chemin depuis settings.json)
> * Les arguments utilisent `${config:saxon.jar.path}` (pareil)
> * C'est pour ça que la configuration est si simple !

---

## Partie 6 : Créer votre premier document XML

### Étape 6.1 : Créer le fichier catalogue.xml

1. Dans l'explorateur VSCode (à gauche), **clic droit** sur la racine du projet (ProjetXML1)
2. **"Nouveau fichier"**
3. Tapez : `catalogue.xml`
4. Appuyez sur **Entrée**

Le fichier s'ouvre dans l'éditeur.

---

### Étape 6.2 : Écrire le code XML

**Copiez-collez** ce contenu :

```
<?xml version="1.0" encoding="UTF-8"?>
<catalogue>
    <livre id="liv001">
        <titre>Le Petit Prince</titre>
        <auteur>Antoine de Saint-Exupéry</auteur>
        <annee>1943</annee>
        <genre>Conte philosophique</genre>
        <disponible>oui</disponible>
    </livre>
    
    <livre id="liv002">
        <titre>1984</titre>
        <auteur>George Orwell</auteur>
        <annee>1949</annee>
        <genre>Science-fiction dystopique</genre>
        <disponible>non</disponible>
    </livre>
    
    <livre id="liv003">
        <titre>L'Étranger</titre>
        <auteur>Albert Camus</auteur>
        <annee>1942</annee>
        <genre>Roman philosophique</genre>
        <disponible>oui</disponible>
    </livre>
</catalogue>
```

**Sauvegardez** : `Ctrl+S` ou `Cmd+S`

---

### Étape 6.3 : Vérifier que le XML est valide

1. Regardez en bas à droite de la fenêtre VSCode
2. Vous devez voir un petit symbole :

   * ✅ **Coche verte** = XML valide
   * ❌ **Croix rouge** = Erreur dans le XML
3. Si vous voyez des **vaguelettes rouges** sous certaines lignes :

   * C'est une erreur de syntaxe
   * Passez la souris dessus pour voir le message d'erreur
   * Corrigez l'erreur

> **⚠️ Erreur courante :** Oublier de fermer une balise. Vérifiez que chaque `<livre>` a son `</livre>`

---

## Partie 7 : Créer votre première feuille XSLT

> Uniquement pour tester que VSCode est opérationnel à ce stade

### Étape 7.1 : Créer le fichier catalogue.xsl

1. **Clic droit** sur la racine du projet
2. **"Nouveau fichier"**
3. Tapez : `catalogue.xsl`
4. Appuyez sur **Entrée**

> **💡 Astuce :** On donne le même nom (catalogue) pour faciliter le repérage, mais ce n'est pas obligatoire

---

### Étape 7.2 : Écrire le code XSLT

**Copiez-collez** ce contenu :

```
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    
    <xsl:template match="/">
        <html>
            <head>
                <meta charset="UTF-8"/>
                <title>Mon catalogue de livres</title>
                <style>
                    body {
                        font-family: Arial, sans-serif;
                        max-width: 800px;
                        margin: 40px auto;
                        padding: 20px;
                        background-color: #f5f5f5;
                    }
                    h1 {
                        color: #2c3e50;
                        border-bottom: 3px solid #3498db;
                        padding-bottom: 10px;
                    }
                    .livre {
                        background-color: white;
                        border-left: 4px solid #3498db;
                        padding: 20px;
                        margin: 20px 0;
                        box-shadow: 0 2px 5px rgba(0,0,0,0.1);
                    }
                    .livre h2 {
                        color: #2c3e50;
                        margin-top: 0;
                    }
                    .info {
                        margin: 8px 0;
                        color: #555;
                    }
                    .label {
                        font-weight: bold;
                        color: #2c3e50;
                    }
                    .disponible {
                        color: #27ae60;
                        font-weight: bold;
                    }
                    .indisponible {
                        color: #e74c3c;
                        font-weight: bold;
                    }
                </style>
            </head>
            <body>
                <h1>📚 Notre catalogue de livres</h1>
                <p>Nombre de livres : <xsl:value-of select="count(catalogue/livre)"/></p>
                
                <xsl:apply-templates select="catalogue/livre"/>
            </body>
        </html>
    </xsl:template>
    
    <xsl:template match="livre">
        <div class="livre">
            <h2><xsl:value-of select="titre"/></h2>
            
            <div class="info">
                <span class="label">Auteur :</span>
                <xsl:value-of select="auteur"/>
            </div>
            
            <div class="info">
                <span class="label">Année :</span>
                <xsl:value-of select="annee"/>
            </div>
            
            <div class="info">
                <span class="label">Genre :</span>
                <xsl:value-of select="genre"/>
            </div>
            
            <div class="info">
                <span class="label">Disponibilité :</span>
                <xsl:choose>
                    <xsl:when test="disponible = 'oui'">
                        <span class="disponible">✓ Disponible</span>
                    </xsl:when>
                    <xsl:otherwise>
                        <span class="indisponible">✗ Indisponible</span>
                    </xsl:otherwise>
                </xsl:choose>
            </div>
        </div>
    </xsl:template>
    
</xsl:stylesheet>
```

**Sauvegardez** : `Ctrl+S` ou `Cmd+S`

---

## Partie 8 : Lancer votre première transformation ! 🚀

### Étape 8.1 : Préparer la transformation

1. Dans l'explorateur VSCode (à gauche), **cliquez sur `catalogue.xml`** pour l'ouvrir
2. Assurez-vous que vous êtes bien dans l'onglet `catalogue.xml` (en haut de l'éditeur)

> **⚠️ Faites attention à :** Vous devez avoir le fichier XML actif, pas le XSL !

---

### Étape 8.2 : Lancer la tâche de transformation

1. Appuyez sur `Ctrl+Shift+B` (Windows) ou `Cmd+Shift+B` (Mac)
2. Une petite fenêtre apparaît en haut de l'écran avec :

   * "Nom du fichier XSLT (ex: catalogue.xsl)"
3. Tapez : `catalogue.xsl`
4. Appuyez sur **Entrée**

---

### Étape 8.3 : Observer l'exécution

1. Un panneau s'ouvre en bas de VSCode (Terminal)
2. Vous voyez des lignes de texte défiler :

```
> Executing task: C:/Outils/jdk17/bin/java.exe -jar...
```

3. À la fin, vous devez voir :

```
Terminal will be reused by tasks, press any key to close it.
```

> **✅ Si vous voyez ce message, la transformation a réussi !**

> **⚠️ Erreur courante :**
>
> * Si vous voyez "java n'est pas reconnu..." → Vérifiez votre settings.json
> * Si vous voyez "Error on line X..." → Erreur dans votre XML ou XSLT
> * Si rien ne se passe → Vérifiez que vous avez bien sauvegardé tous vos fichiers

---

### Étape 8.4 : Voir le résultat

1. Dans l'explorateur VSCode (à gauche), vous voyez maintenant un nouveau fichier :

   * `catalogue_resultat.html`
2. **Clic droit** sur ce fichier
3. Choisissez **"Révéler dans l'Explorateur de fichiers"** (Windows) ou **"Reveal in Finder"** (Mac)
4. L'explorateur de fichiers s'ouvre sur votre fichier HTML
5. **Double-cliquez** sur `catalogue_resultat.html`
6. Le fichier s'ouvre dans votre navigateur par défaut

**Vous devriez voir :**

* Un titre "📚 Notre catalogue de livres"
* "Nombre de livres : 3"
* Les 3 livres affichés avec un joli style
* Les disponibilités en vert ou rouge

> **🎉 BRAVO ! Vous avez réussi votre première transformation XSLT !**

---

## Partie 9 : Tester XPath

### Étape 9.1 : Ouvrir l'évaluateur XPath

1. Ouvrez le fichier `catalogue.xml` dans VSCode
2. Appuyez sur `Ctrl+Shift+P` (Windows) ou `Cmd+Shift+P` (Mac)
3. Dans la boîte qui apparaît en haut, tapez : `xpath`
4. Choisissez **"XPath: Evaluate XPath"** dans la liste
5. Une nouvelle boîte apparaît : **"Enter XPath expression"**

---

### Étape 9.2 : Tester des expressions XPath

**Test 1 : Sélectionner tous les titres**

1. Dans la boîte "Enter XPath expression", tapez :

   ```
   /catalogue/livre/titre
   ```
2. Appuyez sur **Entrée**
3. Dans votre fichier XML, les 3 titres de livres sont maintenant **surlignés en jaune**
4. Un panneau s'ouvre en bas avec les résultats :

   ```
   Le Petit Prince
   1984
   L'Étranger
   ```

> **💡 Astuce :** C'est un moyen rapide de vérifier que votre XPath sélectionne bien ce que vous voulez !

---

**Test 2 : Sélectionner les livres disponibles**

1. Appuyez à nouveau sur `Ctrl+Shift+P` → "XPath: Evaluate XPath"
2. Tapez :

   ```
   /catalogue/livre[disponible='oui']/titre
   ```
3. Appuyez sur **Entrée**
4. Seuls 2 titres sont surlignés : "Le Petit Prince" et "L'Étranger"

> **💡 Ce que fait cette expression :** Elle sélectionne les titres des livres qui ont `<disponible>oui</disponible>`

---

**Test 3 : Compter les livres**

1. `Ctrl+Shift+P` → "XPath: Evaluate XPath"
2. Tapez :

   ```
   count(/catalogue/livre)
   ```
3. Résultat dans le panneau du bas :

   ```
   3
   ```

---

**Test 4 : Livres publiés avant 1945**

1. Nouvelle expression XPath :

   ```
   /catalogue/livre[annee < 1945]/titre
   ```
2. Résultats : "Le Petit Prince" et "L'Étranger"

---

## Partie 10 : Dépannage et erreurs courantes

### Problème 1 : "java n'est pas reconnu..."

**Symptôme :** Quand vous lancez la transformation, vous voyez :

```
'java' n'est pas reconnu en tant que commande interne...
```

**Solutions :**

1. **Vérifiez le chemin dans settings.json :**

   * Ouvrez `.vscode/settings.json`
   * Vérifiez que le chemin vers `java.exe` est correct
   * Testez le chemin dans l'explorateur Windows
2. **Utilisez le chemin absolu complet :**

   * 🪟 Windows : `C:/Outils/jdk17/bin/java.exe`
   * 🍎 Mac : `/Users/votrenom/Outils/jdk17/bin/java`
3. **Vérifiez les slashes :**

   * ✅ Correct : `C:/Outils/jdk17/bin/java.exe`
   * ❌ Incorrect : `C:\Outils\jdk17\bin\java.exe`

---

### Problème 2 : "Unable to access jarfile..."

**Symptôme :**

```
Error: Unable to access jarfile C:/Outils/saxon-he-12.9.jar
```

**Solutions :**

1. Vérifiez que le fichier `.jar` existe bien :

   * Ouvrez l'explorateur Windows
   * Allez dans `C:\Outils`
   * Vous devez voir le fichier `saxon-he-12.9.jar`
2. Vérifiez le chemin dans `settings.json` :

   * Le nom du fichier doit correspondre exactement
   * `saxon-he-12.9.jar` (pas `saxon-he-12-9.jar`)
3. Vérifiez les guillemets :

   * ✅ `"saxon.jar.path": "C:/Outils/saxon-he-12.9.jar"`
   * ❌ `'saxon.jar.path': 'C:/Outils/saxon-he-12.9.jar'`

---

### Problème 3 : Erreur de syntaxe XML

**Symptôme :** Des vaguelettes rouges apparaissent sous certaines lignes

**Solutions :**

1. **Balise non fermée :**

   * ❌ `<titre>Le Petit Prince`
   * ✅ `<titre>Le Petit Prince</titre>`
2. **Mauvaise imbrication :**

   * ❌ `<livre><titre>...</livre></titre>`
   * ✅ `<livre><titre>...</titre></livre>`
3. **Attribut sans guillemets :**

   * ❌ `<livre id=liv001>`
   * ✅ `<livre id="liv001">`
4. **Caractères spéciaux non échappés :**

   * ❌ `<titre>Romeo & Juliet</titre>`
   * ✅ `<titre>Romeo &amp; Juliet</titre>`

> **⚠️ Faites attention à :** Les 5 entités XML à échapper : `&` → `&amp;` | `<` → `&lt;` | `>` → `&gt;` | `"` → `&quot;` | `'` → `&apos;`

---

### Problème 4 : La transformation ne produit rien

**Symptôme :** La transformation se lance mais aucun fichier HTML n'est créé

**Solutions :**

1. Vérifiez le terminal :

   * Regardez les messages d'erreur dans le panneau Terminal en bas
   * Cherchez des lignes commençant par "Error"
2. Vérifiez votre XSLT :

   * Le namespace doit être : `xmlns:xsl="http://www.w3.org/1999/XSL/Transform"`
   * Vérifiez que vous avez bien `<xsl:template match="/">`
3. Vérifiez que le fichier XML est sauvegardé :

   * Un point blanc à côté du nom du fichier = non sauvegardé
   * Sauvegardez avec `Ctrl+S`
4. Vérifiez les permissions du dossier :

   * VSCode doit pouvoir écrire dans le dossier du projet

---

### Problème 5 : L'évaluateur XPath ne trouve rien

**Symptôme :** Quand vous testez une expression XPath, rien n'est surligné

**Solutions :**

1. Vérifiez que vous êtes dans le bon fichier :

   * Vous devez être dans le fichier XML, pas le XSL
2. Vérifiez la syntaxe XPath :

   * Sensible à la casse : `livre` ≠ `Livre`
   * Commence par `/` pour un chemin absolu
   * Utilisez `//` pour chercher partout : `//titre`
3. Testez une expression simple d'abord :

   * Essayez : `/catalogue`
   * Puis : `/catalogue/livre`
   * Puis ajoutez vos filtres progressivement

---

### Problème 6 : Les accents ne s'affichent pas correctement

**Symptôme :** À la place de "é" vous voyez "Ã©"

**Solutions :**

1. Vérifiez l'encodage du fichier XML :

   * En bas à droite de VSCode, vous voyez l'encodage
   * Cliquez dessus → "Save with Encoding" → "UTF-8"
2. Vérifiez la première ligne du XML :

   * ✅ `<?xml version="1.0" encoding="UTF-8"?>`
3. Vérifiez la balise `<meta>` dans le HTML généré :

   * ✅ `<meta charset="UTF-8"/>`

---

### Problème 7 : Erreur "Static error in XPath expression"

**Symptôme :** Erreur lors de la transformation avec message sur XPath

**Solutions :**

1. Vérifiez la syntaxe de vos expressions XPath dans le XSLT :

   * Les guillemets simples dans les attributs : `select="livre[@id='liv001']"`
   * Pas de guillemets doubles imbriqués
2. Vérifiez les fonctions utilisées :

   * `count()`, `sum()`, `min()`, `max()` sont disponibles
   * Certaines fonctions avancées nécessitent XSLT 2.0 ou 3.0
3. Vérifiez la version XSLT :

   * XSLT 2.0 : `<xsl:stylesheet version="2.0">`
   * Si vous utilisez des fonctions XSLT 2.0+, vérifiez la version

---

### Problème 8 : "Échec du lancement du processus de terminal"

**Symptôme :** 🪟 Windows uniquement

```
Échec du lancement du processus de terminal : A native exception occurred during launch (Cannot create process, error code: 740)
```

**Cause :** Ce problème survient principalement quand VSCode ou votre projet est sur un **disque externe** (D:, E:, G:, clé USB, SSD portable).

**Solutions :**

1. **Lancer VSCode en administrateur (solution immédiate) :**

   * Fermez VSCode
   * Clic droit sur l'icône VSCode → "Exécuter en tant qu'administrateur"
   * Rouvrez votre projet
2. **Configurer le lancement automatique en admin (recommandé) :**

   * Clic droit sur le raccourci VSCode → Propriétés
   * Onglet "Compatibilité"
   * Cochez "Exécuter ce programme en tant qu'administrateur"
   * OK
   * VSCode se lancera toujours en admin
3. **Vérifier la configuration PowerShell :**

   * Ouvrez `.vscode/settings.json`
   * Vérifiez que vous avez bien la configuration PowerShell (voir Étape 5.3 - Configuration spéciale pour disques externes)
4. **Alternative - Utiliser Command Prompt :**
   Si PowerShell pose toujours problème, dans `settings.json` :

```
   {
     "terminal.integrated.defaultProfile.windows": "Command Prompt",
     
     "java.home": "G:/Outils/jdk17",
     "saxon.jar.path": "G:/Outils/saxon-he-12.9.jar"
   }
```

> **💡 Astuce :** Si vous travaillez toujours avec un SSD portable, configurez définitivement le mode administrateur. C'est la solution la plus stable.

---

## Annexes

### Annexe A : Raccourcis clavier VSCode utiles

**Édition :**

* `Ctrl+S` / `Cmd+S` : Sauvegarder
* `Ctrl+Z` / `Cmd+Z` : Annuler
* `Ctrl+Shift+Z` / `Cmd+Shift+Z` : Rétablir
* `Ctrl+C` / `Cmd+C` : Copier
* `Ctrl+V` / `Cmd+V` : Coller
* `Ctrl+X` / `Cmd+X` : Couper
* `Ctrl+F` / `Cmd+F` : Rechercher
* `Ctrl+H` / `Cmd+H` : Remplacer
* `Alt+Shift+F` : Formater le document

**Navigation :**

* `Ctrl+P` / `Cmd+P` : Ouvrir rapidement un fichier
* `Ctrl+Shift+E` / `Cmd+Shift+E` : Explorer de fichiers
* `Ctrl+B` / `Cmd+B` : Masquer/afficher la barre latérale
* `Ctrl+ù` / `` Cmd+` `` : Ouvrir/fermer le terminal
* `Ctrl+Tab` : Naviguer entre les fichiers ouverts

**XML/XSLT spécifiques :**

* `Ctrl+Shift+P` / `Cmd+Shift+P` : Palette de commandes
* `Ctrl+Shift+B` / `Cmd+Shift+B` : Lancer la transformation
* `Ctrl+Espace` : Autocomplétion
* `F2` : Renommer une balise (et sa fermeture)

---

### Annexe B : Ressources en ligne

**Documentation officielle :**

* W3C XSLT : <https://www.w3.org/TR/xslt>
* W3C XPath : <https://www.w3.org/TR/xpath/>
* Saxonica (Saxon) : <https://www.saxonica.com/documentation/>

**Tutoriels en français :**

* MDN Web Docs XML : <https://developer.mozilla.org/fr/docs/Web/XML>
* Alsacréations XML : <https://www.alsacreations.com/article/lire/609-XML-introduction.html>

**Tutoriels en anglais :**

* W3Schools XML : <https://www.w3schools.com/xml/>
* W3Schools XSLT : <https://www.w3schools.com/xml/xsl_intro.asp>
* W3Schools XPath : <https://www.w3schools.com/xml/xpath_intro.asp>

**Outils de test en ligne :**

* XML Validator : <https://www.xmlvalidation.com/>
* XPath Tester : <https://www.videlibri.de/cgi-bin/xidelcgi>
* XSLT Fiddle : <https://xsltfiddle-beta.liberty-development.net/>

**Forums et communautés :**

* Stack Overflow (tag: xslt) : <https://stackoverflow.com/questions/tagged/xslt>
* Stack Overflow (tag: xpath) : <https://stackoverflow.com/questions/tagged/xpath>

---

## 🎓 Récapitulatif : Workflow complet

Voici le processus complet que vous utiliserez désormais :

### 1. **Créer ou modifier votre XML**

* Ouvrir/créer le fichier `.xml`
* Ajouter vos données structurées avec balises
* Vérifier la coche verte (validation)
* Sauvegarder (`Ctrl+S`)

### 2. **Créer ou modifier votre XSLT**

* Ouvrir/créer le fichier `.xsl`
* Définir les templates de transformation
* Utiliser XPath pour sélectionner les données
* Sauvegarder (`Ctrl+S`)

### 3. **Tester avec XPath (optionnel mais recommandé)**

* Ouvrir le fichier XML
* `Ctrl+Shift+P` → "XPath: Evaluate XPath"
* Tester vos expressions de sélection
* Ajuster si nécessaire

### 4. **Lancer la transformation**

* Ouvrir le fichier XML source
* `Ctrl+Shift+B`
* Indiquer le nom du fichier XSL
* Vérifier le terminal pour les erreurs

### 5. **Vérifier le résultat**

* Ouvrir le fichier HTML généré
* Vérifier dans un navigateur
* Noter ce qui fonctionne et ce qui ne fonctionne pas

### 6. **Itérer**

* Modifier le XSLT selon les besoins
* Relancer la transformation
* Ajuster jusqu'au résultat souhaité

---

## ✅ Checklist finale

Avant de considérer votre installation terminée, vérifiez que vous pouvez :

* Ouvrir VSCode sans erreur
* Voir les extensions installées (XML Tools)
* Créer un fichier XML et voir la validation (coche verte)
* Créer un fichier XSL avec coloration syntaxique
* Évaluer une expression XPath simple (`/catalogue/livre`)
* Lancer une transformation XSLT avec `Ctrl+Shift+B`
* Voir le fichier HTML résultant créé
* Ouvrir le fichier HTML dans un navigateur
* Comprendre les messages d'erreur de base
* Modifier et relancer une transformation

**Si vous avez coché toutes les cases, félicitations ! 🎉**

Vous êtes prêt(e) à travailler avec XML/XSLT/XPath de manière professionnelle !

---

## 💡 Besoin d'aide ?

**En cas de problème :**

1. ✅ Relisez la section de dépannage (Partie 10)
2. ✅ Vérifiez que tous vos fichiers sont sauvegardés (pas de point blanc)
3. ✅ Relisez attentivement les messages d'erreur dans le terminal
4. ✅ Vérifiez les chemins dans `settings.json` (slashes, guillemets)
5. ✅ Testez Java et Saxon en ligne de commande (Étape 5.4)
6. ✅ Redémarrez VSCode
7. ✅ Si le problème persiste, vérifiez les permissions du dossier
8. ✅ En dernier recours, postez un message sur le forum et/ou contactez-moi !

**Bon courage dans votre apprentissage de XML/XSLT/XPath ! 🚀**

---

*Guide créé pour les étudiants en information-documentation*  
*Version 1.2 - Mars 2026*
