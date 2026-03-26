Example input:

Table: hospital_visits

- id: bigint, primary key
- patient_id: bigint, required
- hospital_id: bigint, required
- visit_time: datetime, required
- triage_level: int, nullable
- diagnosis: text, nullable
- created_at: datetime
- updated_at: datetime

Need:
1. PostgreSQL DDL
2. SQLAlchemy model
3. Pydantic schemas for FastAPI
