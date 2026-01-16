# Les DTD (Document Type Definition) - Cours 

## Introduction

**Objectif** : comprendre comment une DTD permet de contrôler la structure d’un document XML afin d’éviter les incohérences (ordre des balises, répétitions, oublis), avant même tout traitement (XSLT, CSS, import dans une application).

Une **DTD** (Document Type Definition) est un ensemble de **règles** qui définissent la **structure valide** d’un document XML. Elle permet de spécifier :

- les éléments autorisés,
- leur hiérarchie,
- leur contenu,
- leurs attributs.

👉 L’objectif d’une DTD est de transformer un document XML *bien formé* en document XML *valide*.  
Sans DTD, un document XML peut être syntaxiquement correct tout en restant incohérent du point de vue métier.


---

## Partie 1 : Concepts Fondamentaux

### Bien formé vs Valide

#### Document bien formé
Un document XML **bien formé** respecte les règles syntaxiques XML de base :
- Les balises d'ouverture et de fermeture correspondent
- Les attributs sont entre guillemets
- Les éléments sont correctement imbriqués
- Il existe une unique balise racine

Un document bien formé est utilisable **sans DTD**.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<encyclopedie>
    <personne>
        <nom>HAWKING</nom>
    </personne>
</encyclopedie>
```

#### Document valide
Un document XML **valide** est un document bien formé qui **respecte les règles définies par sa DTD**.

Un document valide est plus fiable et facilite l'écriture de feuilles de style (XSL).

### Quatre types d'information dans une DTD

Une DTD spécifie :

1. **Quels éléments** sont permis dans le document
2. **Quel contenu** peuvent posséder les éléments
3. **Quels attributs** peuvent être associés à quels éléments
4. **Quelles valeurs** sont permises pour les attributs

Les points 1 et 2 utilisent les déclarations d'**éléments** (`<!ELEMENT>`).
Les points 3 et 4 utilisent les déclarations d'**attributs** (`<!ATTLIST>`).

---

## Partie 2 : Les trois formes de DTD

### 1. DTD Interne

La DTD est **directement incluse dans le document XML**, entre les balises `[ ]` après `<!DOCTYPE>`.

**Syntaxe** :
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE nom_racine [
    <!-- Déclarations DTD -->
]>
<nom_racine>
    <!-- Contenu du document -->
</nom_racine>
```

**Avantages** :
- Le document est autonome (DTD + XML dans le même fichier)
- Facile à partager
- Pas de dépendance externe

**Inconvénients** :
- Peu pratique si plusieurs documents utilisent la même DTD
- Le fichier devient volumineux

**Exemple** :
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE annuaire [
    <!ELEMENT annuaire (personne*)>
    <!ELEMENT personne (nom+, prenom+, email?)>
    <!ATTLIST personne type (étudiant | professeur) "étudiant">
    <!ELEMENT nom (#PCDATA)>
    <!ELEMENT prenom (#PCDATA)>
    <!ELEMENT email (#PCDATA)>
]>
<annuaire>
    <personne type="étudiant">
        <nom>HEUTE</nom>
        <prenom>Thomas</prenom>
        <email>webmaster@xmlfacile.com</email>
    </personne>
</annuaire>
```

### 2. DTD Externe

La DTD est **dans un fichier séparé** (`encyclopedie.dtd`), et le document XML contient seulement une **référence** vers cette DTD externe.

**Syntaxe** :
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE nom_racine SYSTEM "chemin_vers_dtd">
<nom_racine>
    <!-- Contenu du document -->
</nom_racine>
```

**Formes possibles du chemin** :

**Chemin absolu (URL complète)** :
```xml
<!DOCTYPE html SYSTEM "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

**Chemin relatif** (si DTD et document sont sur le même site) :
```xml
<!DOCTYPE encyclopedie SYSTEM "../../dtd/encyclopedie/encyclopedie.dtd">
```

**Nom simple** (si DTD et document sont dans le même répertoire) :
```xml
<!DOCTYPE encyclopedie SYSTEM "encyclopedie.dtd">
```

**Avantages** :
- DTD réutilisable par plusieurs documents
- Document XML léger
- Facile à maintenir

**Inconvénients** :
- Dépendance sur le fichier externe
- Besoin d'accès au fichier DTD pour valider

### 3. DTD Mixte

La DTD est **constituée d'une partie interne et d'une partie externe**. La partie interne complète ou modifie la DTD externe.

**Syntaxe** :
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE nom_racine SYSTEM "chemin_dtd_externe" [
    <!-- Déclarations supplémentaires/modifications -->
]>
```

**Cas d'usage** :
- Utiliser une DTD standard
- Ajouter des éléments spécifiques pour votre document
- Adapter une DTD générique à vos besoins

**Exemple** :
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE annuaire SYSTEM "annuaire-standard.dtd" [
    <!ELEMENT telephone (#PCDATA)>
    <!ATTLIST personne telephone CDATA #IMPLIED>
]>
```

---

## Partie 3 : Les Opérateurs de Composition

Les opérateurs permettent de définir comment les éléments peuvent être combinés.

### Tableau des opérateurs

| Opérateur | Signification | Syntaxe | Exemple |
|-----------|--------------|---------|---------|
| `+` | Au minimum une fois (1 ou plus) | `A+` | `nom+` : au moins un nom |
| `*` | Zéro à plusieurs fois (0 ou plus) | `A*` | `personne*` : 0 ou plusieurs personnes |
| `?` | Optionnel (0 ou 1) | `A?` | `email?` : 0 ou 1 email |
| `\|` | OU (choix entre A ou B) | `A\|B` | `(étudiant\|professeur)` : l'un ou l'autre |
| `,` | ET (A suivi de B) | `A,B` | `nom,prenom` : nom puis prénom |
| `()` | Groupement/parenthèses | `(A,B)+` | `(version\|ressource)*` : groupe répété |

### Exemples d'utilisation

#### L'opérateur `+` (au minimum une fois)

```xml
<!ELEMENT personne (nom+, prenom+, email?)>
```

**Signification** : Une personne doit contenir :
- Au minimum 1 `<nom>` (peut en avoir plusieurs)
- Au minimum 1 `<prenom>` (peut en avoir plusieurs)
- Optionnellement 1 `<email>`

**Exemples valides** :
```xml
<personne>
    <nom>DUPONT</nom>
    <nom>MARTIN</nom>  <!-- Plusieurs noms OK -->
    <prenom>Jean</prenom>
    <email>jean@example.com</email>
</personne>

<personne>
    <nom>HAWKING</nom>
    <prenom>Stephen</prenom>
    <!-- Pas d'email -->
</personne>
```

**Exemple invalide** :
```xml
<personne>
    <!-- ❌ Au moins un nom est obligatoire -->
    <prenom>Stephen</prenom>
</personne>
```

#### L'opérateur `*` (zéro à plusieurs)

```xml
<!ELEMENT annuaire (personne*)>
```

**Signification** : Un annuaire peut contenir zéro, une ou plusieurs personnes.

**Exemples valides** :
```xml
<annuaire/>  <!-- Vide -->

<annuaire>
    <personne>...</personne>
</annuaire>

<annuaire>
    <personne>...</personne>
    <personne>...</personne>
    <personne>...</personne>
</annuaire>
```

#### L'opérateur `?` (optionnel)

```xml
<!ELEMENT personne (nom, prenom, email?)>
```

**Signification** : Email est optionnel (0 ou 1 occurrence).

**Exemples valides** :
```xml
<personne>
    <nom>MARTIN</nom>
    <prenom>Claire</prenom>
</personne>

<personne>
    <nom>MARTIN</nom>
    <prenom>Claire</prenom>
    <email>claire@example.com</email>
</personne>
```

**Exemple invalide** :
```xml
<personne>
    <nom>MARTIN</nom>
    <prenom>Claire</prenom>
    <email>email1@example.com</email>
    <email>email2@example.com</email>  <!-- ❌ 2 emails (max 1) -->
</personne>
```

#### L'opérateur `,` (séquence)

```xml
<!ELEMENT personne (nom, prenom, email)>
```

**Signification** : La séquence doit être exactement : nom, puis prénom, puis email.

**Exemple valide** :
```xml
<personne>
    <nom>MARTIN</nom>
    <prenom>Claire</prenom>
    <email>claire@example.com</email>
</personne>
```

**Exemples invalides** :
```xml
<!-- ❌ Mauvais ordre -->
<personne>
    <prenom>Claire</prenom>
    <nom>MARTIN</nom>
    <email>claire@example.com</email>
</personne>

<!-- ❌ Email manquant -->
<personne>
    <nom>MARTIN</nom>
    <prenom>Claire</prenom>
</personne>
```

#### L'opérateur `|` (choix)

```xml
<!ELEMENT racine (version | ressource)*>
```

**Signification** : l’élément `racine` peut contenir **zéro, une ou plusieurs occurrences** de `version` ou de `ressource`.  
À chaque position, **un seul des deux éléments est autorisé**, et ils peuvent être **alternés librement**.

**Exemples valides** :

```xml
<racine/>
<racine><version/></racine>
<racine><ressource/></racine>
<racine><version/><ressource/><version/></racine>
```

⚠️ **Piège classique** : l’opérateur `*` autorise **zéro occurrence**.  
Pour imposer **au moins un élément** (`version` ou `ressource`), utiliser `+` :

```xml
<!ELEMENT racine (version | ressource)+>
```

#### Les parenthèses `()` (groupement)

```xml
<!ELEMENT papier (titre, auteur, (version | ressource)*)>
```

**Signification** : 
- D'abord un titre
- Puis un auteur
- Ensuite zéro ou plusieurs éléments qui sont soit `version` soit `ressource`

**Exemples valides** :
```xml
<papier>
    <titre>Les structures</titre>
    <auteur>Jean Dupont</auteur>
</papier>

<papier>
    <titre>Les structures</titre>
    <auteur>Jean Dupont</auteur>
    <version/>
    <ressource/>
    <version/>
</papier>
```

---

## Partie 4 : Les Déclarations d'Éléments

### Élément simple : #PCDATA

Un élément **simple** contient uniquement du texte (character data), pas d'éléments enfants.

**Syntaxe** :
```xml
<!ELEMENT nom_element (#PCDATA)>
```

`#PCDATA` signifie "Parsed Character Data" (données textuelles analysées).

**Exemples** :
```xml
<!ELEMENT nom (#PCDATA)>
<!ELEMENT prenom (#PCDATA)>
<!ELEMENT email (#PCDATA)>
<!ELEMENT titre (#PCDATA)>
<!ELEMENT resume (#PCDATA)>
```

**Utilisation en XML** :
```xml
<nom>HAWKING</nom>
<email>stephen@example.com</email>
<titre>Une brève histoire du temps</titre>
```

### Élément composé

Un élément **composé** contient d'autres éléments (et pas de texte direct).

**Syntaxe** :
```xml
<!ELEMENT nom_element (composition_elements)>
```

La composition utilise les opérateurs vus précédemment.

**Exemples** :
```xml
<!ELEMENT personne (nom, prenom, email?)>
<!ELEMENT annuaire (personne*)>
<!ELEMENT papier (titre, auteur+, resume, abstract, motsCles, (version | ressource)*)>
```

### Élément vide

Un élément **vide** ne contient ni texte ni éléments enfants.

**Syntaxe** :
```xml
<!ELEMENT nom_element EMPTY>
```

**Exemples** :
```xml
<!ELEMENT version EMPTY>
<!ELEMENT ressource EMPTY>
<!ELEMENT ligne EMPTY>
```

**Utilisation en XML** :
```xml
<version/>
<ressource src="fichier.pdf"/>
```

Note : Les éléments vides peuvent avoir des **attributs**.

---

## Partie 5 : Les Déclarations d'Attributs

### Syntaxe ATTLIST

**Syntaxe générale** :
```xml
<!ATTLIST nom_element attribut Type Mode>
```

Ou pour déclarer plusieurs attributs :
```xml
<!ATTLIST nom_element 
          attr1 Type1 Mode1
          attr2 Type2 Mode2>
```

### Les types d'attributs

#### CDATA - Chaîne de caractères libre

**Syntaxe** :
```xml
<!ATTLIST element attribut CDATA Mode>
```

**Description** : Accepte n'importe quelle chaîne de caractères.

**Exemples** :
```xml
<!ATTLIST personne email CDATA #IMPLIED>
<!ATTLIST ressource src CDATA #REQUIRED>
<!ATTLIST version num CDATA #REQUIRED>
```

**Utilisation** :
```xml
<personne email="thomas@example.com">...</personne>
<ressource src="document.pdf"/>
<version num="1.2"/>
```

#### Énumération - Liste fermée de valeurs

**Syntaxe** :
```xml
<!ATTLIST element attribut (valeur1 | valeur2 | valeur3) Mode>
```

**Description** : L'attribut ne peut avoir que l'une des valeurs listées.

**Exemples** :
```xml
<!ATTLIST personne type (étudiant | professeur | administrateur) #REQUIRED>
<!ATTLIST document langue (fr | en | es | de) #REQUIRED>
<!ATTLIST article statut (brouillon | publié | archivé) #IMPLIED>
```

**Utilisation** :
```xml
<personne type="étudiant">...</personne>
<document langue="fr">...</document>
<article statut="publié">...</article>
```

#### ID - Identifiant unique

**Syntaxe** :
```xml
<!ATTLIST element attribut ID Mode>
```

**Description** : Crée un identifiant unique dans le document. Aucun deux éléments ne peuvent avoir le même ID.

**Exemple** :
```xml
<!ATTLIST personne id ID #REQUIRED>
```

**Utilisation** :
```xml
<personne id="p001">...</personne>
<personne id="p002">...</personne>
```

#### IDREF - Référence à un ID

**Syntaxe** :
```xml
<!ATTLIST element attribut IDREF Mode>
```

**Description** : Référence un ID existant ailleurs dans le document.

**Exemple** :
```xml
<!ATTLIST contact responsableId IDREF #REQUIRED>
```

**Utilisation** :
```xml
<personne id="p001">Thomas</personne>
<contact responsableId="p001">...</contact>  <!-- Référence p001 -->
```

### Les modes d'attributs

#### #REQUIRED - Obligatoire

L'attribut **doit obligatoirement être présent**.

```xml
<!ATTLIST personne type (étudiant | professeur) #REQUIRED>
```

**Exemple valide** :
```xml
<personne type="étudiant">...</personne>
```

**Exemples invalides** :
```xml
<personne>...</personne>  <!-- ❌ Attribut manquant -->
<personne type="">...</personne>  <!-- ❌ Attribut vide -->
```

#### #IMPLIED - Optionnel

L'attribut est **facultatif** et n'a pas de valeur par défaut.

```xml
<!ATTLIST personne email CDATA #IMPLIED>
```

**Exemples valides** :
```xml
<personne email="thomas@example.com">...</personne>
<personne>...</personne>  <!-- Email absent, OK -->
```

#### #FIXED - Valeur fixe

L'attribut a une **valeur fixe prédéfinie**. Si présent, il doit avoir cette valeur exacte.

```xml
<!ATTLIST document version CDATA #FIXED "1.0">
```

**Exemples valides** :
```xml
<document/>  <!-- version="1.0" appliqué automatiquement -->
<document version="1.0">...</document>  <!-- Explicite, OK -->
```

**Exemple invalide** :
```xml
<document version="2.0">...</document>  <!-- ❌ Valeur différente -->
```

#### Valeur par défaut (énumération)

Pour les énumérations, on peut spécifier une valeur par défaut.

```xml
<!ATTLIST personne type (étudiant | professeur) "étudiant">
```

**Signification** : Si l'attribut `type` n'est pas présent, "étudiant" est la valeur par défaut.

**Exemples** :
```xml
<personne>...</personne>  <!-- type="étudiant" appliqué automatiquement -->
<personne type="professeur">...</personne>  <!-- Explicite -->
```

---

## Partie 6 : Exemple Complet - Annuaire

### La DTD

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE annuaire [
    <!-- Élément racine -->
    <!ELEMENT annuaire (personne*)>
    
    <!-- Élément personne -->
    <!ELEMENT personne (nom+, prenom+, email?)>
    <!ATTLIST personne 
              type (étudiant | professeur | administrateur) "étudiant"
              id ID #REQUIRED
              telephone CDATA #IMPLIED>
    
    <!-- Éléments simples -->
    <!ELEMENT nom (#PCDATA)>
    <!ELEMENT prenom (#PCDATA)>
    <!ELEMENT email (#PCDATA)>
]>
```

### Analyse détaillée

**`<!ELEMENT annuaire (personne*)>`**
- Un annuaire contient zéro ou plusieurs personnes

**`<!ELEMENT personne (nom+, prenom+, email?)>`**
- Chaque personne contient :
  - Au minimum 1 nom (peut en avoir plusieurs)
  - Au minimum 1 prénom (peut en avoir plusieurs)
  - Optionnellement 1 email

**`<!ATTLIST personne type (étudiant | professeur | administrateur) "étudiant">`**
- Attribut `type` : énumération avec défaut "étudiant"
- Si absent, "étudiant" est appliqué

**`<!ATTLIST personne id ID #REQUIRED>`**
- Attribut `id` : identifiant unique obligatoire
- Chaque personne doit avoir un ID distinct

**`<!ATTLIST personne telephone CDATA #IMPLIED>`**
- Attribut `telephone` : texte libre optionnel

### Document XML valide

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE annuaire SYSTEM "annuaire.dtd">
<annuaire>
    <!-- Personne 1 : étudiant (défaut), avec email et téléphone -->
    <personne id="p001" telephone="06.12.34.56.78">
        <nom>HEUTE</nom>
        <prenom>Thomas</prenom>
        <email>thomas@university.fr</email>
    </personne>
    
    <!-- Personne 2 : professeur explicite, sans email -->
    <personne id="p002" type="professeur">
        <nom>Bachelot</nom>
        <prenom>Mireille</prenom>
    </personne>
    
    <!-- Personne 3 : administrateur, avec plusieurs noms -->
    <personne id="p003" type="administrateur" email="admin@university.fr">
        <nom>DUPONT</nom>
        <nom>MARTIN</nom>
        <prenom>Jean</prenom>
    </personne>
    
    <!-- Personne 4 : informations minimales -->
    <personne id="p004">
        <nom>SMITH</nom>
        <prenom>Alice</prenom>
    </personne>
</annuaire>
```

---

## Partie 7 : Exemple Réaliste - Encyclopédie

### La DTD

```xml
<!DOCTYPE encyclopedie [
    <!ELEMENT encyclopedie (personne*)>
    <!ELEMENT personne (nom, prenom, publication*)>
    <!ATTLIST personne 
              datenaissance CDATA #REQUIRED
              sexe (H | F) #REQUIRED>
    <!ELEMENT nom (#PCDATA)>
    <!ELEMENT prenom (#PCDATA)>
    <!ELEMENT publication (#PCDATA)>
]>
```

### Analyse

**`<!ELEMENT personne (nom, prenom, publication*)>`**
- Chaque personne a exactement 1 nom, 1 prénom, et zéro ou plusieurs publications

**`<!ATTLIST personne datenaissance CDATA #REQUIRED>`**
- Date de naissance obligatoire (format texte libre)

**`<!ATTLIST personne sexe (H | F) #REQUIRED>`**
- Sexe obligatoire : soit "H" (homme) soit "F" (femme)

### Document XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE encyclopedie SYSTEM "encyclopedie.dtd">
<encyclopedie>
    <personne datenaissance="1942-01-08" sexe="H">
        <nom>HAWKING</nom>
        <prenom>Stephen</prenom>
        <publication>Une brève histoire du temps</publication>
    </personne>
    
    <personne datenaissance="1932-07-13" sexe="H">
        <nom>REEVES</nom>
        <prenom>Hubert</prenom>
        <publication>L'Univers expliqué à mes petits-enfants</publication>
        <publication>Patience dans l'azur, L'évolution cosmique</publication>
        <publication>Poussières d'étoiles</publication>
    </personne>
    
    <personne datenaissance="1879-03-14" sexe="H">
        <nom>EINSTEIN</nom>
        <prenom>Albert</prenom>
        <publication>Des ondes gravitationnelles</publication>
        <publication>Sur la théorie quantique du rayonnement</publication>
    </personne>
    
    <personne datenaissance="1867-11-07" sexe="F">
        <nom>CURIE</nom>
        <prenom>Marie</prenom>
        <publication>Traité de radioactivité</publication>
    </personne>
</encyclopedie>
```

---

## Partie 8 : Exercice Pratique

### Énoncé

Le fichier `papier.xml` suivant n'est pas conforme à sa DTD. À vous de corriger la DTD !

**papier.xml** :
```xml
<?xml version="1.0"?>
<!DOCTYPE papier SYSTEM "papier.dtd">
<papier>
    <titre>Les structures documentaires</titre>
    <auteur>Stéphane Crozat</auteur>
    <auteur>Bruno Bachimont</auteur>
    <resume>Nous proposons dans cet article d'aborder ...</resume>
    <abstract>In this paper we define...</abstract>
    <motsCles>
        <terme>Ingénierie des connaissances</terme>
        <terme>Document</terme>
    </motsCles>
    <version num="1"/>
    <ressource src="sic_00001016.pdf"/>
</papier>
```

**papier.dtd (actuelle - INCORRECTE)** :
```xml
<!ELEMENT papier (titre, sousTitre?, auteur, resume, abstract, motsCles, (version | ressource)*)>
<!ELEMENT titre (#PCDATA)>
<!ELEMENT sousTitre (#PCDATA)>
<!ELEMENT auteur (#PCDATA)>
<!ELEMENT resume (#PCDATA)>
<!ELEMENT motsCles (#PCDATA)>
<!ELEMENT version (#PCDATA)>
<!ELEMENT ressource EMPTY>
```



---

## Résumé

### Points clés

✅ **Une DTD valide un document XML** par rapport à une structure prédéfinie

✅ **Trois formes** : Interne, Externe, Mixte

✅ **Opérateurs** : `+`, `*`, `?`, `|`, `,`, `()`

✅ **Deux déclarations principales** : 
- `<!ELEMENT>` pour la structure
- `<!ATTLIST>` pour les attributs

✅ **Document bien formé** : Respecte XML
✅ **Document valide** : Respecte XML + DTD

### Comparaison DTD vs XML Schema

| Aspect | DTD | XML Schema |
|--------|-----|-----------|
| **Simplicité** | Simple | Complexe |
| **Types de données** | Limités | Riches (booléens, entiers, etc.) |
| **Héritage** | Non | Oui |
| **Espaces de noms** | Non | Oui |
| **Cas d'usage** | Petits modèles | Modèles complexes |

Les DTD sont parfaites pour débuter et pour des modèles simples, tandis que XML Schema est préféré pour les applications professionnelles complexes.

---

**Continuez à pratiquer avec des exemples réels et n'hésitez pas à valider vos documents XML contre une DTD !**