## Check Constraints

```sql
SELECT CONSTRAINT_NAME, CHECK_CLAUSE
FROM INFORMATION_SCHEMA.CHECK_CONSTRAINTS
WHERE CONSTRAINT_NAME = 'doctor_chk_1';

```

```sql
SHOW CREATE TABLE doctor;
```
