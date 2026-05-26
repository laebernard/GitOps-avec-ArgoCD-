---
title: "TP 2 — Rapport`"
---

# Etape 0 - Outillage

kubectl version --client
Client Version: v1.34.1
Kustomize Version: v5.7.1

kind --version
kind version 0.30.0

helm version --short
v3.21.0+ge0878d4

argocd version --client
argocd: v3.4.2+0dc6b1b

git --version
git version 2.53.

yq --version
yq (https://github.com/mikefarah/yq/) version v4.53.2

make tools-check
tous les outils sont présents.
  docker  : 29.1.3
  helm    : v3.21.0+ge0878d4
  kind v0.30.0 go1.25.0 linux/amd64
  argocd: v3.4.2+0dc6b1b

# Etape 1 — Comprendre GitOps avant d’écrire la moindre ligne

2.

| Question | *Push* (`kubectl apply` en CI) | *Pull* (ArgoCD) |
|---|---|---|
| Qui a les droits sur le cluster ? | La CI (GitLab CI, GitHub Actions, Jenkins) | agent GitOps (ArgoCD / Flux) dans le cluster |
| Où est l'historique des changements ? | CI logs | Git |
| Que se passe-t-il si un dev modifie le cluster à la main ? | Peut écraser ou créer des dérives non détectées | Le contrôleur corrige automatiquement |
| Comment ajouter un environnement de plus ? | Ajouter une nouvelle pipeline | Ajouter un nouveau dossier/overlay Git |
| Comment faire un rollback ? | Re-run pipeline | Revert commit Git → sync automatique |
| Combien de pipelines pour 30 services ? | Souvent 30 pipelines ou plus | 1 ou quelques agents centralisés |
| Qui voit *en direct* ce qui tourne ? | CI logs | Git |