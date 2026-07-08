# licencesFFTT
# Inscription en ligne — TT Isneauville
Application Google Apps Script (backend `Code.gs` + interface `Index.html`).

## Ce que fait le programme
1. **Identité** : nom, prénom, date de naissance → calcul automatique de l'âge et de la catégorie FFTT (Mineur / Senior / V40…V90).
2. **Si mineur** : questionnaire de santé mineur FFTT n°26-10-2 reproduit à l'identique (24 questions).
   - Si **toutes les réponses sont NON** → signature électronique (joueur + représentant légal, dessinée à l'écran) → génération d'un PDF d'attestation → **dépôt automatique** dans le dossier Drive `1Drzu7ogiSy_1tlX_340SRHhOsDJQ2ZRa`.
   - Si **au moins une réponse est OUI** → le questionnaire n'est pas déposé (il est confidentiel, réservé au médecin) ; la personne est invitée à consulter un médecin et à déposer directement le **certificat médical** obtenu, dans le dossier `1G1SAk8QL8Iu1APL987mEkxPxVga3SSkM`.
3. **Si majeur** : lien direct vers la création de compte et le PPS sur `malicence.fftt.com`.
   - **Si 60 ans ou plus** : possibilité de déposer un certificat médical (changement de catégorie V60 à V90) dans le même dossier `3-Certificat médical`.
4. **Étape finale** : lien direct vers la demande de licence en ligne du club : `https://inscriptionenligne.fftt.com/club/09760374`.

Tous les fichiers déposés sont nommés `NOM_Prenom_...` automatiquement.

## Limites volontaires (sécurité / légalité)
- Le script **ne crée jamais de compte** et **ne saisit jamais d'identifiants** sur malicence.fftt.com ou le site d'inscription du club : ces démarches restent personnelles, le script fournit uniquement les liens directs.
- La règle médicale FFTT exacte (SPID / PPS, 1ère année dans la catégorie, certificat de +5 ans, cas des 90 ans...) reste gérée par les outils officiels de la FFTT ; ce script simplifie volontairement cette partie et se contente de proposer le dépôt du certificat au bon endroit.

## Déploiement (10 minutes)
1. Aller sur https://script.google.com/ avec le compte **TTfrisno@gmail.com** (propriétaire des dossiers Drive concernés).
2. Créer un nouveau projet, le nommer par ex. « Inscription TT Isneauville ».
3. Remplacer le contenu du fichier `Code.gs` par celui fourni.
4. Ajouter un fichier HTML nommé exactement `Index` et coller le contenu du fichier `Index.html` fourni (menu *Fichier > Nouveau > Fichier HTML*, nom : `Index`).
5. Vérifier les deux ID de dossier en haut de `Code.gs` (`FOLDER_ID_QUESTIONNAIRE_MINEUR`, `FOLDER_ID_CERTIFICAT_MEDICAL`) : ils sont déjà pré-remplis avec les identifiants transmis.
6. Cliquer sur **Déployer > Nouveau déploiement > Application Web**.
   - Exécuter en tant que : **Moi** (TTfrisno@gmail.com).
   - Qui a accès : **Tous** (ou restreindre au domaine si le club utilise un Google Workspace).
7. Autoriser les permissions demandées (Drive, Docs) lors du premier lancement.
8. Copier l'URL de l'application web fournie par Google : c'est le lien à partager aux familles/adhérents (à mettre par ex. sur le site du club, à côté du QR code de connexion à `malicence.fftt.com`).

## Pour aller plus loin (optionnel)
- Ajouter l'envoi d'un e-mail de confirmation à l'adhérent après dépôt (via `MailApp.sendEmail`).
- Restreindre l'accès à l'application web aux comptes du domaine du club si besoin de traçabilité.
- Ajouter une case "je certifie l'exactitude des informations" avant envoi.
