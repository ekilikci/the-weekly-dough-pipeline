## The Weekly Dough Pipeline

A weekly data pipeline for collecting, cleaning, validating, and publishing curated bread and sandwich recipe data products.

The Weekly Dough Pipeline is a hobby-baker data engineering project. It collects bread recipes and sandwich ideas from selected open/free online sources, stores the raw data, transforms it into clean and structured datasets, applies data quality checks, and publishes consumer-friendly data products.

The project is designed with Data Mesh principles in mind, using a lightweight and practical interpretation suitable for a solo portfolio project.

### Why this project exists

Bread and sandwich recipes are scattered across many online sources. For hobby bakers and small food businesses, it can be difficult to compare recipes, discover ingredient patterns, or understand which bread types work well with different sandwich ideas.

The purpose of this project is to collect trending or interesting bread and sandwich recipes from selected countries and turn them into trustworthy, reusable data products.

The initial geographic and language focus is intentionally limited to selected English and/or German-language sources, mainly from:

- United States
- United Kingdom
- Germany

This keeps the MVP focused while still allowing international recipe discovery. Future versions may expand to more countries, more languages, and more source systems.

### Target users

#### Hobby bakers:

People who bake bread at home and want inspiration for what to bake next.

Example needs:

- Discover new bread recipes
- Explore sandwich ideas
- Compare ingredients across recipes
- Find recipes by bread type
- Identify beginner-friendly recipes

#### Small food businesses:

Small cafés, bakeries, sandwich shops, or restaurants that want recipe and menu inspiration.

Example needs:

- Discover sandwich ideas
- Explore bread and filling combinations
- Identify popular recipe types
- Find ideas that could become menu items
- Compare ingredient patterns

#### Data engineering audience:

People reviewing the project from a technical perspective.

Example needs:

- Understand the pipeline architecture
- Review Airflow orchestration
- Review data modeling choices
- Review data quality checks
- Review the Data Mesh interpretation

### MVP scope

#### In scope

The first version of the project will:

- Ingest raw recipe data from 2 different open/free sources
- Collect both bread recipes and sandwich ideas
- Store ingested data in a raw layer
- Clean and standardize recipe data into a staging layer
- Create curated data products for downstream usage
- Run the pipeline once per week using Airflow
- Apply basic data quality checks
- Document the architecture and data product design
- Use free and/or open-source technologies
- Avoid collecting or storing personally identifiable information

#### Out of scope

The first version will not include:

- More than 2 source systems
- Paid APIs or paid infrastructure
- Real-time ingestion
- Advanced recommendation algorithms
- User accounts or personalization
- Frontend or mobile application
- Complex production-grade observability
- Multi-language support beyond the selected MVP sources
- Personally identifiable information

### High-level architecture

The project follows a layered data architecture.

```
Third-party recipe sources
        |
        v
Weekly Airflow DAG
        |
        v
Raw Layer
        |
        v
Staging Layer
        |
        v
Data Quality Checks
        |
        v
Data Product Layer
        |
        v
Consumers

```
