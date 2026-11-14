# agenteca-claude-code

Plugin Agenteca pour **Claude Code**. Il ajoute la commande `/hub` et déclare le serveur MCP `agenteca`, qui permet de chercher, lire, installer, mettre à jour et retirer des paquets d'agents IA sans quitter l'outil.

Le plugin ne contient aucune logique : un skill (des consignes) et une déclaration de serveur MCP. Le travail est fait par [`@agenteca/mcp`](https://github.com/agenteca/agenteca-mcp), qui appelle la CLI `ahub`.

> État : 0.1.0. Le plugin s'installe depuis ce dépôt, mais `@agenteca/mcp` n'est pas encore sur npm : tant que ce n'est pas le cas, le serveur MCP qu'il déclare ne démarrera pas et `/hub` ne pourra s'appuyer que sur la commande `ahub`.

## Installer

Dans Claude Code :

```
/plugin marketplace add agenteca/agenteca-claude-code
```

```
/plugin install agenteca@agenteca
```

## Utiliser

| Commande | Effet |
|---|---|
| `/hub search <mots>` | Cherche dans le catalogue |
| `/hub info <paquet>` | Montre le contenu d'un paquet avant installation |
| `/hub install <paquet>` | Installe, après affichage du plan et accord |
| `/hub update [paquet]` | Met à jour |
| `/hub remove <paquet>` | Retire le paquet et ses fichiers |
| `/hub list`, `/hub outdated` | Paquets installés, mises à jour disponibles |

Le skill s'appelle `hub` dans le plugin `agenteca` : son nom complet est `/agenteca:hub`. La forme courte `/hub` fonctionne tant qu'aucune autre commande ne porte ce nom.

Toute installation se fait en deux temps : le plan d'abord (fichiers, hooks, serveurs MCP, scan de sécurité), l'application ensuite, après votre accord. Un paquet dont le scan relève un problème critique ne peut pas être installé depuis l'agent.

## Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `.claude-plugin/plugin.json` | Manifeste du plugin |
| `.claude-plugin/marketplace.json` | Marketplace à un plugin, pour l'installation directe depuis ce dépôt |
| `skills/hub/SKILL.md` | Le skill `/hub` |
| `.mcp.json` | Déclaration du serveur MCP |

## Vérifié, non vérifié

- Vérifié : `claude plugin validate .` passe (un avertissement : pas d'icône, facultative) ; `scripts/validate.mjs` passe.
- Non vérifié : l'installation réelle par `/plugin marketplace add` (le dépôt n'est pas publié) et l'exécution de `/hub` dans une session.

## Développement

```bash
node scripts/validate.mjs
```

## Licence

Apache-2.0.
