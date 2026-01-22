---

## 📦 Annexe : Extension optionnelle pour XSLT avancé

### Alternative : XSLT/XPath for VS Code (DeltaXML)

Si vous souhaitez une **meilleure expérience XSLT**, vous pouvez remplacer ou compléter XML Tools par l'extension DeltaXML.

**Avantages supplémentaires :**
- ✅ Coloration syntaxique XSLT avancée (meilleure que XML Tools)
- ✅ Autocomplétion des éléments XSLT (`<xsl:...`)
- ✅ Évaluation XPath avec surlignage direct dans le XML
- ✅ Validation XSLT en temps réel
- ✅ Intégration native avec Saxon

---

### Installation

**Étape 1 : Installer les extensions**

1. Ouvrez les extensions (`Ctrl+Shift+X`)
2. Recherchez et installez :
   - **"XML"** par **Red Hat** (si pas déjà installé)
   - **"XSLT/XPath for VS Code"** par **DeltaXML**

**Étape 2 : Compléter votre settings.json**

Ajoutez ces 2 lignes à votre fichier `.vscode/settings.json` existant :

**🪟 Windows :**
```json
{
  "java.home": "C:/Outils/jdk17",
  "saxon.jar.path": "C:/Outils/saxon-he-12.9.jar",
  
  // Configuration DeltaXML (ajoutez ces 2 lignes)
  "XSLT.tasks.saxonJar": "C:/Outils/saxon-he-12.9.jar",
  "XSLT.tasks.javaExecutablePath": "C:/Outils/jdk17/bin/java.exe"
}
```

**🍎 Mac :**
```json
{
  "java.home": "/Users/votrenom/Outils/jdk17",
  "saxon.jar.path": "/Users/votrenom/Outils/saxon-he-12.9.jar",
  
  // Configuration DeltaXML
  "XSLT.tasks.saxonJar": "/Users/votrenom/Outils/saxon-he-12.9.jar",
  "XSLT.tasks.javaExecutablePath": "/Users/votrenom/Outils/jdk17/bin/java"
}
```

---

### Utilisation de l'évaluation XPath avec DeltaXML

**Avantage par rapport à XML Tools :** Les résultats sont surlignés directement dans votre fichier XML !

1. Ouvrez votre fichier XML (`catalogue.xml`)
2. `Ctrl+Shift+P` → Tapez "XPath"
3. Choisissez **"XPath: Evaluate XPath"**
4. Entrez votre expression : `/catalogue/livre/titre`
5. Les éléments correspondants sont **surlignés en jaune** dans le document

> **💡 Avec XML Tools :** Les résultats s'affichent dans un panneau séparé  
> **💡 Avec DeltaXML :** Les résultats sont surlignés directement dans le XML (plus visuel !)

---

### Comparaison rapide

| Fonctionnalité | XML Tools | DeltaXML XSLT/XPath |
|----------------|-----------|---------------------|
| Validation XML | ✅ | ✅ (via Red Hat XML) |
| Formatage XML | ✅ | ✅ |
| Évaluation XPath | ✅ Résultats en panneau | ✅ Surlignage direct |
| Coloration XSLT | ⚠️ Basique | ✅ Avancée |
| Autocomplétion XSLT | ❌ | ✅ |
| Transformation XSLT | ❌ Manuelle via tasks | ✅ + Intégration Saxon |

---

### 🎯 Quelle configuration choisir ?

**Configuration actuelle (XML Tools + tasks.json) :**
- ✅ Fonctionne parfaitement
- ✅ Simple et efficace
- ✅ Suffisant pour apprendre XML/XSLT
- **→ Gardez cette configuration si elle vous convient !**

**Configuration avec DeltaXML (optionnelle) :**
- ✅ Meilleure coloration syntaxique XSLT
- ✅ Autocomplétion XSLT
- ✅ XPath plus visuel (surlignage direct)
- ⚠️ Légèrement plus de configuration
- **→ Installez en complément si vous voulez plus de confort**

---

### ⚠️ Note importante

**Vos transformations XSLT fonctionnent déjà** grâce au fichier `tasks.json` que vous avez configuré. L'extension DeltaXML n'est **pas nécessaire** pour que les transformations marchent, elle apporte juste plus de confort d'édition.

Vous pouvez :
- Garder uniquement XML Tools (ça marche)
- Installer DeltaXML en plus (plus confortable)
- Remplacer XML Tools par XML (Red Hat) + DeltaXML (recommandé pour XSLT intensif)