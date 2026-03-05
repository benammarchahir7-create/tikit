# 📱 Wallet App — Guide de mise en prod iOS

## Ce qui est déjà fait dans ce projet
- ✅ Fonts bundlées localement (pas de Google CDN)
- ✅ localStorage intégré (tickets, dossiers, thème persistent)
- ✅ Safe area iOS (notch + home bar gérés)
- ✅ Scroll bounce désactivé (natif iOS)
- ✅ Config Capacitor prête

---

## Étape 1 — Télécharger les fonts (une seule fois)

Télécharge ces 6 fichiers `.woff2` et place-les dans `public/fonts/` :

| Font | URL de téléchargement |
|---|---|
| Outfit Regular | https://fonts.gstatic.com/s/outfit/v11/QGYyz_MVcBeNP4NjuGObqx1XmO1I4TC1.woff2 |
| Outfit Bold | https://fonts.gstatic.com/s/outfit/v11/QGYyz_MVcBeNP4NjuGObqx1XmO1I4TC1.woff2 |
| Space Mono Regular | https://fonts.gstatic.com/s/spacemono/v13/i7dPIFZifjKcF5UAWdDRUEZ2RFq7AwU.woff2 |
| Space Mono Bold | https://fonts.gstatic.com/s/spacemono/v13/i7dMIFZifjKcF5UAWdDRYERMRXSX6z4.woff2 |
| Courier Prime Regular | https://fonts.gstatic.com/s/courierprime/v8/u-450q2lgwslOqpF_6gQ8kELY7pMf-c.woff2 |
| Courier Prime Bold | https://fonts.gstatic.com/s/courierprime/v8/u-4k0q2lgwslOqpF_6gQ8kELawRR4-LfrtQ.woff2 |

> 💡 Astuce : tu peux aussi utiliser `npm install @fontsource/outfit @fontsource/space-mono`
> puis importer dans `src/index.js` : `import '@fontsource/outfit'`

---

## Étape 2 — Créer ton compte Apple Developer

1. Va sur https://developer.apple.com/programs/
2. Clique "Enroll"
3. Paie les 99$/an (carte bancaire)
4. Attends la validation (quelques heures à 2 jours)

---

## Étape 3 — Connecter Appflow (build cloud, sans Mac)

1. Crée un compte sur https://ionic.io/appflow
2. Crée un nouveau projet → connecte ton repo GitHub
3. Upload ce dossier sur GitHub (gratuit) via https://github.com/new
4. Dans Appflow : New Build → iOS → sélectionne ton certificat Apple
5. Lance le build → tu reçois un fichier `.ipa`

---

## Étape 4 — Soumettre sur l'App Store

1. Va sur https://appstoreconnect.apple.com
2. Crée une nouvelle app (Bundle ID : `com.tonnom.walletapp`)
3. Upload le `.ipa` via **Transporter** (app Mac gratuite) ou Appflow directement
4. Remplis les infos : description, screenshots, catégorie (Finance)
5. Soumets → review Apple 1 à 3 jours

---

## Modifier l'identifiant de l'app

Dans `capacitor.config.json`, remplace :
```
"appId": "com.tonnom.walletapp"
```
par quelque chose d'unique, ex : `com.pierre.mywallet`

---

## Questions fréquentes

**Les données persistent si je ferme l'app ?**
Oui. `localStorage` dans Capacitor/iOS = stockage natif WebKit, persistent entre les sessions.

**Puis-je changer le nom affiché sur iOS ?**
Oui, modifie `"appName": "Wallet"` dans `capacitor.config.json`.

**Mon app est-elle 100% offline ?**
Oui. Zéro appel réseau, toutes les fonts sont locales.
