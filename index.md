[about me](./about)

```python
PERSON_SETTINGS = dict(name='Maksim',
                       sirname='Danilchenko',
                       profession='Software Engineer')

with developer_mode(**PERSON_SETTINGS) as developer:
    developer.develop()
```

[Adding total count to flask-sqlalchemy query results](/170925)
