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

Problématique :  
PoketraFinday fait face à une recrudescence de fraudes sur son service, comme les vols de comptes nocturnes et ingénierie sociale ciblant les seniors. Ces fraudes fragilisent la confiance des utilisateurs et peuvent entraîner des pertes financières importantes. Il est donc critique de détecter rapidement les transactions suspectes afin de protéger les clients et la réputation de la plateforme.  
Méthodologie Adoptée :  
(Résumez votre approche technique : EDA, pré-traitement spécifique, choix des modèles, stratégie de validation).  
Résultats Obtenus :  
(Indiquez votre meilleur F1-Score sur le jeu de validation et mentionnez une découverte clé de votre analyse).  
Mots-clés :  
(Citez 5 mots-clés techniques ou métier, ex: Fraude, Imbalanced Data, XGBoost, ...)

### **3\. Contenu du Repository**

Voici la liste des fichiers et liens importants pour évaluer notre travail :

* **PoketraFinday-Mirada.ipynb** : Le code complet (EDA, Preprocessing, Modélisation) avec commentaires.  
* **submission.csv** : Nos prédictions sur le fichier test.csv.  
* **readme.md** : Ce présent rapport.  
* *(Ajoutez ici d'autres fichiers si nécessaire, ex: requirements.txt)*

**🔗 Liens Utiles :**

* [**LIEN VERS LA VIDÉO DE PRÉSENTATION** (Google Drive / YouTube)](https://www.youtube.com/)  
* [Lien vers d'autres ressources (Optionnel)](https://www.google.com/)

### **4\. Réponses aux Questions d'Analyse**

*Répondez de manière précise aux questions posées dans le sujet. Utilisez des chiffres ou des références à vos graphiques pour justifier vos réponses.*

**Q1. Pourquoi on utilise F1-Score au lieu de accuracy ?**

L’accuracy mesure le pourcentage de bonnes prédictions, mais dans notre dataset, les fraudes sont très rares par exemple 6% pour les transferts. Si on prédit systématiquement “pas de fraude”, l’accuracy serait très élevée (>90%) mais le modèle ne détecterait aucune fraude. Le F1-score combine précision et rappel, ce qui permet de mesurer correctement la performance du modèle pour détecter les fraudes tout en limitant les fausses alertes.

**Q2. Qu'est ce qui est plus grave ici, les Faux Positifs ou les Faux Négatifs ?**

Les faux négatifs (FN) correspondent aux fraudes qui ne sont pas détectées par le modèle. Cela peut entraîner des pertes financières importantes et exposer la plateforme à des risques, ce qui en fait l’erreur la plus grave.
Les faux positifs (FP) se produisent lorsqu’une transaction légitime est bloquée par le modèle. Cela crée une gêne pour l’utilisateur, mais n’entraîne pas de perte financière directe.
Ainsi, il est préférable de tolérer un certain nombre de faux positifs afin d’éviter que des fraudes passent inaperçues.

**Q3. Stratégie de Modélisation : Quelles nouvelles variables (Feature Engineering) ont le plus amélioré votre modèle par rapport à la Baseline ?**

*(Votre réponse ici)*

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
*(si vous avez des livres, liens ou articles qui vous ont servi dans ce travail)*
