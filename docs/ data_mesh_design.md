Data Mesh Design

This document explains how The Weekly Dough Pipeline applies Data Mesh principles in a lightweight and practical way.

The project is intentionally small and maintained as a solo portfolio project, but it still follows the spirit of Data Mesh by treating data as a product, organizing datasets around domains, documenting ownership, and applying consistent quality and governance rules.

⸻

Purpose

The Weekly Dough Pipeline collects bread recipes and sandwich ideas from selected open/free online sources, cleans and standardizes the data, validates data quality, and publishes curated data products.

The Data Mesh design helps ensure that the final datasets are not just technical outputs, but useful and trustworthy products for hobby bakers, small food businesses, and technical reviewers.

⸻

Why Data Mesh for this project?

This project could be built as a simple ETL pipeline, but applying Data Mesh thinking makes it more realistic and product-oriented.

Data Mesh helps the project answer questions such as:

- Who owns this data?
- Who consumes this data?
- What problem does each dataset solve?
- How fresh should the data be?
- What quality rules must be met?
- What are the known limitations?
- Can a future user understand and trust the data product?

Even though this is a hobby project, these questions are important for building maintainable and trustworthy data systems.

⸻

Data Mesh principles used in this project

The project uses four Data Mesh principles in a simplified way:

1. Domain-oriented ownership
2. Data as a product
3. Self-serve data platform mindset
4. Lightweight federated governance

⸻

1. Domain-oriented ownership

Data Mesh encourages organizing data around business domains instead of only technical layers.

For this project, the main domains are recipe-related domains.

Bread Recipe Domain
Sandwich Idea Domain
Recipe Quality Domain

Domain overview

Domain Responsibility Main outputs
Bread Recipe Domain Collect, clean, standardize, and publish bread recipe data dp_bread_recipe_catalog
Sandwich Idea Domain Collect, clean, standardize, and publish sandwich idea data dp_sandwich_idea_catalog
Recipe Quality Domain Define and monitor quality rules across recipe datasets dp_weekly_recipe_quality_report

⸻

Bread Recipe Domain

Purpose

The Bread Recipe Domain focuses on recipes where bread is the main product.

Examples:

- Sourdough bread
- Ciabatta
- Focaccia
- Rye bread
- Bagels
- Brioche
- Flatbread
- Baguette

Responsibilities

This domain is responsible for:

- Ingesting bread recipe data from selected sources
- Preserving raw bread recipe payloads
- Cleaning and standardizing bread recipe records
- Normalizing bread-related ingredients
- Preparing the bread recipe catalog data product
- Defining bread-specific quality expectations

Main tables

raw_bread_recipes
stg_bread_recipes
dp_bread_recipe_catalog

Main data product

dp_bread_recipe_catalog

Consumers

- Hobby bakers looking for new bread recipes
- Small bakeries looking for recipe inspiration
- Portfolio reviewers evaluating the data model and pipeline design

⸻

Sandwich Idea Domain

Purpose

The Sandwich Idea Domain focuses on sandwich recipes, filling combinations, and bread-pairing ideas.

Examples:

- Grilled cheese sandwich
- Pastrami sandwich
- Chicken salad sandwich
- Falafel wrap
- Caprese sandwich
- Breakfast sandwich
- Vegetarian sandwich

Responsibilities

This domain is responsible for:

- Ingesting sandwich idea data from selected sources
- Preserving raw sandwich recipe payloads
- Cleaning and standardizing sandwich records
- Identifying fillings, spreads, and bread types where possible
- Preparing the sandwich idea catalog data product
- Defining sandwich-specific quality expectations

Main tables

raw_sandwich_recipes
stg_sandwich_recipes
dp_sandwich_idea_catalog

Main data product

dp_sandwich_idea_catalog

Consumers

- Hobby bakers who want ideas for bread usage
- Small cafés and sandwich shops looking for menu inspiration
- Portfolio reviewers evaluating domain-oriented modeling

⸻

Recipe Quality Domain

Purpose

The Recipe Quality Domain ensures that published recipe data products are fresh, complete, traceable, and reliable.

Responsibilities

This domain is responsible for:

- Defining shared quality rules
- Running validation checks during the weekly pipeline
- Identifying blocking and non-blocking quality failures
- Publishing a weekly quality report
- Helping consumers understand data trustworthiness

Main tables

dp_weekly_recipe_quality_report

Future versions may also include a dedicated quality results table such as:

dq_check_results

Main data product

dp_weekly_recipe_quality_report

Consumers

- The pipeline owner
- Hobby bakers and small businesses who need trustworthy data
- Technical reviewers evaluating data quality practices

⸻

2. Data as a product

In this project, final curated datasets are treated as products.

This means each data product should be understandable, documented, trustworthy, and useful for a specific type of consumer.

A data product should not be created only because a transformation step produced a table. It should exist because it solves a consumer problem.

⸻

Initial data products

dp_bread_recipe_catalog

A curated catalog of bread recipes.

Purpose

Help hobby bakers and small food businesses discover and compare bread recipes.

Example questions it can answer

- Which bread recipes were collected this week?
- What types of bread are available?
- Which recipes include complete ingredient data?
- Which recipes are traceable to a source URL?
- Which bread recipes look suitable for future testing?

Example consumers

- Hobby bakers
- Small bakeries
- Data portfolio reviewers

Refresh frequency

Weekly.

Possible fields

recipe_id
recipe_title
bread_type
source_name
source_url
ingredient_count
has_complete_ingredients
batch_date
ingestion_timestamp
quality_status

⸻

dp_sandwich_idea_catalog

A curated catalog of sandwich ideas and sandwich-style recipes.

Purpose

Help hobby bakers and small food businesses discover sandwich combinations and menu inspiration.

Example questions it can answer

- Which sandwich ideas were collected this week?
- Which sandwiches mention a specific bread type?
- Which sandwich ideas include source URLs?
- Which sandwich records have complete ingredient data?
- Which recipes could be tested as small café menu ideas?

Example consumers

- Hobby bakers
- Small cafés
- Sandwich shops
- Small restaurants
- Data portfolio reviewers

Refresh frequency

Weekly.

Possible fields

recipe_id
recipe_title
sandwich_type
main_bread_type
source_name
source_url
ingredient_count
has_complete_ingredients
batch_date
ingestion_timestamp
quality_status

⸻

dp_weekly_recipe_quality_report

A weekly summary of pipeline and data quality results.

Purpose

Help users understand whether the latest weekly recipe data is complete, fresh, and trustworthy.

Example questions it can answer

- Did the weekly pipeline run successfully?
- How many recipes were ingested?
- How many records failed critical checks?
- What was the data quality pass rate?
- Are the data products fresh?

Example consumers

- Pipeline owner
- Data engineering reviewers
- Future users of the recipe data products

Refresh frequency

Weekly.

Possible fields

batch_date
pipeline_run_id
source_count
raw_bread_recipe_count
raw_sandwich_recipe_count
staging_bread_recipe_count
staging_sandwich_recipe_count
critical_check_failure_count
warning_check_failure_count
data_quality_pass_rate
pipeline_status

⸻

Data product contract template

Each data product should eventually have a small contract.

# Data Product Contract: <data_product_name>

## Purpose

## Owner

## Consumers

## Refresh frequency

## Source tables

## Output table

## Schema

## Quality rules

## Known limitations

## Example use cases

⸻

3. Self-serve data platform mindset

The project should be easy to run, understand, and extend locally.

This does not mean building a large platform. It means using simple and reusable project structure, commands, documentation, and tools.

⸻

Platform principles

The project should be:

- Easy to run locally
- Free or open-source
- Well documented
- Modular by pipeline step
- Testable
- Reproducible
- Safe from PII collection

⸻

Possible technology choices

Area Possible tools
Programming language Python
Orchestration Airflow
Storage DuckDB or PostgreSQL
Transformation SQL, Python, optionally dbt
Data quality Custom Python checks, Great Expectations, or Soda Core
Local environment Docker
Version control GitHub
Project management GitHub Projects
CI/CD GitHub Actions
Documentation Markdown and Mermaid

The MVP should avoid paid services and unnecessary complexity.

⸻

Local self-serve experience

A future user or reviewer should be able to understand and run the project with commands similar to:

make setup
make test
make run-local
make quality-checks

This helps make the project feel like a real data product platform, even though it is small.

⸻

4. Lightweight federated governance

In a large organization, federated governance means that domains follow shared rules without depending on one central data team for every decision.

In this project, governance is simplified into shared conventions and documentation.

⸻

Governance areas

Naming conventions

Tables should clearly show their layer and purpose.

Examples:

raw_bread_recipes
stg_bread_recipes
dp_bread_recipe_catalog

Recommended prefixes:

Prefix Meaning
raw* Raw source-aligned tables
stg* Cleaned and standardized staging tables
dp* Consumer-facing data products
dq* Data quality result tables

⸻

Layering rules

The project uses three main layers.

Layer Purpose Example tables
Raw Store source-aligned data with minimal transformation raw_bread_recipes, raw_sandwich_recipes
Staging Clean, standardize, normalize, and deduplicate data stg_bread_recipes, stg_ingredients
Data Product Publish consumer-ready datasets dp_bread_recipe_catalog

Rules:

- Raw data should preserve source information.
- Staging data should not be directly presented as a final product.
- Data products should be documented and quality checked.
- Critical quality failures should block data product publishing.

⸻

Source metadata

All ingested records should include source metadata.

Recommended fields:

source_name
source_url
source_recipe_id
ingestion_timestamp
batch_date
payload_hash

This supports traceability and reprocessing.

⸻

No-PII rule

This project should not collect personally identifiable information.

The pipeline should avoid storing:

- User names
- Email addresses
- Private comments
- Account information
- Private profile information
- Individual user location data

The project should only store recipe-level, ingredient-level, and source-level information.

⸻

Data quality rules

Initial quality dimensions:

- Freshness
- Completeness
- Uniqueness
- Valid values
- Traceability

Example checks:

Layer Table Rule Severity
Raw raw_bread_recipes source_recipe_id must not be null Critical
Raw raw_sandwich_recipes source_recipe_id must not be null Critical
Staging stg_bread_recipes recipe_title must not be null Critical
Staging stg_sandwich_recipes recipe_title must not be null Critical
Staging stg_recipe_ingredients Recipe should have at least one ingredient Warning
Data Product dp_bread_recipe_catalog Latest weekly batch should exist Critical
Data Product dp_sandwich_idea_catalog Latest weekly batch should exist Critical

⸻

Data ownership

Since this is a solo project, the initial owner of all domains and data products is the project maintainer.

Asset Owner
Bread Recipe Domain Project maintainer
Sandwich Idea Domain Project maintainer
Recipe Quality Domain Project maintainer
dp_bread_recipe_catalog Project maintainer
dp_sandwich_idea_catalog Project maintainer
dp_weekly_recipe_quality_report Project maintainer

Future versions could split ownership if more contributors join the project.

⸻

Data product lifecycle

Each data product should move through a simple lifecycle.

Proposed
|
v
Designed
|
v
Implemented
|
v
Quality Checked
|
v
Published
|
v
Maintained

Lifecycle definitions

Status Meaning
Proposed The data product idea is documented but not designed yet
Designed Schema, consumers, and quality rules are defined
Implemented The build logic exists
Quality Checked The data product has validation rules
Published The product is available for users or analysis
Maintained The product is refreshed and monitored weekly

⸻

MVP boundaries

The MVP applies Data Mesh thinking without overengineering.

Included in MVP

- Domain-oriented documentation
- Raw, staging, and data product layers
- Initial data product names
- Basic data product contracts
- Weekly refresh definition
- Basic data quality checks
- No-PII rule
- Free/open-source technology principle

Not included in MVP

- Complex data catalog tooling
- Enterprise governance workflows
- Fine-grained access control
- Real-time streaming
- Full lineage platform
- Multiple teams or ownership groups
- Paid observability tools

⸻

Future improvements

Future versions of the Data Mesh design may include:

- Dedicated data product contract files
- Data lineage documentation
- Automated schema validation
- Data catalog generation
- More domains, such as Ingredient Intelligence or Bread Pairing
- More advanced quality scoring
- Consumer-facing dashboards
- Recommendation data products

Potential future domains:

Ingredient Intelligence Domain
Bread Pairing Domain
Recipe Trend Domain
Menu Inspiration Domain

Potential future data products:

dp_ingredient_frequency
dp_bread_sandwich_pairings
dp_recipe_trend_summary
dp_menu_inspiration_candidates

⸻

Summary

The Weekly Dough Pipeline uses Data Mesh principles to make a small hobby-baker project more structured, trustworthy, and product-oriented.

The goal is not to build an enterprise Data Mesh platform. The goal is to demonstrate clear thinking around domains, ownership, data quality, data products, and consumer value.

This makes the project useful both as a personal recipe exploration tool and as a data engineering portfolio project.
