# openpgpkey.glads.fr

Web Key Directory (WKD, méthode avancée) de glads.fr : permet aux clients mail
(GnuPG, Thunderbird, Proton…) de trouver automatiquement la clé publique PGP de
contact@glads.fr (empreinte `41C6 DE51 D5AF A96D 1958 7A44 99D5 0993 F06A DCF8`).

- Servi par GitHub Pages sur `openpgpkey.glads.fr` (CNAME DNS chez Infomaniak
  vers `glads-code.github.io.`). Dépôt public par nécessité (Pages gratuit) :
  il ne contient que la clé publique.
- `.nojekyll` : sans lui, Jekyll ignorerait le dossier `.well-known`.

## Sous-clés

Elles expirent le 2028-09-24 et sont renouvelées avant cette date.

| Usage | Empreinte |
|---|---|
| Signature [S] | `4739 6D7E 43F4 792C 2CF8  9E2B E33D F3F3 AAF3 0EA9` |
| Chiffrement [E] | `5928 2797 0CD8 A28E F138  0E3F 7DCB 8947 2DA6 C906` |
| Authentification [A] | `0BF1 81DF 6ABF 0EB3 C8B4  E58F 86A3 B47D 5D41 0B73` |

## Mettre à jour la clé

Après toute modification (sous-clé ajoutée, expiration prolongée…), publier
la clé publique à trois endroits : ce dépôt (commande ci-dessous), le compte
GitHub, et les serveurs de clés :

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys 41C6DE51D5AFA96D19587A4499D50993F06ADCF8
gpg --keyserver hkps://keyserver.ubuntu.com --send-keys 41C6DE51D5AFA96D19587A4499D50993F06ADCF8
```

Pour ce dépôt :

```bash
gpg --export --export-options export-minimal \
  --export-filter keep-uid='mbox = contact@glads.fr' \
  41C6DE51D5AFA96D19587A4499D50993F06ADCF8 \
  > .well-known/openpgpkey/glads.fr/hu/dj3498u4hyyarh35rkjfnghbjxug6b19
```

Puis vérifier :
`gpg --auto-key-locate clear,wkd --locate-external-keys contact@glads.fr`.
