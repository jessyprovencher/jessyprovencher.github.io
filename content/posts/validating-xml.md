---
draft: false
date: 2021-05-15
title: "Validating XML"
tags: ["xml", "dtd", "xsd"]
categories: ["code quality"]
description: "Yes, even XML documents must be validated."
canonicalURL: "https://jessyprovencher.xyz/posts/validating-xml/"
---

Last week, I had a lecture about the fundamentals of XML and JSON. I expected another long explanation about things
I was already well acquainted with. However, I've learned a few things that others may find useful.
Let's talk about it! :coffee:

# What is XML?

XML stands for Extensible Markup Language. It's a markup language that specifies a set of rules for encoding
documents in a format that is both human-readable and machine-readable. It's in the same vein as HTML, as the
name suggests. An HTML file is a valid XML file, but not the other way around. You might want to resort to use
this type of files when looking for a way to store configs, transmit data or simply writing "html-like" documents.
Nowadays, some might say that JSON took it's place but I think it's still important to know some basics which could
come useful when you lease expect it. As long as technologies such as HTTP/HTTPS, RSS feeds & HTML exists, XML is here to stay. :wink:

# Why validate?

By doing validation we ensure our document conforms to a set of rules detailing
the structure and content. Simply, we make sure it's valid. Seems
obvious right? -- but what is "valid"? -- A valid XML document must be well formed.

It must respect these syntax rules:

* Tags are case sensitive
* Elements must be properly nested
* Documents must have a root element
* Attributes values be quoted (single or double)
* Elements must have a closing tag eg. `<tag></tag>`

# How to validate?

To validate our XML document, we'll need to create two new documents. I won't provide examples because I'm sure you
can find some docs and/or tools online to help you with this task.

Firstly, we'll need a DTD (Document Type Definition) file. It defines the valid building blocks of our XML document
and its structure with a list of validated elements & attributes. Secondly, we'll need a XML schema (XSD) file. It's a
guideline from the [World Wide Web Consortium](https://www.w3.org) (W3C) that explains how to formally define the elements
in an XML document.

---

Now, let's test our XML document shall we? :scientist:

Many online resources and IDEs (eg. Eclipse) provide ways to validate. However, I'll show you a quick & simple
way to do it locally. We'll need the xmllint program included with [libxml](http://www.xmlsoft.org) library.

If you're using Arch Linux, you can install the requirements with the
following command:

```console
pacman -S libxml2
```

Validate XML with DTD file:

```console
xmllint --valid --dtdvalid <dtd> --noout <xml>
```

Validate XML with XML schema (xsd):

```console
xmllint --noout --schema <xsd> <xml>
```
