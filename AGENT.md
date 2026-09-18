# AGENT.md — kube-securepods (repo parent)

## Contexte

Ce repo est le **repo pere / landing** du projet Epitech "KUBE — Sailing through the Clouds", realise par l'equipe **SecurePods**. Il ne contient pas de code de deploiement : il sert de point d'entree, de documentation d'ensemble et de lien vers les deux repos fonctionnels du projet.

- Sujet officiel : "KUBE — Sailing through the Clouds" (Epitech MSc Cybersecurite & Cloud, Nancy, promotion 2027)
- Equipe : SecurePods — Deniz Ok (chef de groupe, doc + soutenance), Lounis (securite/RBAC), Claire, Yohem, Michel (code + doc liee)
- Board Jira : SEC (10 epics, 54 tickets)
- Documentation detaillee : Confluence, espace KUBE

## Repos du projet

| Repo | Role |
|---|---|
| `kube-securepods` (ce repo) | Landing / doc d'ensemble / lien vers les 2 repos ci-dessous |
| `kube-infra` | Repo GitOps infra : provisioning Ansible du cluster + manifests des outils (Traefik, ArgoCD, VictoriaMetrics, Loki, Keycloak, Sealed Secrets, cert-manager, etc.) |
| `kube-app` | Repo GitOps application : Helm chart de l'app Laravel + MySQL, overlays kustomize (staging/prod) |

## Architecture en un coup d'oeil

- Cluster Kubernetes sur AWS, 3 VMs :
  - `kube-1` : control-plane + worker, IP publique stable
  - `kube-2`, `kube-3` : workers, IP publique ephemere, IP privee VPC stable
- Provisioning : Ansible (doit permettre un teardown/rebuild complet), acces via AWS SSM (pas de SSH public par defaut)
- Stockage partage : Amazon EFS (PersistentVolumes)
- Exposition : Ingress via Traefik, NodePort, resolu via sslip.io/nip.io (pas de LB/DNS wildcard dedie)
- GitOps : ArgoCD, synchronisation depuis `kube-infra` et `kube-app`
- Identite : Keycloak (IdP self-hosted) + dex, OIDC couvrant tous les outils deployes (Grafana, Headlamp, ArgoCD, kubectl) **et** l'API Kubernetes elle-meme, avec mapping groupes OIDC -> Role/RoleBinding
- Admission control : ValidatingAdmissionPolicy (CEL)
- Secrets : Sealed Secrets
- HTTPS : cert-manager + Let's Encrypt sur tous les endpoints exposes
- Registre d'images : prive, authentifie
- Observabilite : VictoriaMetrics (monitoring) + Loki/Grafana Alloy (logging) + Grafana (dashboards) + Headlamp (dashboard K8s)

Voir `kube-infra/AGENT.md` et `kube-app/AGENT.md` pour le detail par repo.

## Ce qui va ici

- README de presentation du projet et de l'equipe
- Schemas d'architecture globale
- Liens vers les deux repos fonctionnels, vers le board Jira et l'espace Confluence
- Pas de manifests Kubernetes, pas de code applicatif ici

## Conventions

- Langue de la documentation : francais
- Commits : voir `CONTRIBUTING.md` — format `<type>(SEC-XX): <description courte>`
- Toute decision technique structurante doit etre tracee dans le Journal de decisions Confluence avant d'etre appliquee ici
