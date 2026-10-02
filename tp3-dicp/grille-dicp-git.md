| Critère | Git le garantit ? | Preuve tirée du TP (commande + observation) | Ce qu'il faut ajouter |
| :--- | :--- | :--- | :--- |
| **Disponibilité (D)** | Oui (clones complets) | `git clone` puis restauration d'un dossier supprimé avec `rm -rf`. Chaque clone possède l'historique complet, permettant de retrouver les données perdues. | Une véritable politique de sauvegarde (un clone ne protège pas contre une suppression propagée). |
| **Intégrité (I)** | Oui (empreintes chaînées) | `git hash-object` (effet avalanche) et `git cat-file -p HEAD` (chaque commit contient l'empreinte de son parent). | Vérification de l'intégrité hors Git. |
| **Confidentialité (C)** | Non (tout en clair) | `git show HEAD:config.env` affiche le mot de passe de production en clair. Rien n'est chiffré dans l'historique. | Chiffrement symétrique des données elles-mêmes (AES) et contrôles d'accès au dépôt. |
| **Preuve (P)** | Partiellement (falsifiable) | `git commit --author="..."` permet d'attribuer un commit à une autre personne sans mot de passe. Git trace les actions, mais n'assure pas la non-répudiation. | Signature cryptographique des commits avec une clé privée (module RSA). |

**Conclusion pour le DPO :**
La phrase "les données sont versionnées dans Git" est insuffisante pour le registre de MyCallCenter. Si Git excelle pour garantir l'intégrité (hachage) et sécurise la disponibilité (clones distribués), il n'offre aucune confidentialité (tout est stocké en clair) et la traçabilité des auteurs est falsifiable. 
Il faut écrire à la place : "L'intégrité et la disponibilité des données sont assurées par le versionnement Git ; la sécurité est complétée par un chiffrement externe des secrets (confidentialité) et la signature cryptographique des commits (preuve)."