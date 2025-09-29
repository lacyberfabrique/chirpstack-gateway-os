# ChirpStack Gateway OS

ChirpStack Gateway OS est un système d'exploitation embarqué open-source basé sur [OpenWrt](https://openwrt.org/) pour les passerelles LoRa<sup>&reg;</sup>. Il fournit une interface web pour la configuration et contient des options de configuration prédéfinies pour le matériel LoRa courant afin de faciliter la mise en place d'une passerelle LoRa et optionnellement d'un serveur de réseau LoRaWAN<sup>&reg;</sup> basé sur ChirpStack.

**Note :** Si vous recherchez les recettes [Yocto](https://www.yoctoproject.org/) de l'ancienne version basée sur Yocto de ChirpStack Gateway OS, veuillez basculer vers la branche [v4_yocto](https://github.com/chirpstack/chirpstack-gateway-os/tree/v4_yocto).

## Documentation et binaires

Veuillez vous référer à la [documentation ChirpStack Gateway OS](https://www.chirpstack.io/docs/chirpstack-gateway-os/) pour la documentation et les images pré-compilées.

## Compilation depuis les sources

### Prérequis

La compilation de ChirpStack Gateway OS nécessite :

* [Docker](https://www.docker.com/)

### Initialisation

Pour initialiser l'environnement de compilation [OpenWrt](https://openwrt.org/), exécutez la commande suivante :

```bash
make init
```

Cela va :

* Cloner le code OpenWrt
* Récupérer tous les feeds OpenWrt, y compris le [ChirpStack OpenWrt Feed](https://github.com/chirpstack/chirpstack-openwrt-feed)
* Créer des liens symboliques pour la configuration et les fichiers

### Mise à jour

Cette étape n'est pas requise après avoir exécuté `make init`, mais vous permet de mettre à jour les sources OpenWrt et les feeds à un moment ultérieur :

```bash
make update
```

### Compilation

Pour compiler ChirpStack Gateway OS, vous devez d'abord entrer dans l'environnement de développement basé sur Docker :

```
make devshell
```

#### Changer de configuration

Chaque cible et image a son propre fichier de configuration OpenWrt, ses fichiers et ses correctifs. Ceux-ci peuvent être trouvés dans le répertoire `conf` de ce dépôt.

Pour basculer vers l'un de ces environnements de configuration, vous devez exécuter :

```
make switch-env ENV=nom-de-l-env
```

Par exemple, si vous souhaitez basculer vers `lacyber_raspberrypi_bcm27xx_bcm2709`, vous exécutez :

```
make switch-env ENV=lacyber_raspberrypi_bcm27xx_bcm2709
```

Cela va :

* Annuler tous les correctifs précédemment appliqués
* Mettre à jour les liens symboliques pour la configuration et les fichiers OpenWrt
* Appliquer tous les correctifs

#### Compilation de l'image

Une fois que la configuration a été définie, exécutez la commande suivante pour compiler l'image ChirpStack Gateway OS :

```bash
make
```

Notez que cela peut prendre plusieurs heures selon la configuration sélectionnée et nécessitera une quantité importante d'espace disque.

#### Modifications de configuration

**Note :** Les commandes listées ci-dessous doivent être exécutées dans le répertoire `openwrt`.

Pour apporter des modifications de configuration (par exemple, ajouter des paquets supplémentaires), vous pouvez exécuter :

```bash
make menuconfig
```

Comme les mises à jour des paquets OpenWrt peuvent introduire de nouvelles options de configuration au fil du temps, vous pouvez exécuter la commande suivante pour mettre à jour la configuration :

```bash
make defconfig
```

Veuillez également vous référer à la [documentation d'utilisation du système de compilation OpenWrt](https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem).

## Liens

* [Documentation ChirpStack](https://www.chirpstack.io/)
* Dépôt [chirpstack-openwrt-feed](https://github.com/chirpstack/chirpstack-openwrt-feed)
