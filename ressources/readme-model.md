# **Rapport de Projet \- PoketraFinday**

## **Examen Final Machine Learning & Data Science**

Réalisé au sein de ISPM - Madagascar (www.ispm-edu.com)

### **1\. Informations sur le Groupe**

Liste de tous les membres de l'équipe ayant participé au Hackathon.

#### Membre 1 :
* nom : ANDRIANANDRAINA
* prénom(s) : Anja Fanirintsoa Mathieu
* classe : ISAIA 5
* numéro : 02
* rôle : Analyse des données

#### Membre 2 : 
* nom : HARIMALALA
* prénom(s) : Mendrika Henintsoa
* classe : IGGLIA 5
* numéro : 06
* rôle :  Baseline Model (Régression Logistique) et Analyse des fraudes

#### Membre 3 :
* nom : ANDRIAMANANA
* prénom(s) : Aina Sariaka
* classe : IGGLIA 5
* numéro : 09
* rôle : Modèles Avancés et optimisation

#### Membre 4 : 
* nom : ANDRIANTSOA
* prénom(s) : Safidy Herinirina Arindranto
* classe : IGGLIA 5
* numéro : 19
* rôle : Feature Engineering

#### Membre 5 : 
* nom : RAKOTOARISOA
* prénom(s) : Finaritra Onintsoa
* classe : ISAIA 5
* numéro : 06
* rôle : Responsable EDA

#### Membre 6 : 
* nom : ANDRIANIRINASOA
* prénom(s) : Tsiky Ny Aina
* classe : IGGLIA 5
* numéro : 20
* rôle : Responsable prétraitement des données

### **2\. Résumé du Travail**

**Problématique :** 
PoketraFinday fait face à une recrudescence de fraudes sur son service, comme les vols de comptes nocturnes et ingénierie sociale ciblant les seniors. Ces fraudes fragilisent la confiance des utilisateurs et peuvent entraîner des pertes financières importantes. Il est donc critique de détecter rapidement les transactions suspectes afin de protéger les clients et la réputation de la plateforme.  
**Méthodologie Adoptée :**  
L'approche se concentre sur la maximisation du F1-Score pour la détection de fraude dans un contexte de données très déséquilibrées.
* EDA : Identification d'un fort déséquilibre des données et corrélation majeure avec le type de transaction (CASH_OUT et TRANSFERT).
* Feature Engineering : Création de features temporelles (heure, jour) et transformation logarithmique de la variable amount.
* Modèles & Déséquilibre :
    - Baseline : Régression Logistique avec class\_weight='balanced' et validation stratifiée.
    - Avancé : Random Forest entraîné après application de SMOTE pour rééquilibrer les données d'entraînement et améliorer le rappel.

L'objectif est d'atteindre un F1-Score élevé (visé : $\approx 0.85$ à $0.92$) en utilisant des techniques robustes pour gérer les classes minoritaires.

**Résultats Obtenus :**  
En se basant sur la puissance du Random Forest combinée à la gestion du déséquilibre par SMOTE, le meilleur F1-Score sur le jeu de validation serait dans la fourchette de 0.85 à 0.92.

**Mots-clés :**  
* Imbalanced Data (Déséquilibre des données)
* F1-Score
* Feature Engineering (Ingénierie de fonctionnalités)
* SMOTE (Synthetic Minority Over-sampling Technique)
* Détection de Fraude

### **3\. Contenu du Repository**

Voici la liste des fichiers et liens importants pour évaluer notre travail :

* **PoketraFinday-Mirada.ipynb** : Le code complet (EDA, Preprocessing, Modélisation) avec commentaires.  
* **submission.csv** : Nos prédictions sur le fichier test.csv.  
* **readme.md** : Ce présent rapport.  

**🔗 Liens Utiles :**

* [**LIEN VERS LA VIDÉO DE PRÉSENTATION** (Google Drive / YouTube)](https://www.youtube.com/)  
* [Lien vers d'autres ressources (Optionnel)](https://www.google.com/)

### **4\. Réponses aux Questions d'Analyse**

**Q1. Pourquoi on utilise F1-Score au lieu de accuracy ?**

L’accuracy mesure le pourcentage de bonnes prédictions, mais dans notre dataset, les fraudes sont très rares par exemple 6% pour les transferts. Si on prédit systématiquement “pas de fraude”, l’accuracy serait très élevée (>90%) mais le modèle ne détecterait aucune fraude. Le F1-score combine précision et rappel, ce qui permet de mesurer correctement la performance du modèle pour détecter les fraudes tout en limitant les fausses alertes.

**Q2. Qu'est ce qui est plus grave ici, les Faux Positifs ou les Faux Négatifs ?**

Les faux négatifs (FN) correspondent aux fraudes qui ne sont pas détectées par le modèle. Cela peut entraîner des pertes financières importantes et exposer la plateforme à des risques, ce qui en fait l’erreur la plus grave.
Les faux positifs (FP) se produisent lorsqu’une transaction légitime est bloquée par le modèle. Cela crée une gêne pour l’utilisateur, mais n’entraîne pas de perte financière directe.
Ainsi, il est préférable de tolérer un certain nombre de faux positifs afin d’éviter que des fraudes passent inaperçues.

**Q3. Stratégie de Modélisation : Quelles nouvelles variables (Feature Engineering) ont le plus amélioré votre modèle par rapport à la Baseline ?**

* Variables Temporelles (hour_of_day, day_of_week, is_night) : Elles ont permis de capturer les schémas de fraude qui se produisent préférentiellement à des moments spécifiques (ex: la nuit ou le week-end).
* Transformation Logarithmique du Montant (amount_log) : Cette transformation a normalisé la distribution très asymétrique des montants, rendant cette variable clé plus exploitable par les modèles.
* Encodage du Type de Transaction (type_encoded) : C'est un critère de séparation très puissant puisque les fraudes sont concentrées sur CASH_OUT et TRANSFERT.

**Q4. Enoncez tous les types de fraudes que vous avez décelé lors de votre analyse**

* Fraude sur les transferts (TRANSFER) → le type le plus risqué (~6,46% de taux de fraude).
* Fraude sur les retraits d’espèces (CASH_OUT) → moins fréquente (~0,27%).
* Fraude sur les paiements et DEBIT → très rare, mais possible.
* Fraude horaire → certaines heures de la nuit présentent un taux de fraude plus élevé.

**Q5. Selon vous, quelle décision prendre si une transaction *en cours* est détectée comme *fraude* par le modèle ?**

* Bloquer temporairement la transaction et alerter le client par SMS ou notification pour vérifier l’authenticité.
* Demander une authentification supplémentaire (ex : code OTP, confirmation via application).
* Conserver la trace pour analyse afin d’améliorer le modèle et détecter d’éventuels patterns similaires.

### **5\. Bibliographie**

* Cours Machine Learning M2
* Scikit-learn Documentation Officielle
* Pandas Documentation Officielle

