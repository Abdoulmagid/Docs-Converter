# Projet Semestriel - Cloud Computing 2018

### Travail demandé :  Développer une application de conversion de documents prête à être déployée sur Cloud.

#### Fonctionnement général de l'application : 

* Un client se rend sur la page d'accueil de l'application. Il y dépose son document, choisit les conversions à réaliser parmi celles disponibles et un e-mail de contact (facultatif).
* Une fois la demande enregistrée, l'application envoie un message (facultativement : un email) confirmant que l'opération est en cours et un lien vers une page résumant le statut de chaque conversion : en attente, en cours, terminé. Pour chaque statut, il est important de
connaître le temps passé dans l'état courant.
* Lorsqu'un documet est converti, un lien est mis à disposition depuis la page de sattut permettant de le télécharger. L' utilisateur dispose alors de 5 minutes pour le télécharger après quoi le document sera supprimé.
* Quand le document a été converti, un message (facultativement : un email ) est envoyé à l'utilisateur avec le lien.7
* Pour chaque utilisateur, il est possible de réaliser seulement 2 conversions à la fois.

## Partie 1 : Architecture de l' application

L'architecture optée pour developper cette application est celle des microservices qui propose de découper une applicaton en un ensemble de services à composants multiples appelés microservices. Le choix de cette architecture est motivé par les multiples avantages que confère cette dernière, à savoir : 

* La liberté offerte au developpeur de développer et de déployer de manière indépendante
* Un microservice peut être développé par une équipe assez petite
* Le code pour différents services peut être écrit dans différentes langues (bien que de nombreux praticiens le découragent)
* Intégration facile et déploiement automatique (utilisation d'outils d'intégration continue open source tels que Jenkins, Hudson, etc.)
* Facile à comprendre et à modifier pour les développeurs, peut donc aider un nouveau membre de l'équipe à devenir productif rapidement
* Les développeurs peuvent utiliser les dernières technologies
* Le code est organisé autour des capacités commerciales 
 
Néanmoins, cette architecture, comme toute autre possède quelques inconvénients notamment :

* Le fractionnement de l'application dans les microservices est tout un art
* L'architecture entraîne généralement une consommation de mémoire accrue
* Les développeurs doivent mettre des efforts supplémentaires dans la mise en œuvre du mécanisme de communication entre les services

Ci-desous l'architecture de l'application en termes de services:

![Services Architecture](https://github.com/Abdoulmagid/Docs-Converter/blob/master/img/DocConverterArchitecture1.0.PNG)

* **Frontend:** represente le frontend de l'application, point d'interaction entre l'utilisateur et toute l'application.
* **Backend Service:** fournit une API REST pour gérer les démandes de conversion
* **Storage Service:** gère les opérations Upload, Download et Delete
* **Upload Service:** pour le chargement (Uploading) des fichiers
* **Download Service:** pour le téléchargement des fichiers
* **Delete Service:** pour la suppression de fichiers
* **Email Service:** pour l'envoi des emails

![Data Model](https://github.com/Abdoulmagid/Docs-Converter/blob/master/img/DocConverterModel1.0.PNG)
