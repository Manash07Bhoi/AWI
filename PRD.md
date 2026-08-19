PROJECT NAME:
Adult Web Intelligence & Metadata Platform

PROJECT TYPE:
Advanced professional, production-grade global adult-industry public-web intelligence,
metadata aggregation, research, entity-resolution, search, analytics and reporting platform.

MISSION:
Build a lawful, privacy-conscious, source-aware intelligence platform that discovers,
indexes, collects, normalizes, verifies, correlates and analyzes publicly accessible
adult-industry metadata from around the world.

The system must NOT attempt to "break into" websites, bypass authentication,
circumvent paywalls/access controls, defeat CAPTCHAs, evade anti-bot systems,
scrape private accounts, obtain leaked databases, collect credentials, or access
non-public/private personal information.

The system must respect applicable law, website Terms of Service, robots.txt,
rate limits, copyright restrictions, privacy requirements and source-specific
access policies.

The platform should prioritize metadata and public professional information.
Do not download or redistribute copyrighted adult videos/images unless the source
explicitly authorizes such use and the implementation has a documented lawful basis.
For embedded media, store embed/page metadata and provenance rather than copying
the underlying media.

==================================================
1. CORE PRODUCT OBJECTIVE
==================================================

Create a global knowledge platform capable of organizing:

A. Adult-industry websites
B. Studios
C. Production companies
D. Networks
E. Platforms
F. Performers
G. Directors
H. Producers
I. Writers
J. Cinematographers
K. Editors
L. Photographers
M. Public creators
N. Public channels/profiles
O. Productions
P. Scenes
Q. Public video metadata
R. Categories
S. Tags
T. Awards
U. Distributors
V. Public professional relationships
W. Public source databases
X. Historical changes
Y. Public APIs
Z. Public datasets
AA. Public CSV/JSON/XML/ZIP datasets
AB. Public sitemap/index resources
AC. Public embedded-video metadata
AD. Public structured data
AE. Search/index results
AF. Geographic and language information

The objective is NOT to claim that the database represents literally every adult
website or every video on the Internet.

Instead provide:

DISCOVERED
OBSERVED
INDEXED
VERIFIED
ESTIMATED
UNKNOWN

as separate states.

Never fabricate completeness.

==================================================
2. SOURCE DISCOVERY ENGINE
==================================================

Build a source-discovery subsystem.

Sources may include:

- Public search engines
- Public web directories
- Common Crawl
- Public APIs
- Public datasets
- Public GitHub repositories
- Public JSON/XML feeds
- Public CSV files
- Public ZIP archives
- Public sitemaps
- RSS/Atom feeds
- Schema.org/JSON-LD
- OpenGraph metadata
- Public industry databases
- Official studio websites
- Official creator pages
- Public platform pages
- Public award databases
- Public news/article pages
- Public interviews
- Public professional profiles

Create:

source_discovery_jobs
source_registry
source_types
source_permissions
source_access_policies
source_snapshots
source_reliability

Each source must have:

source_id
source_name
source_type
domain
canonical_url
country
language
operator
access_method
terms_url
privacy_url
robots_url
robots_status
allowed_collection
collection_notes
license
last_checked
confidence

==================================================
3. GLOBAL WEBSITE DISCOVERY
==================================================

Create a website discovery engine.

Discover:

- adult entertainment websites
- adult studio websites
- creator platforms
- subscription platforms
- video platforms
- scene databases
- performer databases
- studio databases
- industry news sites
- award sites
- public directory sites
- public metadata providers
- public API providers

For every discovered domain:

domain_id
domain
canonical_domain
subdomains
site_name
operator
parent_company
country
region
language
languages[]
timezone
category
subcategory
business_model
platform_type
content_model
public_catalogue
public_profiles
public_search
public_api
public_sitemap
public_feed
public_embed
status
first_seen
last_seen
last_verified
source_count
confidence_score

Do not infer ownership as fact unless supported by evidence.

==================================================
4. WEBSITE CLASSIFICATION TAXONOMY
==================================================

Build a normalized taxonomy.

TOP LEVEL:

ADULT INDUSTRY

├── Studio
├── Production Company
├── Distributor
├── Performer Platform
├── Creator Platform
├── Subscription Platform
├── Tube/Video Platform
├── Cam Platform
├── Scene Database
├── Performer Database
├── Studio Database
├── Award Database
├── News / Media
├── Search / Discovery
├── Affiliate / Directory
├── Marketplace
├── Community
├── Streaming
├── Archive
└── Other

Allow multiple classifications.

Never force a website into one category if several apply.

==================================================
5. PERFORMER ENTITY MODEL
==================================================

Create a sophisticated performer record.

Fields:

performer_id
canonical_name
stage_name
aliases[]
name_variants[]
public_profile_urls[]
official_urls[]
gender_if_publicly_self-described
professional_roles[]
birth_date_if_publicly_available
birth_year
age_calculated_at_reference_date
country_association
nationality_if_publicly_verified
languages
career_start_year
career_end_year
active_status
studio_affiliations[]
production_credits[]
directing_credits[]
producing_credits[]
writing_credits[]
photography_credits[]
awards[]
public_social_profiles[]
public_platform_profiles[]
verification_status
confidence_score
first_seen
last_seen

IMPORTANT:

Do not automatically infer:
- legal name
- home address
- private phone number
- private email
- exact current location
- family information
- medical information
- private relationships
- sexual orientation
- other sensitive personal attributes

Only store public professional information with legitimate relevance.

==================================================
6. CREATIVE-PROFESSIONAL ENTITY MODEL
==================================================

Create separate entities:

directors
producers
writers
cinematographers
editors
photographers
production_staff
distributors
studio_executives_if_publicly_documented

Each record supports:

entity_id
canonical_name
aliases
roles
credits
organizations
public_profiles
sources
verification
confidence
history

Do not assume that a person is a director/producer/writer merely because
a website displays them in an ambiguous field.

==================================================
7. STUDIO DATABASE
==================================================

Create:

studios

Fields:

studio_id
canonical_name
aliases
parent_company
country
region
founded_year_if_public
status
official_website
brands[]
subsidiaries[]
networks[]
distributors[]
production_count_observed
performer_count_observed
director_count_observed
public_catalogue_url
public_profiles_url
sources[]
confidence
first_seen
last_seen

Relationships:

studio -> production
studio -> performer
studio -> director
studio -> producer
studio -> distributor
studio -> website
studio -> brand

==================================================
8. PRODUCTION / SCENE DATABASE
==================================================

Create:

productions
scenes

Fields:

production_id
canonical_title
alternate_titles[]
release_date
release_year
runtime_if_public
studio
producer
director
writer
cinematographer
editor
performers[]
distributors[]
platforms[]
genres[]
tags[]
description
source_urls[]
external_ids[]
poster_metadata
trailer_metadata
public_video_page
embed_metadata
verification
confidence

Do NOT download copyrighted media by default.

==================================================
9. VIDEO METADATA SYSTEM
==================================================

This is a metadata collector, not a media piracy downloader.

Collect, when publicly exposed and permitted:

video_id
page_url
canonical_url
title
description
duration
release_date
upload_date
creator
channel
studio
performers
director
producer
categories
tags
thumbnail_url
poster_url
preview_url
embed_url
embed_provider
iframe_metadata
schema_org_video_object
open_graph_metadata
twitter_card_metadata
JSON_LD
source_domain
source_page
external_ids
view_count_if_public
like_count_if_public
comment_count_if_public
availability_status
last_seen

For embedded players:

Store:

embed_provider
embed_page_url
embed_url
iframe_src
iframe_title
allow_attributes
player_metadata
poster_reference
source_page
collection_timestamp

Do NOT automatically download the underlying video.

Do not bypass DRM, signed URLs, token systems, authentication or access controls.

==================================================
10. PUBLIC DATASET COLLECTOR
==================================================

Build a dataset discovery and ingestion subsystem.

Supported:

CSV
TSV
JSON
JSONL
XML
RSS
ATOM
ZIP
GZIP
TAR
WARC
WAT
WET
Parquet

Pipeline:

DISCOVER
↓
VALIDATE
↓
DOWNLOAD IF PERMITTED
↓
HASH
↓
ARCHIVE METADATA
↓
PARSE
↓
SCHEMA DETECTION
↓
NORMALIZE
↓
DEDUPLICATE
↓
ENTITY RESOLUTION
↓
DATABASE
↓
PROVENANCE

For every dataset:

dataset_id
name
source_url
publisher
license
format
size
sha256
created_date
modified_date
download_date
schema
row_count
column_count
quality_score
license_status
provenance
parser_version

ZIP files should be treated as containers.

Inspect their manifest safely.

Do not execute files from downloaded archives.

==================================================
11. COMMON CRAWL INTEGRATION
==================================================

Integrate Common Crawl as a discovery/history source.

Use:

CDX/CDXJ indexes
WARC
WAT
WET

Use Common Crawl primarily for:

- historical discovery
- URL discovery
- page metadata
- historical snapshots
- large-scale domain research

Do not blindly download entire crawls.

Use targeted queries and bulk/index methods.

Track:

crawl_id
index_id
capture_timestamp
url
status
mime_type
digest
length
offset
filename
source

==================================================
12. ROBOTS / POLICY ENGINE
==================================================

Before crawling a website:

1. Fetch robots.txt.
2. Parse according to RFC 9309.
3. Identify applicable crawler rules.
4. Check domain policy.
5. Check internal allowlist.
6. Check rate limit.
7. Check legal/access restrictions.
8. Decide:

ALLOW
DENY
REVIEW
THROTTLE

Cache robots policies.

Never treat robots.txt as permission to bypass other restrictions.

==================================================
13. CRAWLER ARCHITECTURE
==================================================

Build:

URL frontier
scheduler
robots manager
rate limiter
HTTP client
redirect handler
retry manager
content-type detector
parser router
deduplication engine
content hashing
change detector

Respect:

timeouts
maximum response size
maximum redirects
per-domain concurrency
request delays
server errors
429 responses
5xx responses

If a domain rejects automated access:

STOP.

Do not implement anti-bot bypassing.

==================================================
14. HTML EXTRACTION
==================================================

Extract:

<title>
<meta>
<link canonical>
OpenGraph
Twitter cards
JSON-LD
Schema.org
video objects
breadcrumbs
author
publisher
datePublished
dateModified
keywords
language
alternate URLs
sitemap references
RSS links
public social links

Use:

BeautifulSoup
lxml
selectolax
trafilatura where appropriate

For JavaScript-heavy sites:

Use browser automation ONLY where permitted.

Prefer static HTML/API/JSON-LD over browser automation.

==================================================
15. ENTITY RESOLUTION
==================================================

Create canonical identities.

Example:

"Jane Doe"
"Jane_Doe"
"Jane Doe Official"
"Jane D."
"J. Doe"

may represent the same person.

But never merge automatically solely because names are similar.

Use evidence:

name
aliases
source IDs
credits
studio association
profile URLs
birth information if public
career timeline
cross-source references

Create:

entity_match_candidates
entity_merge_decisions
entity_aliases
entity_conflicts

Every merge must have:

reason
evidence
confidence
review_status

==================================================
16. DEDUPLICATION
==================================================

Deduplicate:

URLs
domains
pages
videos metadata
performers
studios
productions
tags
datasets

Use:

canonical URLs
URL normalization
content hashes
SimHash
MinHash
fuzzy matching
exact external IDs
perceptual hashes ONLY for lawful metadata comparison of authorized/local media

Never use hashing to circumvent access controls.

==================================================
17. TAG NORMALIZATION
==================================================

Create:

source_tags
canonical_tags
tag_aliases
tag_relationships
tag_categories

Example:

source:
"Amateur Model"

canonical:
"AMATEUR"

Keep both values.

Never erase original source terminology.

Create a versioned taxonomy.

==================================================
18. SEARCH ENGINE
==================================================

Implement:

full-text search
exact search
fuzzy search
semantic search
field search
Boolean search
advanced filters

Examples:

name:"X"
studio:"Y"
country:"US"
year:2020..2026
tag:"X"
domain:"example.com"

Support:

AND
OR
NOT
quotes
wildcards
date ranges

Search entities, sources, productions, websites and relationships.

==================================================
19. KNOWLEDGE GRAPH
==================================================

Create graph relationships:

PERFORMER
DIRECTOR
PRODUCER
WRITER
CINEMATOGRAPHER
STUDIO
PRODUCTION
SCENE
WEBSITE
PLATFORM
CHANNEL
AWARD
TAG
COUNTRY
SOURCE

Edges:

PERFORMED_IN
DIRECTED
PRODUCED
WROTE
FILMED
EDITED
PUBLISHED_BY
DISTRIBUTED_BY
AFFILIATED_WITH
FEATURED_ON
HAS_PROFILE
HAS_ALIAS
HAS_AWARD
HAS_TAG
SAME_AS
RELATED_TO

Every edge stores:

source
confidence
created_at
observed_at
evidence_url

==================================================
20. SOURCE PROVENANCE
==================================================

This is mandatory.

Every important field should be traceable.

Example:

performer.date_of_birth

VALUE:
1990-01-01

SOURCE:
source_123

SOURCE_URL:
...

OBSERVED:
2026-08-19

CONFIDENCE:
0.91

STATUS:
VERIFIED

Never overwrite historical evidence.

==================================================
21. CONFLICT MANAGEMENT
==================================================

If sources disagree:

Create:

data_conflicts

Fields:

conflict_id
entity
field
value_a
source_a
value_b
source_b
resolution
resolution_reason
reviewer
confidence

Never silently overwrite conflicting data.

==================================================
22. CHANGE DETECTION
==================================================

Track:

website changes
performer profile changes
studio changes
production changes
tag changes
metadata changes
availability changes

Store:

before
after
timestamp
source
hash

Generate alerts:

NEW
UPDATED
REMOVED
REDIRECTED
CONFLICTING
REAPPEARED

==================================================
23. HISTORICAL DATABASE
==================================================

Maintain snapshots.

Never destroy previous records.

Example:

performer_profile_versions
website_versions
production_versions
studio_versions

Allow:

"Show what was known on 2024-01-01."

==================================================
24. ANALYTICS
==================================================

Build analytics for:

website count
studio count
performer count
production count
director count
producer count
country distribution
language distribution
category distribution
tag frequency
yearly production trends
studio activity
creator activity
platform growth
new-domain discovery
dead domains
metadata completeness
source reliability
duplicate rate
conflict rate

Do not manufacture market-share estimates.

Clearly label:

OBSERVED
ESTIMATED
CALCULATED
UNKNOWN

==================================================
25. GLOBAL GEOGRAPHIC ANALYSIS
==================================================

Store:

country
region
continent
language
timezone

Generate:

country → websites
country → studios
country → performers
country → productions
country → platforms

Do not infer a person's current physical location from IP addresses,
geolocation, social posts or unrelated evidence.

==================================================
26. PUBLIC PROFILE COLLECTION
==================================================

Store public professional profile URLs.

Supported profile types:

official website
public studio profile
public database profile
public creator profile
public platform profile
public social profile

Store:

platform
username/public handle
profile URL
verification
first_seen
last_seen

Do not collect private profiles or private account information.

==================================================
27. VIDEO COUNTING
==================================================

Never use the word TOTAL unless verified.

Store separately:

reported_video_count
indexed_video_count
observed_video_count
estimated_video_count
last_count_date

Example:

Website claims:
1,200,000 videos

Your crawler observed:
843,221 public pages

Database:
reported = 1,200,000
observed = 843,221
estimated = NULL

==================================================
28. API INTEGRATION
==================================================

Build connectors for publicly documented APIs.

Create:

api_sources
api_connectors
api_requests
api_responses
api_rate_limits

Support:

REST
GraphQL
JSON
XML

Store raw response metadata and normalized output.

Do not expose API keys in frontend code.

Use environment variables.

==================================================
29. DATABASE
==================================================

Recommended architecture:

PostgreSQL
+
Redis
+
OpenSearch
+
Object storage for permitted datasets/archives
+
DuckDB for analytical workloads

Core tables:

sources
domains
websites
subdomains
urls
pages
page_versions
datasets
dataset_files
performers
performer_aliases
directors
producers
writers
cinematographers
editors
photographers
studios
production_companies
brands
productions
scenes
videos_metadata
channels
profiles
platforms
distributors
awards
tags
tag_aliases
relationships
embeds
external_ids
crawl_jobs
crawl_requests
crawl_results
robots_policies
source_snapshots
conflicts
entity_matches
entity_merges
change_events
audit_logs
reports

==================================================
30. DATA WAREHOUSE
==================================================

For large analytics:

DuckDB / Parquet.

Create:

daily_domain_metrics
monthly_industry_metrics
studio_metrics
performer_metrics
production_metrics
source_metrics
crawl_metrics

Partition by:

date
country
source
entity type

==================================================
31. FILE EXPORT
==================================================

Support:

CSV
JSON
JSONL
XML
Parquet
XLSX
ZIP

Exports should include:

data
schema
source
collection date
version
hash
license/provenance

Never produce an export that strips provenance.

==================================================
32. CEO REPORT GENERATOR
==================================================

Generate professional reports.

Sections:

1. Executive Summary
2. Research Scope
3. Methodology
4. Global Website Landscape
5. Studio Landscape
6. Performer Landscape
7. Production Landscape
8. Director/Producer/Writer Ecosystem
9. Platform Landscape
10. Video Metadata Landscape
11. Geographic Analysis
12. Language Analysis
13. Taxonomy
14. Knowledge Graph
15. Source Analysis
16. Data Quality
17. Conflicts
18. Trends
19. Limitations
20. Compliance
21. Recommendations
22. Appendix
23. Source Register

Every statistic must have:

value
definition
time
source
calculation method

==================================================
33. DASHBOARD
==================================================

Create a modern executive UI.

Design:

dark professional interface
high information density
responsive
desktop/tablet/mobile
accessible
clear typography
professional charts
minimal unnecessary animation

Dashboard:

GLOBAL OVERVIEW
WEBSITES
STUDIOS
PERFORMERS
PRODUCTIONS
PEOPLE
PLATFORMS
TAGS
COUNTRIES
SOURCES
CRAWL OPERATIONS
DATA QUALITY
CONFLICTS
REPORTS

==================================================
34. DATA QUALITY DASHBOARD
==================================================

Show:

Completeness %
Accuracy/confidence
Duplicate rate
Conflict rate
Unknown rate
Source coverage
Last verification
Stale records
Failed crawls
Blocked domains
Broken URLs

Example:

DATA QUALITY

Completeness        91.4%
High confidence     83.2%
Conflicts            2.7%
Duplicates           1.4%
Stale records        5.9%
Unknown              6.8%

❤️NON-NEGOTIABLE:

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
