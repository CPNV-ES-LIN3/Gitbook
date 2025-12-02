# Les outils de surveillance

## Introduction

Il existe plusieurs outils spécialement adaptés pour surveiller une infrastructure Docker. <mark style="color:orange;">Ces outils couvrent les métriques système, les logs et les événements en temps réel</mark>.

## Les outils

### Prometheus et Grafana

* **Prometheus** est <mark style="color:orange;">un outil de surveillance open-source qui collecte des métriques à partir de diverses sources</mark>, y compris Docker. Il utilise un modèle de **scraping** (récupération de métriques à intervalles réguliers).
* **Grafana** est souvent <mark style="color:orange;">associé à Prometheus pour la visualisation</mark> des métriques sous forme de tableaux de bord graphiques.
* Avec Docker, un **exporter cAdvisor** est généralement utilisé pour fournir des métriques détaillées sur les conteneurs Docker (CPU, mémoire, etc.).

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<p align="center">Source : <a href="https://developer.hpe.com/blog/get-started-with-prometheus-and-grafana-on-docker-with-hpe-storage-array-exporter/">developer.hpe.com</a></p>

### cAdvisor

* **cAdvisor (Container Advisor)** <mark style="color:orange;">est un outil open-source développé par Google</mark>. Il s’intègre bien avec Docker et <mark style="color:orange;">fournit des métriques détaillées</mark> sur l’utilisation des ressources des conteneurs en temps réel.
* cAdvisor s’intègre souvent à Prometheus pour stocker les métriques sur le long terme.

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<p align="center">Source : blog.devops.dev</p>

### ELK Stack (Elasticsearch, Logstash, Kibana)

* Le stack **ELK** est utilisé <mark style="color:orange;">pour la gestion et l'analyse des logs</mark>. Dans le cadre de Docker, vous pouvez configurer des agents pour centraliser les logs de vos conteneurs.
* **Filebeat** ou **Fluentd** sont souvent utilisés <mark style="color:orange;">pour collecter les logs des conteneurs</mark> et les envoyer vers **Elasticsearch** pour indexation, suivi d'une visualisation avec **Kibana.**

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<p align="center">Source :<a href="https://www.tatvasoft.com/blog/data-analytics-elasticsearch-logstash-kibana-elk/"> tatvasoft.com</a></p>

### Docker Swarm & Kubernetes Monitoring

* Si vous utilisez Docker dans <mark style="color:orange;">un cluster orchestré avec</mark> <mark style="color:orange;"></mark><mark style="color:orange;">**Docker Swarm**</mark> <mark style="color:orange;"></mark><mark style="color:orange;">ou</mark> <mark style="color:orange;"></mark><mark style="color:orange;">**Kubernetes**</mark>, il est important de surveiller l’état de vos <mark style="color:orange;">**services**</mark><mark style="color:orange;">, la</mark> <mark style="color:orange;"></mark><mark style="color:orange;">**santé des nœuds**</mark><mark style="color:orange;">, et la</mark> <mark style="color:orange;"></mark><mark style="color:orange;">**planification des conteneurs**</mark>.
* Kubernetes offre des outils natifs comme **Kube-State-Metrics**, **Metrics Server** ou encore des intégrations avec Prometheus pour <mark style="color:orange;">surveiller les pods et les nœuds du cluster</mark>.

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<p align="center">Source : <a href="https://www.quobyte.com/storage-explained/what-is-kubernetes/">quobyte.com</a></p>

### Sysdig

**Sysdig** <mark style="color:orange;">est une solution complète pour surveiller les infrastructures Docker</mark>. Il permet de surveiller à la fois les conteneurs, les applications et les performances réseau. Sysdig propose également des fonctionnalités de sécurité pour détecter des comportements anormaux.

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<p align="center">Source : <a href="https://docs.sysdig.com/en/docs/sysdig-monitor/using-monitor/">Sysdig.com</a></p>

### Datadog

**Datadog** <mark style="color:orange;">est une solution de monitoring SaaS (Software-as-a-Service)</mark> qui offre des intégrations avec Docker. Il fournit une vue d'ensemble des performances des conteneurs, des métriques réseau, des logs, et propose également une solution pour les alertes en temps réel.

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<p align="center">Source : <a href="https://www.gremlin.com/community/tutorials/chaos-engineering-on-docker-swarm-with-gremlin-and-datadog">gremlin.com</a></p>
