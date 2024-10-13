# Django

## How to change the name of the Model field in serializer
```python
sample_id = serializers.PrimaryKeyRelatedField(source='sample', read_only=True)
created_at = serializers.DateTimeField(read_only=True)
new_name = serializers.FieldType(source='original_field_name', read_only=True)
active_status = serializers.BooleanField(source='is_active', read_only=True)
```

If you don't set `read_only` for `PrimaryKeyRelatedField`, you need to set `queryset=Sample.objects.all()` so serializer would know where to look for 