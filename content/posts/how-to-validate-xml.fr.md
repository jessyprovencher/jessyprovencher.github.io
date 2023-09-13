---
draft: false
date: 2021-05-15
title: "Comment valider un fichier XML?"
tags: ["xml", "dtd", "xsd"]
categories: ["code quality"]
description: "Oui, même les documents XML doivent être validés."
canonicalURL: "https://jessyprovencher.xyz/posts/how-to-validate-xml/"
---

La semaine passée, j'ai eu un retour sur les bases de XML et JSON. Je m'attendais à un long monologue sur des choses que
je connaissais déjà bien. Cependant, j’ai appris certaines choses qui pourraient être utiles à d'autres personnes.
Parlons-en! :coffee:

# Qu'est-ce que XML?

XML signifie Extensible Markup Language. C'est un langage de balisage qui spécifie un ensemble de règles d'encodage pour documents dans un format à la fois lisible par l'humain et lisible par les machines. C'est dans la même veine que HTML, comme le nom suggère. Un fichier HTML est un fichier XML valide, mais pas l'inverse. Vous voudrez peut-être recourir à l'utilisation de ce type de fichiers lorsque vous cherchez un moyen de stocker des configurations, de transmettre des données ou simplement d'écrire des documents "de type html". De nos jours, certains pourraient dire que JSON a pris sa place mais je pense qu'il est toujours important de connaître quelques bases qui pourraient être utiles lorsque vous vous y attendez le moins. Tant que des technologies telles que HTTP/HTTPS, les flux RSS et les fichiers HTML existent, XML est là pour rester. :wink:

# Pourquoi valider?

En faisant la validation, nous nous assurons que notre document est conforme à un ensemble de règles détaillant
la structure et le contenu. Simplement, nous nous assurons qu'il est valide. Ça semble
évident non? -- mais qu'est-ce que «valide»? -- Un document XML valide doit être bien formé.

Il doit respecter ces règles de syntaxe:

* Les balises sont sensibles à la casse
* Les éléments doivent être correctement imbriqués
* Les documents doivent avoir un élément racine
* Les valeurs d'attributs doivent être entre guillemets (simples ou doubles)
* Les éléments doivent avoir une balise de fermeture ex. `<balise></balise>`

# Comment valider?

Pour valider notre document XML, nous devrons créer deux nouveaux fichiers. Je ne donnerai pas d'exemples car je suis sûr
que vous pouvez trouver de la documentation et/ou des outils en ligne pour vous aider dans cette tâche.

Tout d'abord, nous aurons besoin d'un fichier DTD (Document Type Definition). Il définit les blocs de construction valides de notre document XML
et sa structure avec une liste d'éléments et d'attributs validés. Deuxièmement, nous aurons besoin d'un fichier de schéma XML (XSD). C'est une
directive du [World Wide Web Consortium](https://www.w3.org) (W3C) qui explique comment définir formellement les éléments dans un document XML.

---

Maintenant, testons notre document XML. :scientist:

De nombreuses ressources en ligne et IDEs (par exemple Eclipse) fournissent des moyens de valider notre document.
Cependant, je vais vous montrer une façon rapide et simple de le faire localement. Nous aurons besoin du programme
xmllint inclus avec la librairie [libxml](http://www.xmlsoft.org).

Si vous utilisez Arch Linux, vous pouvez installer les requis avec la commande suivante:

```console
pacman -S libxml2
```

Validation XML avec un fichier DTD:

```console
xmllint --valid --dtdvalid <dtd> --noout <xml>
```

Validation XML avec un schéma XML (xsd):

```console
xmllint --noout --schema <xsd> <xml>
```
