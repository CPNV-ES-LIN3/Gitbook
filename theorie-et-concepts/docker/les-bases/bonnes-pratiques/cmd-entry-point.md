# CMD / ENTRY POINT



## Introduction

Lors de l'écriture d'un _dockerfile,_ comment spécifie la commande à réaliser au lancement du conteneur ?

### Sources

* [Dockerfile](https://docs.docker.com/reference/dockerfile)
* [Dockerfile - Best practices - cmd](https://docs.docker.com/build/building/best-practices/#cmd)
* [Dockerfile - Best practices - entrypoint](https://docs.docker.com/reference/dockerfile#exec-form-entrypoint-example)



## Synthèse

| Instruction          | Rôle                                            | Peut être écrasée par `docker run` ? | Exécution                                     |
| -------------------- | ----------------------------------------------- | ------------------------------------ | --------------------------------------------- |
| **CMD**              | Fournit une **commande par défaut**             | Oui                                  | Est exécutée **si rien d'autre n'est fourni** |
| **ENTRYPOINT**       | Définit la **commande principale du conteneur** | Non (sauf option `--entrypoint`)     | Toujours exécutée, avec ou sans arguments     |
| **ENTRYPOINT + CMD** | Entrée + paramètres par défaut                  | CMD fournit les **arguments**        | Modèle recommandé                             |

## Exemple pratique

{% hint style="warning" %}
* **ENTRYPOINT** = programme principal
* **CMD** = arguments par défaut
{% endhint %}

* Extrait du _dockerfile_

```
ENTRYPOINT ["python3", "app.py"]
CMD ["--port", "8080"]
```

* Lancement du conteneur, en appliquant les paramètres par défaut

```
docker run monimage //lance python3 app.py --port 8080
```

* Lancement du conteneur, avec redéfinition des paramètres (override)

```
docker run monimage --port 9090 //lance python3 app.py --port 9090 (override)
```
