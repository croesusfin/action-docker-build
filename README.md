# Action Docker Build

Action regroupant les quelques étapes identifiées pour _build_, _push_ & _release_ des images Docker.

Le but de cette action est de permettre l'assemblage des images Docker à travers plusieurs _repository_ afin de
faciliter la gestion de ces repos d'image (point de vue versioning) sans avoir a répéter les étapes des workflows et les
maintenir à travers plusieurs repos manuellement.

La disponnibilité des actions composites est assez récente!
https://github.blog/changelog/2021-08-25-github-actions-reduce-duplication-with-action-composition/

Pour plus de détails sur comment se lancer dans une action composite :
https://docs.github.com/en/actions/creating-actions/creating-a-composite-action

## Ce que l'action fait

- _Build_ une image Docker dans un repo donné simplement en lui passant le nom désiré de l'image
- Utilise la _cache inline_ de Docker pour ne pas refaire les couches qui n'ont pas changé
    - Voir https://github.com/docker/build-push-action/blob/master/docs/advanced/cache.md
- Prépare et popule les metadata de l'image à partir des informations du repo sur lequel elle est basée
- Gère automatiquement les tag des images dans le registry Docker lorsque poussé à partir d'un tag
    - Voir https://github.com/docker/metadata-action
  
## Comment référencer cette action dans vos workflows

Une action composite peut être apellée comme tout autre action dans le workflow

```
  - name: Docker Build Action
    uses: croesusfin/action-docker-build@v0.3.5
    with:
      gh_token: ${{ secrets.GITHUB_TOKEN}}
      img_name: "<nom de l'image>"
```

## Comment contribuer?

Comme tout bon projet sous git, il y a une PR obligatoire pour amener vos changements dans la branche main.

Pour la suite, le processus est encore manuel, il faut pousser un tag (à partir de la branche main) afin que cette
version de l'action soit visible aux GHA Runners (le v0.3.5 mentionné plus haut). Ce tag officiel doit être fait à
partir de la branche main, en ligne de commande ou par l'interface de GitHub.

## Pourquoi le repo est public?

Le guideline chez Croesus est d'avoir des repository _internal_ (visible par tous les membres de l'entreprise). Ceci
pose problème avec une action comme celle présentée ici car les GitHub Runners n'ont pas la capacité pour le moment
d'accéder au code de l'action, voir :

- https://github.com/github/roadmap/issues/74
- https://github.com/actions/runner/issues/1005
