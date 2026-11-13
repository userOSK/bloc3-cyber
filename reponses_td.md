# Réponses du TD - Chiffrement symétrique (AES)

## 1. QCM
1. c. la confidentialité
2. c. la même clé chiffre et déchiffre
3. b. le chiffrement est réversible (avec la clé), pas le hachage
4. b. elle ajoute une donnée aléatoire pour que deux textes identiques donnent deux chiffrés différents
5. a. pour dériver une vraie clé robuste à partir d'un mot de passe
6. b. Cipher Block Chaining (les blocs dépendent les uns des autres)
7. c. il ne peut rien lire (confidentialité assurée)

## 2. Exercice 1 - Le bon outil
* Stocker le mot de passe : Hachage | Non réversible
* Envoyer un fichier confidentiel : Chiffrement | Réversible
* Vérifier un téléchargement : Hachage | Non réversible
* Protéger des numéros de dossier : Chiffrement | Réversible

## 3. Exercice 2 - Le pingouin
1. En mode ECB, on devine parfaitement la silhouette du pingouin. La confidentialité n'est donc pas totale.
2. C'est dangereux car si deux blocs de données sont identiques en clair, ils seront chiffrés de la même façon. Un attaquant peut deviner la structure du document.
3. En mode CBC, on ne voit plus du tout le pingouin (bruit aléatoire).
4. L'IV ajoute une valeur aléatoire de départ, et le mode CBC fait en sorte que chaque bloc chiffré dépende du bloc précédent. Ainsi, une répétition dans le texte clair ne crée jamais de répétition dans le texte chiffré.

## 4. Exercice 3 - Architecture
1. Le téléphone ou l'e-mail ne sont pas sûrs (interception possible). La solution est d'utiliser un protocole d'échange de clé sécurisé comme Diffie-Hellman.
2. Le déchiffrement va s'exécuter, mais le contenu du fichier sera corrompu à l'endroit modifié. C'est très dangereux car une information médicale vitale (ex: groupe sanguin) pourrait être faussée à l'insu de Bob (AES garantit la confidentialité, mais pas l'intégrité).
3. Solution combinée : Alice doit hacher le fichier avec SHA-256 pour créer une empreinte (intégrité), puis elle chiffre le fichier et l'empreinte avec AES (confidentialité). À la réception, Bob déchiffre tout et recalcule le hachage pour vérifier que rien n'a été modifié.
