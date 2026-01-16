# Les Schémas XML (XML Schema – XSD) 

## Introduction

**XML Schema (XSD)** est une technologie de validation XML plus moderne et plus puissante que les DTD.  
Contrairement aux DTD, issues de SGML, les schémas XML sont eux-mêmes des **documents XML**, ce qui permet une validation plus fine et plus expressive.

Les schémas XML ne remplacent pas les DTD, mais les **dépassent largement** en termes de précision, de typage et de contrôle.

**Objectifs** :
- Comprendre les bases de XML Schema (XSD)
- Lire et interpréter un schéma simple
- Identifier clairement les différences avec une DTD
- Valider un document XML à l’aide d’un schéma

---

## Partie 1 : DTD vs XML Schema

### Comparaison rapide

**Points forts des schémas XML** :
- **Types riches** : booléens, entiers, dates, intervalles…
- **Héritage** : possibilité de définir des types réutilisables
- **Occurrences précises** : cardinalités numériques exactes
- **Gestion des espaces de noms**
- **Schémas = documents XML** (lisibles et manipulables)

**Quand utiliser XSD ou DTD ?**
- **DTD** : modèles simples, apprentissage, petits fichiers
- **XSD** : applications professionnelles, validation stricte

---

## Partie 2 : Référencer un schéma XML depuis un document XML

### Principe

Un document XML indique **où se trouve le schéma** qui sert à le valider à l’aide d’attributs du namespace `xsi`.

### Exemple (document XML sans namespace)

```xml
<bibliotheque xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:noNamespaceSchemaLocation="ma_bibliotheque.xsd">
```

### Signification des attributs

- `xmlns:xsi`  
  Déclare le namespace **XML Schema Instance**, utilisé uniquement dans le document XML.

- `xsi:noNamespaceSchemaLocation`  
  Indique le chemin vers le fichier XSD lorsque le document XML **n’utilise pas de namespace**.

⚠️ **Important** :  
- `xsi:` est utilisé **dans le document XML**
- il ne sert **qu’à référencer le schéma**, pas à écrire des règles

---

## Partie 3 : Structure d’un fichier XSD (côté schéma)

Une fois le schéma référencé depuis le XML, sa structure est définie dans un **fichier XSD distinct**.

### Début d’un fichier XSD

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           elementFormDefault="qualified"
           attributeFormDefault="unqualified">
```

### Signification

- `xmlns:xs`  
  Déclare le namespace du **langage XML Schema**.

- `xs:`  
  **Préfixe** utilisé **dans le fichier XSD** pour écrire les règles (`xs:element`, `xs:sequence`, etc.).

- `elementFormDefault="qualified"`  
  Les éléments définis doivent être qualifiés par un namespace.

- `attributeFormDefault="unqualified"`  
  Les attributs ne sont pas qualifiés par défaut.

⚠️ **À retenir** :  
- `xsi:` → utilisé dans le **XML**
- `xs:` → utilisé dans le **XSD**  
Ce sont deux namespaces différents, avec deux rôles distincts.

### Éléments de base

| Élément | Rôle | Syntaxe |
| :-- | :-- | :-- |
| `xs:element` | Élément | `<xs:element name="titre" type="xs:string"/>` |
| `xs:complexType` | Structure complexe | `<xs:complexType><xs:sequence>...</xs:sequence></xs:complexType>` |
| `xs:sequence` | Ordre strict | Enfants dans l'ordre |
| `xs:choice` | Choix exclusif | Une option parmi les choix |
| `xs:all` | Ordre libre | Enfants dans n'importe quel ordre |
---

## Partie 4 : Exemple complet — Bibliothèque

### Document XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<bibliotheque xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="ma_bibliotheque.xsd">
	<roman>
		<titre>Imajica</titre>
		<auteur>Clive Barker</auteur>
		<prix>6</prix>		
	</roman>
	<roman>
		<titre>Dune</titre>
		<auteur>Frank Herbert</auteur>
		<prix>7</prix>
	</roman>
	<magazine>
		<titre>Science et Vie</titre>
		<dateparution>2019-02-01</dateparution>
	</magazine>
	<roman>
		<titre>Christine</titre>
		<auteur>Stephen King</auteur>
		<prix>5</prix>
	</roman>
</bibliotheque>

```

### Schéma XSD correspondant

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           elementFormDefault="qualified" 
           attributeFormDefault="unqualified">
           
    <xs:element name="bibliotheque">
        <xs:complexType>
            <xs:choice maxOccurs="unbounded">
                <xs:element name="magazine">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="titre" type="xs:string"/>
                            <xs:element name="dateparution" type="xs:date"/>
                        </xs:sequence>
                    </xs:complexType>
                </xs:element>
                <xs:element name="roman">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="titre" type="xs:string"/>
                            <xs:element name="auteur" type="xs:string"/>
                            <xs:element name="prix" type="xs:integer"/>
                        </xs:sequence>
                    </xs:complexType>
                </xs:element>
            </xs:choice>
        </xs:complexType>
    </xs:element>
</xs:schema>
<!-- Je définie que BIBLIOTHEQUE peut contenir 
au choix (xs:choice) un nombre quelquonque (maxOccurs="unbounded") d'élements ROMAN et MAGAZINE.
Chaque MAGAZINE comprend obligatoirement une séquence (xs:sequence) de deux éléments: un TITRE et une DATEPARUTION.
La DATEPARUTION contient obligatoirement une date (type="xs:date", format année-mois-jour) -->
```

---

### Lecture du schéma

- `xs:choice` : à chaque occurrence, **un seul des éléments est autorisé**
- `maxOccurs="unbounded"` : ce choix peut être répété librement

👉 La bibliothèque peut contenir une suite de `roman` **ou** `magazine`, dans n’importe quel ordre.

---

## Partie 5 : Types de données XSD (exemples)

| Type XSD | Exemple valide                |
|---------|-------------------------------|
| `xs:string` | <titre>Science et Vie</titre> |
| `xs:integer` | 7                             |
| `xs:decimal` | 12.5                          |
| `xs:date` | 2019-02-01                    |
| `xs:boolean` | true / false                  |

👉 Avantage majeur sur les DTD : la validation porte aussi sur le **type des données**.

---

## Partie 6 : Opérateurs XSD vs DTD

| Opérateur XSD                         | Équivalent DTD | Exemple             | Signification |
|:--------------------------------------|:---------------|:--------------------| :-- |
| `xs:sequence`                         | `,`            | `titre,auteur,prix` | Ordre strict |
| `xs:choice`                           | `(A\|B)`       | `(roman\|magazine)` | Un seul élément par occurrence |
| `xs:all`                              | ` (pas d'équivalent exact)`       |          | Tous éléments requis, ordre libre |
| `minOccurs="0"`                       | `?`            | Optionnel           | 0 ou 1 |
| `minOccurs="0" maxOccurs="unbounded"` | `*`            | 0 ou plus           | Zéro ou plus |
| `minOccurs="1" maxOccurs="unbounded"` | `+`            | 1 ou plus           | Un ou plus |
**XSD avantage** : des valeurs précises :

```xml
<!-- Exactement 3 -->
minOccurs="3" maxOccurs="3"
```
**Note importante** :
- `xs:all` n'a pas d'équivalent en DTD : il permet des éléments dans n'importe quel ordre.
- En DTD, `(A,B)` impose l'ordre A puis B, ce qui correspond à `xs:sequence` en XSD.
- Pour reproduire un ordre libre en DTD, il faudrait lister toutes les permutations possibles : `(A,B) | (B,A)`, ce qui devient impossible avec 3+ éléments.

---

## Partie 7 : Exercice pratique

**Objectif** : modifier uniquement le schéma XSD, **sans changer le document XML**.

Contraintes :
1. Prix minimum : 1
2. Maximum 10 romans
3. Magazine : numéro optionnel
4. Auteur : minimum 2 caractères

---
**Solution** :
Voici les modifications à apporter (à intégrer dans la structure existante du schéma) :

```xml
<!-- roman limité à 10 -->
<xs:element name="roman" maxOccurs="10">

<!-- Prix minimum 1 -->
<xs:element name="prix">
    <xs:simpleType>
        <xs:restriction base="xs:integer">
            <xs:minInclusive value="1"/>
        </xs:restriction>
    </xs:simpleType>
</xs:element>

<!-- Auteur min 2 caractères -->
<xs:element name="auteur">
    <xs:simpleType>
        <xs:restriction base="xs:string">
            <xs:minLength value="2"/>
        </xs:restriction>
    </xs:simpleType>
</xs:element>

<!-- Magazine : numéro optionnel -->
<xs:element name="numero" type="xs:integer" minOccurs="0"/>
```
---
## Sources Officielles

### 📖 W3C (Normes)

1. **XML Schema Part 1** : https://www.w3.org/TR/xmlschema-1/
2. **XML Schema Part 2 (Types)** : https://www.w3.org/TR/xmlschema-2/

### 🛠️ Validateurs Gratuits

1. **FreeFormatter** : https://www.freeformatter.com/xml-validator-xsd.html
2. **XMLValidation** : https://www.xmlvalidation.com/
3. XmlCopyEditor, VScode, NotePad++
