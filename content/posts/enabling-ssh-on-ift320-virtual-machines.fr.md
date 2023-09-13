---
draft: false
date: 2023-09-13
title: "Utiliser SSH pour accéder aux machines virtuelles pour le cours IFT320"
tags: ["ift320", "ssh", "terminal"]
categories: ["university", "sherbrooke"]
description: "Pratique, mais demande un peu de jus de bras avant de pouvoir s'en servir sous Linux."
canonicalURL: "https://jessyprovencher.xyz/posts/enabling-ssh-on-ift320-virtual-machines/"
---

# Problème de clés

Dans le cadre du premier devoir (TP1) du cours IFT320, donné à l'Université de Sherbrooke, il faut rédiger du code pour un pilote (driver) Linux.

Afin de faciliter le transfert de code entre les deux machines virtuelles, il est préférable d'utiliser une connexion SSH. Par contre, puisque ces machines utilisent une vieille version du kernel (2.6.15.7) et d'anciens packages, il est possible de rencontrer des erreurs de "mismatch" de clés lorsqu'on tente de s'y connecter.

Le problème réside dans les algorithmes utilisés qui sont rendus obsolètes. Vivons dangereusement en autorisant l'usage de ceux-ci pour permettre la connexion aux machines virtuelles. 🙃

Plus précisément, voici le message d'erreur que j'avais lorsque je tentais de me connecter via SSH:
```
Unable to negotiate with x.x.x.x port 22: no matching key exchange method found. Their offer: diffie-hellman-group-exchange-sha1,diffie-hellman-group14-sha1,diffie-hellman-group1-sha1
```

# Comment régler ça?

Pour ce faire, il va falloir spécifier les algorithmes à utiliser.

Ouvrez le fichier situé ici `~/.ssh/config`. Il est possible qu'il n'existe pas, vous pouvez le créer à l'aide de la commande `touch`.

Pour chaque machine vous devez ajouter ce bloc de texte:
```
Host x.x.x.x    
    KexAlgorithms +diffie-hellman-group1-sha1
    Ciphers aes128-cbc,3des-cbc,aes192-cbc,aes256-cbc
    User ift320
    PubkeyAcceptedAlgorithms +ssh-rsa
    HostkeyAlgorithms +ssh-rsa
```

où `x.x.x.x` est l'adresse IP de chaque machine. Vous pouvez la trouver grâce à la commande `ifconfig`.

Vous pouvez également remplacer par `Host *` pour l'appliquer à tous les hôtes (hosts).

Le changement devrait être immédiat, mais dans le cas échéant, vous pouvez redémarrer le service SSH à l'aide de la commande suivante: `systemctl restart sshd`.

Si tout se passe bien, vous devriez être en mesure de vous connecter via SSH aux machines virtuelles!

# Certaines commandes ne fonctionnent pas?

Effectivement, si vous tentez de faire par ex. `clean` ou `nano`, vous risquez d'avoir l'erreur suivante: `'xterm-256color': unknown terminal type`.

Pour régler celle-ci, vous devrez modifier le fichier `.bashrc` ou `.zshrc` sur la machine hôte.

Ajoutez cette ligne: `export TERM="xterm"`.

Vous aurez peut-être besoin de faire `source .bashrc` ou `source .zshrc` afin que les changements soient appliqués. Vous serez ensuite en mesure d'utiliser ces commandes.

# Conclusion

Grâce à ces modifications, vous serez en mesure de travailler sur les machines virtuelles sans passer par leur interface graphique.

Sur ce, bonne chance avec le devoir! 📝