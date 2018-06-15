## Posts

[about me](./about)

```python
PERSON_SETTINGS = dict(name='Maksim',
                       sirname='Danilchenko',
                       age=23,
                       profession='Software Engineer')

with developer_mode(**PERSON_SETTINGS) as developer:
    developer.develop()
```
