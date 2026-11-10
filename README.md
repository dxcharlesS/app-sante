# 📱 MediQueue Mobile - Application Mobile de Gestion de File d'Attente

Application mobile web moderne (PWA) de file d'attente médicale interactive, conçue pour les patients, les médecins, le personnel d'accueil et les administrateurs.

---

## 🌟 Fonctionnalités Clés

### 👤 Espace Patient
- **Prise de ticket virtuel en 1 clic :** Choix du service médical (*Consultation Générale*, *Pédiatrie*, *Urgences*, *Cardiologie*, *Radiologie*) et du degré d'urgence.
- **Pass Numérique en Temps Réel :**
  - Numéro de ticket haute visibilité (ex: `A-102`).
  - Position dynamique dans la file d'attente recalculée instantanément.
  - Estimation du temps d'attente en minutes basée sur le rythme moyen des consultations.
  - Barre de progression d'avancement.
- **Appel Sonore & Vibreur :**
  - Carillon hospitalier multi-tons réaliste synthétisé via la Web Audio API (sans fichier audio externe, fonctionne 100% hors-ligne).
  - Synthèse vocale de l'annonce en français (*"Ticket A-102, veuillez vous présenter au Cabinet 1"*).
  - Retour haptique par vibration (`navigator.vibrate`).
- **Historique & Notifications :** Centre de notifications avec horodatage et alertes en direct.
- **Annulation :** Possibilité de quitter la file et d'annuler son ticket à tout moment.

### 🩺 Espace Médecin
- **Bouton d'Appel Rapide :** *"Appeler le patient suivant"* qui sélectionne automatiquement le patient prioritaire (Urgent > Normal > Non-urgent > Planifié, ordonné selon l'heure d'arrivée FIFO).
- **Cabinet Actif :** Affichage du patient en cours de consultation avec options :
  - *Démarrer la consultation*
  - *Terminer et valider*
  - *Rappeler (sonnerie)*
  - *Marquer absent*
- **File d'attente en direct :** Liste filtrable (*En attente*, *Appelés*, *Terminés*) avec indicateurs visuels et possibilité d'ajouter des patients en salle.
- **KPIs du jour :** Nombre de patients en attente, consultés et temps moyen d'attente.

### 📋 Espace Réception / Accueil
- Enregistrement rapide des patients et émission immédiate de tickets virtuels.
- Recherche instantanée par nom, numéro de ticket ou numéro de téléphone.
- Ajustement des priorités et consultation globale de la file.

### ⚡ Espace Administration
- Métriques complètes : temps moyen, plus longue attente, total des tickets de la journée.
- Répertoire complet des patients avec génération de ticket.
- Bouton de réinitialisation sécurisé pour recharger les données de démonstration.

### 🔄 Multi-onglets & Synchronisation Temps Réel
- Utilisation de `localStorage` et de `BroadcastChannel` : ouvrez deux onglets (l'un en Médecin, l'autre en Patient), lorsque le médecin clique sur *"Appeler"*, l'onglet du patient sonne et affiche instantanément l'alerte !

---

## 🚀 Démarrage Rapide

### Option 1 : Double-clic direct
Vous pouvez directement ouvrir le fichier `index.html` dans n'importe quel navigateur moderne (Chrome, Edge, Firefox, Safari).

### Option 2 : Serveur local HTTP (recommandé pour PWA)
Dans le dossier `app-sante-mobile` :
```bash
python -m http.server 8080
```
Puis accédez à `http://localhost:8080` sur votre ordinateur ou votre smartphone sur le même réseau Wi-Fi.

---

## 🔑 Comptes de Démonstration

L'application intègre un **sélecteur rapide de rôles** (bouton `⚡ Rôles` en haut à droite) permettant de basculer instantanément sans retaper les identifiants :

| Rôle | Email | Mot de passe | Description |
|---|---|---|---|
| **Patient** | `p@test.com` | `Test1234!` | Jean Dupont (Ticket actif A-102) |
| **Médecin** | `d@test.com` | `Test1234!` | Dr. Pierre Martin (Cabinet 1) |
| **Accueil** | `r@test.com` | `Test1234!` | Marie Laurent (Réceptionniste) |
| **Admin** | `a@test.com` | `Test1234!` | Sophie Dubois (Administrateur) |

---

## 📁 Structure du Code Source

```text
app-sante-mobile/
├── index.html            # Interface mobile responsive & shell smartphone
├── manifest.json         # Manifeste PWA pour installation sur écran d'accueil
├── sw.js                 # Service Worker pour le mode hors-ligne
├── css/
│   └── app.css           # Feuilles de styles modernes mobile-first
├── js/
│   ├── store.js          # Persistance LocalStorage & synchronisation multi-onglets
│   ├── audio.js          # Synthèse sonore d'appel Web Audio & vibrations
│   ├── queue.js          # Moteur de tri prioritaire (FIFO) & calculs statistiques
│   ├── auth.js           # Gestion de session, hachage & validation des mots de passe
│   ├── ui.js             # Rendu dynamique des vues mobiles & modales
│   └── app.js            # Initialisation, écouteurs d'événements & minuteurs
└── README.md             # Documentation complète
```
