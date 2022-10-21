# SQLAlchemy

## How to check cardinality
```python
col_name = Column(ARRAY(INT), CheckConstraint('cardinality(col_name) <= 50'))
```