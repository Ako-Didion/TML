# tml : serveur tModLoader (Docker)

Configuration de mon serveur tModLoader modé, hébergé sur un VPS Ubuntu avec Docker.

## Contenu du dépôt

- `Dockerfile` et `docker-compose.yml` : conteneur du serveur (projet officiel tModLoader).
- `tModLoader/Mods/install.txt` et `enabled.json` : liste des mods du Workshop à installer et à activer.
- `tModLoader/serverconfig.example.txt` : modèle de configuration du serveur.
- `tModLoader/ModConfigs/` : réglages des mods.

Ne sont pas versionnés : `serverconfig.txt` (contient le mot de passe), les mondes (`Worlds/`) et les fichiers téléchargés (`server/`, `steamapps/`).

## Installation

1. Cloner le dépôt :
```bash
   git clone git@github.com:Ako-Didion/tml.git && cd tml
```
2. Créer la vraie configuration à partir du modèle, puis modifier le mot de passe et le nom du monde :
```bash
   cp tModLoader/serverconfig.example.txt tModLoader/serverconfig.txt
   nano tModLoader/serverconfig.txt
```
3. Dans `docker-compose.yml`, mettre l'UID et le GID de l'utilisateur (commande `id`).
4. Lancer le serveur :
```bash
   docker compose up -d --build
   docker logs -f tml
```

Le serveur est prêt quand les logs indiquent qu'il écoute sur le port 7777.

## Utilisation

| Action | Commande |
|---|---|
| Suivre les logs | `docker logs -f tml` |
| Redémarrer | `docker compose restart` |
| Arrêter | `docker compose stop` |
| Console du serveur | `docker attach tml` (quitter avec Ctrl-P puis Ctrl-Q) |

## Mettre à jour tModLoader

```bash
docker compose build --no-cache && docker compose up -d
```

Les joueurs doivent avoir la même version de tModLoader et les mêmes mods que le serveur.

## Modifier les mods

Créer un modpack dans le jeu (Workshop, Mod Packs, Save Enabled as New Mod Pack), remplacer `install.txt` et `enabled.json` dans `tModLoader/Mods/`, puis `docker compose restart`.

## Sauvegardes

Les mondes sont dans `tModLoader/Worlds/` et ne sont pas dans Git : à sauvegarder séparément.
