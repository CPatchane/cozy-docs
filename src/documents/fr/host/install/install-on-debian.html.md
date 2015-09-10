---
title: "sur Debian"
layout: "default"
category: "host"
menuOrder: 1
toc: false
---


<div style="height: 0; overflow: shown; text-align: right">
<img alt="Logo de Debian" src="/assets/images/debian-logo.png">
</div>

# Installer Cozy sur Debian

Vous devez être sous **Debian 8 Jessie (stable)** pour pouvoir suivre les étapes ci-dessous.

```
root@debian-8:~# lsb_release -c
Codename:     jessie
```

Si `lsb_release` n'est pas installé, vous être probablement sur une version
trop ancienne de Debian. Vous pouvez vous en assurer en regardant la version
de cette façon :

```
root@debian-8:~# cat /etc/debian_version
8.1
```

<br>

1. Assurez-vous que les paquets `ca-certificates` et `apt-transport-https` sont bien installés
    ```
    apt-get install ca-certificates apt-transport-https
    ```
2. Importez la clé publique du dépôt
    ```
    wget -O - https://debian.cozycloud.cc/cozy.gpg.key 2>/dev/null | apt-key add -
    ```
3. En option, vérifiez que la clé importée est valide
    ```
    apt-key --keyring /etc/apt/trusted.gpg finger
    ```
    Vous devriez lire:
    ```
    pub   2048R/2765B235 2014-11-17 [expires: 2015-11-17]
          Key fingerprint = E28C F8B2 ABBF E285 743B  27F1 BCB2 ED5D 2765 B235
    uid                  Cozy Debian Packaging <debian-packaging@cozycloud.cc>
    sub   2048R/D58A9D35 2014-11-17 [expires: 2015-11-17]
    ```
4. Ajoutez le dépôt Cozy à vos sources de logiciels.
    ```
    echo 'deb [arch=amd64] https://debian.cozycloud.cc/debian jessie main' \
    > /etc/apt/sources.list.d/cozy.list
    ```
5. Installez Cozy
    ```
    apt-get update
    apt-get install cozy
    ```
6. Assurez vous que le service Nginx est bien démarré:
    ```
    service nginx start
    ```

7. Enregistrer votre compte Cozy et profitez!
    ```
    https://your-cozy-IP/

## Que faire en cas de soucis

### Comment re-générer le certificat ?

    sudo openssl req -x509 -nodes -newkey rsa:2048 -keyout /etc/cozy/server.key -out /etc/cozy/server.crt -days 3650 -subj "/CN=URL.DE.VOTRE.INSTANCE"

