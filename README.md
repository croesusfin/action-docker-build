# Action Docker Build

Action regroupant les quelques étapes identifiées pour _build_, _push_ & _release_ des images Docker.

Le but de cette action est de permettre l'assemblage des images Docker à travers plusieurs _repository_ afin de
faciliter la gestion de ces repos d'image (point de vue versioning) sans avoir a répéter les étapes des workflows et les
maintenir à travers plusieurs repos manuellement.

La disponnibilité des actions composites est assez récente!
https://github.blog/changelog/2021-08-25-github-actions-reduce-duplication-with-action-composition/

Pour plus de détails sur comment se lancer dans une action composite :
https://docs.github.com/en/actions/creating-actions/creating-a-composite-action

## Comment référencer cette action

Une action composite peut être apellée comme tout autre action dans le workflow

```
  - name: Docker Build Action
    uses: croesusfin/action-docker-build@v0.3.5
    with:
      gh_token: ${{ secrets.GITHUB_TOKEN}}
      img_name: "proxy.co7x"
```

## Comment contribuer?

À déterminer, il faut pousser des tags pour que l'action puisse être référencée.

## Pourquoi le repo est public?

Le guideline chez Croesus est d'avoir des repository internal (visible par tous les membres de l'entreprise). Ceci pose
problème avec une action comme celle présentée ici car les GitHub Runners n'ont pas la capacité pour le moment d'accéder
au code de l'action, voir :

- https://github.com/github/roadmap/issues/74.
- https://github.com/actions/runner/issues/1005
