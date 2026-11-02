# Stremio Glass — correctif lecteur 4.3.3 (candidate de test)

## Contenu

Cette archive est construite à partir de la version 4.2 fournie par l’utilisateur, avec les corrections ciblées du lecteur 4.3.3. Les fichiers sont à la racine de l’archive.

## Correctifs du lecteur

- Attend l’événement `ready` (ou le callback `client.add`) avant de sélectionner un fichier. Cela garantit que les métadonnées ET le stockage torrent sont prêts ; l’événement `metadata` seul peut être trop précoce.
- Corrige le chemin du script Service Worker WebTorrent : `dist/sw.min.js` (le fichier n’est pas à la racine du paquet npm).
- Charge WebTorrent via l’URL de module du tutoriel officiel, puis tente un second CDN si nécessaire.
- Affiche des erreurs distinctes si le CDN, WebRTC, le Service Worker ou le serveur vidéo échoue.
- Utilise `file.streamTo(video)`, la méthode de lecture navigateur documentée par WebTorrent, après création du serveur HTTP adossé au Service Worker.
- Conserve les diagnostics de chargement, les erreurs média, la progression, la vitesse, les pairs et l’estimation restante.
- Garde les commandes Lecture/Pause et le bouton de plein écran iOS/Safari.
- Versionne le cache Service Worker en `stremio-glass-v4.3.3`.

## Installation

Faire une sauvegarde du dépôt avant déploiement. Remplacer à la racine `index.html`, `sw.js`, `manifest.webmanifest`, `icon-192.png` et `icon-512.png`.

## Limites de validation

La syntaxe JavaScript et l’intégrité de l’archive peuvent être vérifiées ici, mais cette version n’a pas été exécutée sur un iPad physique ni testée avec un torrent réel. Il serait trompeur de garantir à 100 % la lecture avant cet essai.

WebTorrent dans un navigateur dépend de WebRTC et ne se connecte qu’aux pairs compatibles WebTorrent/WebRTC. Les codecs et conteneurs doivent aussi être pris en charge par Safari. Les formats MP4/MOV/WebM ne garantissent pas à eux seuls la compatibilité du codec audio/vidéo.
