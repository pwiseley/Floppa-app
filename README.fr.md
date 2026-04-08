> 🇬🇧 [Read in English](README.md)

# floppa-project

Backend de marketplace développé en équipe dans le cadre du cours GLO-2003 Processus du génie logiciel à l'Université Laval (Hiver 2026).

L'API gère les vendeurs, produits, offres et ventes. Développé avec un accent sur les bonnes pratiques : TDD, clean code, CI/CD et flux de collaboration d'équipe réels.

> Le dépôt original du cours est privé. Ce miroir contient uniquement ce README et le diagramme d'architecture.

---

## Architecture

![Diagramme d'architecture](./floppa-architecture-diagram.png)

Trois couches strictes — aucune fuite de dépendance entre elles :

- **API** — Ressources Jersey, modèles de requête/réponse, assembleurs, exceptions, mappeurs d'exceptions. Reste mince : gestion HTTP, délégation, construction des réponses.
- **Domaine** — Logique métier, entités, services, fabriques, interfaces de dépôts, exceptions. Ne dépend jamais de la persistance.
- **Infrastructure** — MongoDB via Morphia. Deux implémentations par dépôt : `InMemory` (tests) et `Mongo` (production), sélectionnées au démarrage via propriété système.

---

## Endpoints

| Méthode | Route | Description |
|---------|-------|-------------|
| `POST` | `/sellers` | Créer un vendeur |
| `GET` | `/sellers/{sellerId}` | Obtenir un vendeur avec ses produits et statistiques d'offres |
| `POST` | `/sellers/{sellerId}/products` | Créer un produit |
| `GET` | `/products/{productId}` | Obtenir un produit avec son vendeur et ses statistiques d'offres |
| `POST` | `/products/{productId}/offers` | Soumettre une offre sur un produit |
| `GET` | `/sellers/{sellerId}/offers` | Obtenir toutes les offres reçues par un vendeur |
| `GET` | `/sellers/{sellerId}/offers/stats` | Obtenir les statistiques d'offres d'un vendeur |
| `POST` | `/products/{productId}/sales` | Créer une vente à partir d'une offre |
| `PUT` | `/sellers/{sellerId}/rating` | Évaluer un vendeur |

---

## Technologies

**Backend**
- Java 21, Jersey (JAX-RS), MongoDB, Morphia

**Tests**
- JUnit 5, Mockito, Testcontainers
- Tests unitaires (Mockito) · Tests d'intégration (Testcontainers — instance MongoDB réelle)

**DevOps**
- Docker, GHCR, GitHub Actions (CI/CD)

**Pratiques**
- TDD, Clean Code, Jakarta Bean Validation
- Commits et nommage de branches conventionnels
- Révisions de PR imposées via protection de branche (CI doit passer + 1 approbation)
- GitHub Projects — issues, jalons, backlog
- `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `LICENSE` (simulation de contribution open-source)

---

## Structure du projet

```
src/
├── main/java/
│   ├── api/               # Ressources, assembleurs, modèles de requête/réponse
│   ├── domain/            # Entités, services, interfaces de dépôts
│   └── infrastructure/    # Documents Morphia, dépôts MongoDB
├── test/java/
│   ├── api/
│   ├── domain/
│   └── infrastructure/
.gitignore
Dockerfile
docker-compose.yml
README.md
```

---

## CI/CD/CS

Trois pipelines GitHub Actions :

- **CI** — s'exécute à chaque push : compilation, tests unitaires, tests d'intégration
- **CD** — s'exécute lors d'une fusion vers `main` : construction et publication de l'image Docker vers GHCR
- **CS** — s'exécute à chaque push pour détecter les vulnérabilités

---

## Mes contributions

- Conception de l'architecture trois couches (API / Domaine / Infrastructure)
- Fonctionnalité de soumission d'offre par l'acheteur
- Pipeline CI (GitHub Actions — build et tests à chaque push)
- Pipeline CD (GitHub Actions — image Docker publiée sur GHCR à la fusion)
- Pipeline CS (sécurité continue — analyse automatisée des vulnérabilités des dépendances)
- Outillage qualité de code (configuration Spotless)
- Documentation open-source (CONTRIBUTING.md, CODE_OF_CONDUCT.md, LICENSE)
- Tests unitaires (Mockito) et tests d'intégration (Testcontainers)
- Réviseur principal sur les pull requests de l'équipe

---

## Contributeurs

Projet universitaire d'équipe — GLO-2003, Université Laval.

- **[Petiton Wiseley Paul-Enzer](https://github.com/pwiseley)**
- **[Ouedraogo Aliya Imann](https://github.com/aioue8)**
- **[Dongmeza Murielle Christelle](https://github.com/muriellec)**
- **[Guerby Benoit](https://github.com/guben18)**
- **[Mamoudou Hamadou Mamoudou Hamadou](https://github.com/mamoudouhamadou)**

---

*[petiton.dev](https://petiton.dev)*
