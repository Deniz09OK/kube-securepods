# SecurePods — KUBE Sailing through the Clouds

Repo pere du projet Epitech "KUBE — Sailing through the Clouds", realise par l'equipe **SecurePods**.

Ce repo est le point d'entree : documentation d'ensemble, architecture globale, et liens vers les repos fonctionnels du projet. Il ne contient pas de code de deploiement.

## Equipe

Deniz Ok (chef de groupe), Lounis, Claire, Yohem, Michel — Epitech Nancy, MSc Cybersecurite & Cloud, promotion 2027.

## Repos du projet

- [kube-infra](https://github.com/Deniz09OK/kube-infra) — provisioning Ansible du cluster + manifests des outils de plateforme (Traefik, ArgoCD, VictoriaMetrics, Loki, Keycloak, Sealed Secrets, cert-manager...)
- [kube-app](https://github.com/Deniz09OK/kube-app) — Helm chart de l'application Laravel + MySQL, overlays kustomize staging/prod

## Documentation

Voir [AGENT.md](./AGENT.md) pour le contexte complet du projet et l'architecture, et [CONTRIBUTING.md](./CONTRIBUTING.md) pour la convention de commits.
