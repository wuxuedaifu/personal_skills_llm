---
name: table-def-to-models
description: Use this skill when the task involves converting a database table definition, field list, schema notes, or sample JSON into ORM models, SQL DDL, migration drafts, API request/response models, or CRUD scaffolding. Do not use it for complex query tuning, distributed database architecture, or business logic implementation unless the task is explicitly centered on schema-to-code translation.
---

# Table Definition → ORM / SQL / API Model

## Purpose

Transform database-oriented input into consistent engineering artifacts.

This skill is for tasks like:
- turning a table definition into ORM classes
- generating SQL DDL from field descriptions
- generating API request/response models from schema
- aligning DB fields, ORM fields, and API fields
- checking naming, nullability, defaults, indexes, and type consistency
- producing migration-ready drafts

## When to use

Use this skill when the user provides any of the following:
- a CREATE TABLE statement
- a table field list
- a markdown table describing columns
- JSON samples that imply a schema
- notes like "id int, name string, created_at datetime"
- requests like:
  - "generate SQLAlchemy model"
  - "generate pydantic models"
  - "create Java entity and DTO"
  - "design API model based on this table"
  - "convert this schema into ORM and DDL"

## When NOT to use

Do not use this skill when:
- the task is mainly query optimization
- the task is mainly database performance tuning
- the task is mainly sharding / partitioning / distributed architecture
- the task is mainly business logic implementation
- the task is mainly API endpoint business behavior rather than schema/model generation

## Core principles

1. Preserve meaning, not just names.
2. Keep DB / ORM / API naming aligned and explicit.
3. Surface ambiguity instead of inventing silently.
4. Prefer safe defaults and note assumptions clearly.
5. Separate persistence model from API model when appropriate.
6. Include nullability, defaults, indexes, uniqueness, and constraints whenever derivable.
7. Avoid overengineering: generate the minimum clean structure that can be extended.

## Output workflow

When this skill is used, follow this sequence:

### Step 1: Normalize the input schema

Extract:
- table name
- column names
- source types
- nullability
- primary key
- unique constraints
- foreign keys
- defaults
- index hints
- enum-like values
- timestamps / audit fields
- example payload semantics

If the input is incomplete, infer cautiously and mark assumptions.

### Step 2: Produce a schema summary

Start with a compact summary:

- table name
- purpose of the table
- key fields
- required fields
- nullable fields
- special constraints
- notable ambiguities

### Step 3: Generate target artifacts

Depending on the request, generate one or more of:

- SQL DDL
- migration draft
- ORM model
- API request model
- API response model
- DTO / entity / schema classes
- example insert payload
- example API JSON
- field mapping table

### Step 4: Highlight assumptions and risks

Always include:
- assumptions made
- possible type mismatches
- naming inconsistencies
- fields that should maybe be split or normalized
- fields that should maybe not be exposed in API
- fields that may need indexes

## Language/framework mapping rules

### If the target stack is Python
Default preferences:
- ORM: SQLAlchemy 2.x style
- API model: Pydantic v2
- Use `Mapped[...]` and `mapped_column(...)` when generating SQLAlchemy
- Separate ORM model from Pydantic schemas unless the user explicitly wants a combined pattern

### If the target stack is FastAPI
Generate:
- ORM model
- `Create` schema
- `Update` schema
- `Read` schema

Rules:
- `Create` excludes server-generated fields
- `Update` makes most fields optional
- `Read` includes DB-generated fields
- avoid exposing internal-only fields unless requested

### If the target stack is Java
Default preferences:
- JPA entity for ORM
- DTOs for request/response
- use `LocalDateTime` for timestamps unless user specifies otherwise
- use validation annotations where appropriate

### If the target stack is TypeScript
Default preferences:
- interface or zod schema depending on user request
- distinguish DB model from API contract
- use explicit optional properties for nullable fields only when semantically correct

## Field conversion guidelines

Apply these conventions unless the user specifies otherwise.

### Common DB → Python ORM mapping
- bigint / int8 → int
- int / integer → int
- smallint → int
- varchar / text / string → str
- boolean / tinyint(1) → bool
- decimal / numeric → Decimal
- float / double → float
- json / jsonb → dict[str, Any] or JSON column
- datetime / timestamp → datetime
- date → date
- uuid → UUID

### Common DB → API mapping
- internal IDs may be exposed only if appropriate
- `created_at`, `updated_at`, `deleted_at` should usually be read-only
- secret/internal fields should not appear in outward API models
- large text/blob fields may need separate detail endpoints if relevant

## Output format rules

When generating output, use the following structure unless the user asks otherwise:

1. **Schema Summary**
2. **Assumptions**
3. **Generated Artifacts**
4. **Field Mapping Notes**
5. **Potential Improvements**

If code is requested, provide production-usable code blocks.

## Quality checks

Before finalizing, verify:

- field names are consistent
- required vs optional is consistent across DB/ORM/API
- defaults are not duplicated incorrectly
- timestamp behavior is reasonable
- primary key is explicit
- unique constraints are explicit
- indexes are suggested for lookup/filter fields
- API schemas do not leak internal-only fields
- update schema is not identical to create schema unless justified

## Preferred response patterns

### Pattern A: table definition → Python backend
Produce:
- schema summary
- SQLAlchemy model
- Pydantic Create/Update/Read schemas
- optional sample FastAPI payload

### Pattern B: field list → SQL DDL
Produce:
- normalized `CREATE TABLE`
- indexes
- comments on missing constraints

### Pattern C: JSON example → API + DB draft
Produce:
- inferred DB table
- ORM model
- API request/response schema
- assumptions list

## Example instruction handling

If user says:
"Create SQLAlchemy and Pydantic models from this table"

Then:
- infer normalized types
- create SQLAlchemy 2.x model
- create Pydantic `Create`, `Update`, `Read`
- include assumptions and questionable fields

If user says:
"Turn this markdown column list into PostgreSQL DDL"

Then:
- generate `CREATE TABLE`
- infer PK/defaults if strongly implied
- flag anything that is ambiguous

## Anti-patterns to avoid

Do not:
- invent business logic
- fabricate foreign keys without evidence
- expose every DB field in response models by default
- mix create/update/read models into one unless requested
- assume all strings should be `Text`
- assume all timestamps should auto-update unless justified
