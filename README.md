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

![Services Architecture](https://github.com/MahametH/Docs-Converter/blob/master/img/DocConverterArchitecture1.0.PNG)

* **Frontend:** represente le frontend de l'application, point d'interaction entre l'utilisateur et toute l'application.
* **Backend Service:** fournit une API REST pour gérer les démandes de conversion
* **Storage Service:** gère les opérations Upload, Download et Delete
* **Upload Service:** pour le chargement (Uploading) des fichiers
* **Download Service:** pour le téléchargement des fichiers
* **Delete Service:** pour la suppression de fichiers
* **Email Service:** pour l'envoi des emails

#### Modèle de données
 
![Data Model](https://github.com/MahametH/Docs-Converter/blob/master/img/DocConverterModel1.0.png)

#### Technologies choisies pour le developpement

**Pourquoi SpringBoot et SpringCloud constituent-ils un bon choix pour MicroServices?**

*Spring Boot* est le framework Java le plus populaire et le plus utilisé pour la création de MicroServices. De nos jours, de nombreuses entreprises préfèrent déployer leurs applications dans un environnement cloud plutôt que de prendre elles-mêmes toutes les difficultés à gérer un centre de données. Mais nous devons prendre soin des divers aspects pour rendre nos applications Cloud Native. Voilà la beauté de *Spring Cloud*.

*Spring Cloud* est essentiellement une implémentation de divers modèles de conception à suivre lors de la création d'applications Cloud natives. Au lieu de réinventer la roue, nous pouvons simplement tirer parti des différents modules de Spring Cloud et nous concentrer sur notre principal problème d’activité, au lieu de nous préoccuper des problèmes d’infrastructure.

Voici quelques-uns des modules Spring Cloud pouvant être utilisés pour résoudre les problèmes liés aux applications distribuées:

* *Spring Cloud Config Server:* Pour externaliser la configuration des applications sur un serveur de configuration central avec la possibilité de mettre à jour les valeurs de configuration sans nécessiter de redémarrage des applications. Nous pouvons utiliser *Spring Cloud Config Server* avec *git* ou *Consul* ou *ZooKeeper* en tant que référentiel de configuration.

* *Service Registry and Discovery( ou Registre de service et découverte):* Comme il peut exister de nombreux services et que nous avons besoin de la capacité d’agrandissement ou de réduction dynamique, nous avons besoin d’un mécanisme de registre de service et de découverte afin que la communication service à service ne dépende pas de noms d’hôte et de numéros de port codés en dur. *Spring Cloud* fournit une prise en charge du service de registre et de découverte basée sur *Netflix Eureka* avec une configuration minimale. Nous pouvons également utiliser *Consul* ou *ZooKeeper* pour le Service Registry and Discovery.

* *Circuit Breaker( ou Disjoncteur):* dans l'architecture à base de microservices, un service peut dépendre d'un autre service et si un service tombe en panne, les défaillances peuvent également se répercuter sur d'autres services. Spring Cloud fournit un disjoncteur basé sur *Netflix Hystrix* pour traiter ce type de problèmes.

* *Spring Cloud Data Streams:* ces jours-ci, nous avons peut-être besoin de travailler avec d'énormes volumes de flux de données utilisant *Kafka* ou *Spark*, etc. *Spring Cloud Data Streams* fournit des abstractions de niveau supérieur pour utiliser ces frameworks plus facilement.

* *Spring Cloud Security:* Certains microservices doivent être accessibles uniquement aux utilisateurs authentifiés et nous souhaiterions probablement une fonctionnalité d'authentification unique pour propager le contexte d'authentification entre les services. *Spring Cloud Security* fournit des services d'authentification utilisant *OAuth2*.

* *Distributed Tracing:* l'un des challenges avec les microservices est la capacité de déboguer les problèmes. Une simple action de l'utilisateur final peut déclencher une chaîne d'appels de microservices. Un mécanisme doit permettre de suivre les chaînes d'appels associées. Nous pouvons utiliser *Spring Cloud Sleuth* avec *Zipkin* pour suivre les invocations entre services.

* *Contract Spring Cloud:* il est fort probable que des équipes distinctes travaillent sur différents microservices. Il devrait exister un mécanisme permettant aux équipes de s’entendre sur les contrats de points de terminaison des API afin que chaque équipe puisse développer leurs API de manière indépendante. *Spring Cloud Contract* permet de créer de tels contrats et de les valider à la fois par le fournisseur de services et par le consommateur.
