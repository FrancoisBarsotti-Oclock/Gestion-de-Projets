# Challenge C104: PCA & PRA
> Continuation (Partie 4) du projet "fil rouge", à être suivi tout au long de la saison C1.
## Énoncé E4 - Consignes
Jusqu'hier nous avons créé la note de cadrage du projet, son WBS et son registre des risques.

Aujourd'hui on prépare la continuité (PC) et la reprise (PR) d’activité.

1. Définir un scénario d’incident majeur (panne totale serveur)
2. Décrire :
    * Mesures préventives
    * Procédures de reprise
    * Responsable et délai de restauration
3. Identifier les indicateurs de succès

**Livrable attendu** : mini-PRA ou PCA
#
# :books: Mini-PRA / PCA – Modernisation infrastructure IT

### Hypothèse d’architecture

* Hyperviseur (ex : cluster virtualisé ou hôte unique)
* VM Serveur principal (AD / fichiers)
* NAS de stockage + sauvegardes quotidiennes
* Firewall périmétrique
* VLAN segmentés

### Scénario d’incident majeur

**Incident** : panne totale du serveur principal (serveur fichiers / authentification).
**Cause possible** : défaillance matérielle, corruption système, ransomware.
**Conséquence** : indisponibilité des partages, arrêt des activités pédagogiques et administratives.

## :soon: Mesures techniques préventives (PCA)
🔹 **Sauvegardes quotidiennes automatisées (3-2-1)**
* Backup incrémental quotidien
* Backup complet hebdomadaire
* Copie externalisée (cloud ou site secondaire)
* Test de restauration trimestriel

🔹 **Virtualisation des serveurs**
* Snapshot avant mises à jour majeures
* Export OVF mensuel
* Possibilité redéploiement sur second hôte

🔹 **Stockage**
* RAID 5/6 sur NAS
* Onduleur (UPS) + arrêt propre automatique
* Supervision et alerting (SMART monitoring)

🔹 **Sécurité**
* Segmentation VLAN
* Comptes admin séparés
* Journalisation activée

## Mesures Organisationnelles préventives (PCA)
🔹 Organisationnelles
* Procédures écrites de reprise
* Tests de restauration semestriels
* Accès d’urgence documenté
* Formation alternant + IT

## :arrows_counterclockwise: Procédure de reprise (PRA)
### Étape 1 – Diagnostic (≤ 30 min)
*  Vérifier état hyperviseur
* Vérifier stockage NAS
* Identifier cause panne (logique ou matérielle)
* Vérifier sauvegardes disponibles

### Étape 2 – Restauration (entre 2h et 4h cible)
### Cas A : VM corrompue, hyperviseur OK
* Supprimer VM défectueuse
* Redéploiement VM sur hyperviseur
* Restauration dernière sauvegarde valide
* Vérification intégrité données
* Reconfigurer IP si nécessaire
* Démarrer services 
* Vérifier AD / DNS / SMB
Durée cible: ≤ 2h

### Cas B : Hyperviseur HS
* Réinstaller hyperviseur sur matériel disponible
* Connecter NAS
* Importer VM sauvegardée
* Vérifier cohérence VLAN
* Tests services
Durée cible: ≤ 4h

### Étape 3 – Validation (≤ 1h)
  
* Test Authentification, accès utilisateurs
* Test droits
* Test utilisateurs pilotes
* Logs propres
* Validation direction

## :beginner: Responsables & délais

| **Élément** | **Responsable** | **Responsabilité** | **Délai cible** |
| -------- | :-------: | :-------: | :-------: |
| Diagnostic | Responsable IT | Décision reprise | 30 min |
| Restauration VM | Responsable IT | Décision restauration | 2–4 h |
| Vérification données | IT + alternant | Support technique / vérifications | 1 h |
| Communication | Direction | Communication interne | immédiat |
| Matériel | Fournisseur | Support matériel si besoin | meilleur possible |

**Objectif RTO (Recovery Time Objective)** : 4 heures
**Objectif RPO (Recovery Point Objective)** : 24 heures maximum
#
### :shield: Indicateurs de succès

* ✅ Service restauré dans le délai RTO (délai respecté)
* ✅ Perte de données ≤ RPO
* ✅ Taux succès restauration = 100 %
* ✅ Temps diagnostic < 30 min 
* ✅ Accès utilisateurs fonctionnel
* ✅ Aucune faille de sécurité post-incident
* ✅ Rapport post-incident formalisé sous 48h.

### :arrow_upper_right: Amélioration continue
Après incident :
* Analyse cause racine (RCA)
* Mise à jour documentation
* Ajustement sauvegardes
* Test PRA supplémentaire

### 🎯 Synthèse stratégique

Le projet doit intégrer dès la conception :
* Redondance minimale
* Sauvegarde vérifiée
* Procédure testée

:brain: Ce qui doit être valorisé et mis en avant :
* 👉 logique de résilience
* 👉 maîtrise RTO/RPO
* 👉 tests réguliers

