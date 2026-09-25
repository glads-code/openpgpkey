# openpgpkey.glads.fr

Web Key Directory (WKD, méthode avancée) de glads.fr : permet aux clients mail
(GnuPG, Thunderbird, Proton…) de trouver automatiquement la clé publique PGP de
contact@glads.fr (empreinte `41C6 DE51 D5AF A96D 1958 7A44 99D5 0993 F06A DCF8`).

- Servi par GitHub Pages sur `openpgpkey.glads.fr` (CNAME DNS chez Infomaniak
  vers `glads-code.github.io.`). Dépôt public par nécessité (Pages gratuit) :
  il ne contient que la clé publique.
- `.nojekyll` : sans lui, Jekyll ignorerait le dossier `.well-known`.

## Mettre à jour la clé

```bash
gpg --export --export-options export-minimal \
  --export-filter keep-uid='mbox = contact@glads.fr' \
  41C6DE51D5AFA96D19587A4499D50993F06ADCF8 \
  > .well-known/openpgpkey/glads.fr/hu/dj3498u4hyyarh35rkjfnghbjxug6b19
```

Puis vérifier :
`gpg --auto-key-locate clear,wkd --locate-external-keys contact@glads.fr`.
