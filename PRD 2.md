AWI — GAP-CLOSURE & PRODUCTION ENGINEERING SPECIFICATION

0. ABSOLUTE DATA INTEGRITY RULE

NON-NEGOTIABLE:

DO NOT CREATE MOCK DATA.
DO NOT CREATE FAKE DATA.
DO NOT CREATE DUMMY RECORDS.
DO NOT INVENT PEOPLE.
DO NOT INVENT WEBSITES.
DO NOT INVENT STUDIOS.
DO NOT INVENT VIDEO COUNTS.
DO NOT INVENT RELATIONSHIPS.
DO NOT INVENT STATISTICS.
DO NOT INVENT API RESPONSES.
DO NOT INVENT SOURCE RESULTS.
DO NOT INVENT CRAWL RESULTS.
DO NOT INVENT BUSINESS LOGIC.

DO NOT USE PLACEHOLDER RECORDS THAT CAN ENTER PRODUCTION.

DO NOT PRESENT SYNTHETIC DATA AS REAL DATA.

DO NOT MAKE UP MISSING VALUES.

If information is unavailable, use a controlled state:

UNKNOWN
NOT_AVAILABLE
NOT_DISCLOSED
NOT_FOUND
NOT_VERIFIED
CONFLICTING
NOT_APPLICABLE

Every production record must originate from:
1. A real permitted source,
2. A real API response,
3. A real permitted crawl,
4. A real imported dataset,
5. A real manually verified source.

Every record must retain provenance.

For automated testing, use isolated fixtures under something like:

/tests/fixtures/

and enforce:

TEST DATA ≠ PRODUCTION DATA

with automated safeguards preventing fixture data from entering production.


---

1. PROGRAMMING LANGUAGE STRATEGY

I agree with your basic direction, but using many languages simply because they are powerful is not automatically better.

Too many languages create:

maintenance burden

security surface

duplicated libraries

developer complexity

harder CI/CD

harder onboarding

more dependency vulnerabilities


The right approach is polyglot where each language has a clear job.

Recommended stack

Python — Intelligence/Data/Research Layer

Use Python for:

data science

ETL/ELT

metadata processing

NLP

entity resolution

data validation

analytical pipelines

report generation

dataset processing

ML experimentation

research tooling


Recommended:

Python
FastAPI
Pydantic
SQLAlchemy
Polars
DuckDB
PyArrow
BeautifulSoup
lxml
httpx


---

TypeScript — Web/API/Product Layer

Use TypeScript for:

frontend

dashboard

administrative UI

search interface

API gateway/BFF where useful

realtime UI

visualization

browser-side validation


Recommended:

TypeScript
React
Next.js
Tailwind CSS
TanStack Query
Zod
ECharts / Apache ECharts


---

Rust — Security/Performance-Critical Infrastructure

Use Rust for components where performance and safety genuinely matter:

high-performance URL normalization

parser components

hashing

deduplication

crawling primitives

security-sensitive processing

high-throughput data transformation

CPU-intensive pipelines

specialized indexing components


Recommended:

Rust
Tokio
Axum
Serde
Reqwest
Rayon
SQLx

Don't rewrite the entire platform in Rust merely for marketing. Use it where it provides measurable benefit.


---

Go — Distributed Infrastructure

Go is excellent for:

workers

schedulers

queue consumers

service daemons

crawler orchestration

monitoring agents

high-concurrency network services

lightweight microservices


Use Go when the component needs:

high concurrency
low memory overhead
simple deployment
long-running services

Don't duplicate Python/Rust functionality unnecessarily.


---

Bash/Shell — Operations

Use Bash for:

deployment scripts

local setup

CI helpers

backups

migrations

environment checks

Termux utilities

operational automation


Keep shell scripts small and auditable.


---

SQL — Core Data Layer

SQL should be treated as a first-class language.

Use PostgreSQL for:

transactional data

relational entities

constraints

relationships

provenance

audit logs

permissions


Use advanced:

CTEs
window functions
indexes
materialized views
partitioning
JSONB
full-text search
constraints
triggers where justified


---

Optional languages

Only introduce these if a measurable requirement appears:

Language	Appropriate use

C/C++	Existing high-performance/native libraries
Zig	Specialized low-level tooling
Lua	Embedded scripting/plugin engine
Java	Enterprise integrations if required
Kotlin	Android companion application
WebAssembly	Browser-side CPU-heavy processing
R	Specialized statistical research
Julia	Numerical/scientific workloads


Do not add all of them just to make the project look advanced.


---

2. RECOMMENDED ARCHITECTURE

┌────────────────────────┐
                    │       WEB CLIENT       │
                    │ TypeScript / React     │
                    └───────────┬────────────┘
                                │
                                ▼
                    ┌────────────────────────┐
                    │       API GATEWAY      │
                    │ TypeScript / FastAPI   │
                    └───────────┬────────────┘
                                │
          ┌─────────────────────┼─────────────────────┐
          ▼                     ▼                     ▼
    Search Service        Entity Service       Report Service
    TypeScript/Go          Python/Go             Python
          │                     │                     │
          └─────────────────────┼─────────────────────┘
                                ▼
                     ┌─────────────────────┐
                     │    Event / Queue    │
                     │     Kafka/NATS      │
                     └──────────┬──────────┘
                                │
             ┌──────────────────┼──────────────────┐
             ▼                  ▼                  ▼
       Crawl Workers      Parser Workers      ETL Workers
          Go/Rust          Rust/Python          Python
             │                  │                  │
             └──────────────────┼──────────────────┘
                                ▼
                     ┌─────────────────────┐
                     │     PostgreSQL      │
                     └─────────────────────┘
                                │
              ┌─────────────────┼─────────────────┐
              ▼                 ▼                 ▼
           Redis            OpenSearch        Object Storage
              │                 │                 │
              └─────────────────┼─────────────────┘
                                ▼
                       Analytics / Reports

For the first release, however, do not deploy Kafka + dozens of microservices immediately.

Start modular:

Python + TypeScript + PostgreSQL + Redis

Then introduce Rust/Go workers when actual workload justifies them.


---

3. ANTI-BOT / DEFENDER ARCHITECTURE

This section needs major clarification.

Do not build an anti-bot system whose purpose is to defeat other websites' protections.

Instead create two separate concepts.

A. Responsible crawler behavior

Detect:

429
403
503
robots denial
rate-limit headers
CAPTCHA
WAF challenge
bot detection
authentication requirement
geo restriction
access denial

Then:

STOP
THROTTLE
BACKOFF
REVIEW

Never:

bypass CAPTCHA
rotate identities to evade blocking
circumvent WAF
defeat bot detection
bypass authentication
bypass paywalls
circumvent DRM
forge browser fingerprints

B. Defensive anti-abuse system for YOUR platform

Protect your own infrastructure with:

WAF

rate limiting

IP reputation

request anomaly detection

credential stuffing protection

bot detection

API abuse detection

SSRF protection

DDoS mitigation

suspicious automation detection

account takeover detection

request signatures

abuse scoring


This distinction should be explicit in the documentation.


---

4. CRAWLER INTELLIGENCE

Add:

Adaptive scheduling

Calculate:

crawl_priority =
source_value
× freshness_need
× historical_change_rate
× reliability

Don't crawl every page at the same frequency.

Example:

high-change source → frequent
low-change source → infrequent
dead source → stop
blocked source → review


---

5. CRAWL BUDGET MANAGEMENT

Every domain needs:

requests_per_minute
requests_per_hour
concurrency
bandwidth_limit
daily_budget
maximum_page_size
maximum_depth
maximum_urls

Track:

requests
bytes
errors
429
timeouts
success_rate
average_latency


---

6. CONTENT TYPE SAFETY

Before processing:

Content-Type
Content-Length
Magic bytes
File extension
Encoding
Compression

Supported safely:

HTML
JSON
XML
CSV
TSV
JSONL
RSS
Atom
WARC
WET
WAT
Parquet
ZIP
GZIP

Reject or quarantine:

executables
scripts disguised as documents
malformed archives
oversized files
archive bombs
path traversal
unexpected binary formats


---

7. EMBED EXTRACTION

Add a dedicated:

Embed Intelligence Engine

Extract only publicly exposed metadata.

Recognize:

iframe
video
source
embed
JSON-LD
VideoObject
OpenGraph video
player configuration
schema metadata

Record:

embed_id
source_page
embed_provider
embed_url
iframe_attributes
video_id
player_id
thumbnail
duration
title
metadata
observed_at

Critically:

EMBED URL ≠ OWNED MEDIA

Do not automatically mirror or download the media.


---

8. SOURCE HEALTH ENGINE

Every source should receive a health score:

SOURCE HEALTH

Availability
Freshness
Completeness
Consistency
Response quality
Schema stability
Error rate
Change frequency
Policy status

Example:

Availability: 98.2%
Freshness: HIGH
Schema stability: HIGH
Data completeness: 87%
Policy: ALLOWED
Confidence: HIGH


---

9. SCHEMA EVOLUTION

Websites constantly change their HTML.

Build:

parser_version
schema_version
source_schema_version
extraction_version
normalization_version

When a parser fails:

detect
→ alert
→ quarantine
→ investigate
→ update parser
→ regression test
→ redeploy

Never silently produce empty/incorrect records.


---

10. AUTOMATIC DATA VALIDATION

Before inserting a record:

Schema validation
↓
Type validation
↓
Required-field validation
↓
URL validation
↓
Date validation
↓
Entity validation
↓
Duplicate detection
↓
Conflict detection
↓
Provenance validation
↓
Database insertion

Invalid records go into:

quarantine_records

not directly into production.


---

11. DATA LINEAGE

This was missing and is extremely important.

Every field should support:

record
↓
field
↓
source
↓
URL
↓
timestamp
↓
collector
↓
parser version
↓
normalizer version
↓
confidence

Therefore your CEO can ask:

> Where did this number come from?



and the system can answer immediately.


---

12. REPRODUCIBILITY

Every report should store:

report_id
database_version
query
filters
time_range
source_snapshot
calculation_version
generated_at
software_version

Therefore:

Report #2026-08-19

can be regenerated later.


---

13. DATA VERSIONING

Use:

raw
normalized
verified
published

layers.

Never destroy raw evidence unnecessarily.

Recommended:

RAW
 ↓
STAGED
 ↓
NORMALIZED
 ↓
RESOLVED
 ↓
VERIFIED
 ↓
ANALYTICS
 ↓
REPORT


---

14. DATABASE CONSTRAINTS

Don't rely only on application code.

PostgreSQL should enforce:

NOT NULL
UNIQUE
FOREIGN KEY
CHECK
ENUM/domain constraints
indexes

Examples:

canonical URL unique
external source ID unique per source
entity relationship valid
confidence between 0 and 1
valid timestamps


---

15. ENTITY MERGE SAFETY

Automatic merging can destroy databases.

Implement:

AUTO-MERGE
REVIEW REQUIRED
DO NOT MERGE

with configurable confidence thresholds.

For example:

> 0.98 → automatic candidate
0.80–0.98 → human review
< 0.80 → don't merge

Those thresholds must be configurable and empirically validated—not treated as universal truth.


---

16. HUMAN-IN-THE-LOOP

A professional system should not automate everything.

Create review queues:

Entity conflicts
Possible duplicates
Suspicious sources
Parser failures
Ownership conflicts
Metadata conflicts
Policy violations
Low-confidence records

Analyst actions:

Accept
Reject
Merge
Split
Correct
Ignore
Escalate

Every action gets audited.


---

17. AUTO-UPDATE SYSTEM

Implement controlled automatic updates.

Source changed
      ↓
Detect
      ↓
Run parser
      ↓
Validate
      ↓
Compare
      ↓
Quality gate
      ↓
If PASS
      ↓
Publish

If validation fails:

DO NOT PUBLISH

Instead:

QUARANTINE
ALERT
ROLLBACK


---

18. "SELF-IMPROVEMENT" — SAFE VERSION

Do not allow the AI to autonomously rewrite production code and deploy itself.

Instead:

AI observes failures
        ↓
Identifies probable improvement
        ↓
Creates proposed patch
        ↓
Runs tests
        ↓
Security scan
        ↓
Data regression tests
        ↓
Human approval
        ↓
Canary deployment
        ↓
Monitoring
        ↓
Full deployment

This gives you AI-assisted improvement without uncontrolled self-modification.


---

19. CI/CD

Use GitHub Actions or equivalent.

Pipeline:

COMMIT
 ↓
FORMAT
 ↓
LINT
 ↓
TYPE CHECK
 ↓
UNIT TEST
 ↓
INTEGRATION TEST
 ↓
SECURITY SCAN
 ↓
DEPENDENCY SCAN
 ↓
SBOM
 ↓
BUILD
 ↓
CONTAINER SCAN
 ↓
DATABASE MIGRATION CHECK
 ↓
E2E TEST
 ↓
STAGING
 ↓
CANARY
 ↓
PRODUCTION


---

20. SECURITY TOOLCHAIN

Add:

Semgrep
Trivy
Gitleaks
OSV Scanner
cargo-audit
cargo-deny
pip-audit
npm audit
Dependabot
CodeQL
Syft
Cosign

Use them according to the language/component.

Generate an SBOM:

CycloneDX
or
SPDX

Sign production artifacts where practical.


---

21. DEPENDENCY MANAGEMENT

Pin versions.

Maintain:

lock files
dependency policy
approved licenses
vulnerability thresholds
update cadence

Automatic updates should:

create PR
run tests
run security scan
check breaking changes

Never blindly auto-upgrade production dependencies.


---

22. DISASTER RECOVERY

Add:

backup
restore
point-in-time recovery
database snapshots
object-storage replication
configuration backup
secret recovery procedure

Define:

RPO
RTO

and test restoration regularly.

A backup that has never been successfully restored is not a proven backup strategy.


---

23. OBSERVABILITY

Use:

OpenTelemetry
Prometheus
Grafana
structured logs
distributed tracing

Monitor:

CPU
RAM
disk
database
queue
crawler
HTTP
errors
latency
source health
parser health
data quality


---

24. ALERTING

Alert when:

crawler suddenly fails
source changes schema
429 rate spikes
parser output drops
duplicate rate increases
database grows unexpectedly
storage approaches limit
security vulnerability appears
API error rate rises
data quality falls


---

25. PERFORMANCE ENGINEERING

Add benchmarks for:

URL normalization
HTML parsing
JSON parsing
deduplication
entity resolution
database insertion
search
export
report generation

Use profiling before optimization.

Don't optimize based on assumptions.


---

26. CACHING

Use Redis carefully for:

source metadata
robots policies
search results
API responses
rate limits
job state

Never cache private credentials or sensitive data improperly.


---

27. SEARCH ENGINE

For serious scale:

PostgreSQL
+
OpenSearch

Use PostgreSQL as the source of truth.

Use OpenSearch for:

full text
fuzzy search
faceting
filtering
ranking
aggregations

Never make the search index the authoritative database.


---

28. ANALYTICAL ENGINE

Use:

DuckDB
Polars
Parquet

for large analytical datasets.

Avoid loading huge datasets into Python lists.

Use streaming/chunked processing.


---

29. DATA RETENTION

Define separate retention policies:

raw source data
metadata
crawl logs
audit logs
reports
exports
temporary files
failed downloads
quarantine data

Don't keep everything forever merely because storage is available.


---

30. SOURCE LICENSING

Every dataset should contain:

license
terms
attribution requirement
redistribution_allowed
commercial_use
retention_rules
source_owner

The platform must distinguish:

CAN VIEW
CAN COLLECT
CAN STORE
CAN TRANSFORM
CAN REDISTRIBUTE
CAN COMMERCIALIZE

These are not automatically equivalent.


---

31. PUBLIC DATASET INGESTION

For CSV/ZIP/JSON etc.:

discover
↓
license verification
↓
SHA-256
↓
download
↓
virus/malware scan
↓
archive validation
↓
schema detection
↓
encoding detection
↓
delimiter detection
↓
row validation
↓
deduplication
↓
normalization
↓
provenance

Record:

sha256
size
source
download timestamp
license
parser version
row count
schema


---

32. DATA QUALITY SCORE

Every entity gets:

completeness
source_count
source_agreement
freshness
verification
confidence

Then calculate an overall score.

But don't call this "truth score".

Call it:

DATA CONFIDENCE SCORE

because confidence is not proof.


---

33. GLOBAL LANGUAGE SUPPORT

Support Unicode properly.

At minimum:

UTF-8
Unicode normalization
language detection
transliteration
localized names
aliases
non-Latin scripts

Do not destroy original spelling.

Store:

original_name
normalized_name
transliterated_name

when available.


---

34. TIME/ZONES

Store timestamps in:

UTC

and retain source timezone where known.

Never confuse:

publication date
upload date
crawl date
last-modified date
database update date

These are separate concepts.


---

35. INTERNATIONALIZATION

Architecture should support:

country
region
language
locale
currency
timezone
date format

without hardcoding one country.


---

36. API GOVERNANCE

Implement:

API versioning
pagination
cursor pagination
rate limiting
authentication
authorization
request IDs
idempotency
OpenAPI
error schema
deprecation policy

Use:

/api/v1/

rather than breaking clients whenever the database changes.


---

37. EXPORT GOVERNANCE

Every export should contain:

export_id
created_at
creator
query
filters
source snapshot
database version
schema version
record count
SHA-256

This is particularly important for your CEO submission.


---

38. CEO EXECUTIVE REPORT

The final report should distinguish:

FACT

Directly supported by a source.

DERIVED

Calculated from multiple verified records.

ESTIMATE

Statistically/model-derived.

UNKNOWN

No reliable information.

CONFLICT

Sources disagree.

Never mix these categories.


---

39. NO FAKE DEMONSTRATION MODE

Add this to the project requirements:

PRODUCTION ENVIRONMENT MUST NEVER DISPLAY:

"10,000 websites"
"500,000 performers"
"1 billion videos"

unless those numbers actually exist in the production database.

No hardcoded dashboard numbers.

No fake counters.

No fabricated charts.

No fake geographic maps.

No fake source results.

No fake search results.

No fake API responses.

All dashboard numbers must be generated from the database.

If the database contains zero records:

DISPLAY ZERO.

Do not fill empty states with fabricated examples.

This is especially important because many AI coding agents generate impressive-looking dashboards full of fake data.


---

40. REAL-DATA BOOTSTRAPPING

The production bootstrap process should be:

1. Configure legitimate sources
2. Verify source access
3. Verify licenses/terms
4. Run source discovery
5. Import real data
6. Validate
7. Deduplicate
8. Resolve entities
9. Index
10. Calculate metrics
11. Generate reports

No fake seed dataset.


---

41. DEVELOPMENT ENVIRONMENTS

Use:

development
testing
staging
production

with completely separate databases.

Example:

nexus_dev
nexus_test
nexus_staging
nexus_prod

Never allow:

development → production data contamination


---

42. FEATURE FLAGS

Use feature flags for risky changes:

new_parser
new_entity_model
new_search_algorithm
new_crawler
new_taxonomy
new_report_engine

Allow controlled rollout.


---

43. CANARY DEPLOYMENT

For important crawler/parser changes:

1% sources
↓
5%
↓
25%
↓
50%
↓
100%

Monitor:

error rate
data quality
duplicate rate
missing-field rate
parser accuracy

Rollback automatically if thresholds are exceeded.


---

44. PLUGIN ARCHITECTURE

Make sources modular.

/connectors
    /commoncrawl
    /public_api
    /sitemap
    /rss
    /dataset
    /web

Each connector implements:

discover()
validate()
collect()
parse()
normalize()
health()

Then adding a new legitimate source doesn't require rewriting the platform.


---

45. TESTING REALITY

Tests should use:

real parser fixtures captured lawfully

real schema examples where redistribution/use permits

real API test endpoints

real public-format examples

controlled local test servers


But:

TEST FIXTURES MUST NEVER ENTER PRODUCTION.


---

46. FINAL TECHNOLOGY RECOMMENDATION

If I were engineering this seriously, I'd choose:

FRONTEND
TypeScript
React
Next.js

API
Python
FastAPI

DATA / ETL
Python
Polars
DuckDB

HIGH-PERFORMANCE WORKERS
Rust

DISTRIBUTED WORKERS
Go

DATABASE
PostgreSQL

SEARCH
OpenSearch

CACHE / QUEUE
Redis

EVENT STREAMING
NATS initially
Kafka only when scale justifies it

STORAGE
S3-compatible object storage

CONTAINER
Docker

ORCHESTRATION
Docker Compose initially
Kubernetes later if genuinely required

CI/CD
GitHub Actions

SECURITY
CodeQL
Semgrep
Trivy
Gitleaks
OSV Scanner
cargo-audit
cargo-deny

OBSERVABILITY
OpenTelemetry
Prometheus
Grafana

ANALYTICS
DuckDB
Polars
Parquet

DOCUMENTATION
Markdown
OpenAPI

SHELL
Bash

The important part

I would not start with Kubernetes + Kafka + Rust + Go + Python + TypeScript + OpenSearch all at once.

For a first production-capable version:

TypeScript
     +
Python
     +
PostgreSQL
     +
Redis
     +
DuckDB/Polars
     +
Bash

Then add:

Rust → performance bottlenecks
Go → high-concurrency workers
OpenSearch → search-scale bottleneck
NATS/Kafka → event-scale bottleneck
Kubernetes → infrastructure-scale bottleneck

That is more professional than choosing ten technologies upfront.


---

47. FINAL DEVELOPMENT PRINCIPLE

Add this as the final instruction to the AI coding agent:

BUILD THE REAL SYSTEM, NOT A VISUAL DEMONSTRATION.

Do not optimize for how impressive the screenshots look.

Optimize for:

DATA INTEGRITY
SECURITY
TRACEABILITY
RELIABILITY
PERFORMANCE
MAINTAINABILITY
SCALABILITY
OBSERVABILITY
LEGAL/POLICY COMPLIANCE
REPRODUCIBILITY
LONG-TERM SUPPORT

Never hide an implementation limitation behind a fake feature.

If a feature cannot currently be implemented correctly:

1. Clearly report the limitation.
2. Do not fabricate its output.
3. Implement the correct interface/contract only if useful.
4. Mark it as unavailable.
5. Document what is required to implement it properly.

Never silently replace real functionality with mock logic.

Never hardcode fake production statistics.

Never claim successful collection when collection failed.

Never claim a source was queried when it was not.

Never claim a record was verified when it was not.

Never claim global coverage when only partial coverage exists.

Every production result must be reproducible from real source data,
real processing logic and an identifiable software/data version.
