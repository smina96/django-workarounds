# django-workarounds

## Translation with django parler  
useful article aside from the documentation guide of the package [link](https://phrase.com/blog/posts/website-i18n-with-django-rest-framework-and-django-parler/)
### workarounds  : 
Before you migrate the translation migration generated :
* change  manually in the translation migration of your Model 's  bases to only models.Model :
add to the migration operations:
``` 
def fix_bases(apps, schema_editor): 
    list_models = [apps.get_model("module", "Model"),  ]
    for MyModel in list_models:
      MyModel.__bases__ = (models.Model,)
```
    migrations.RunPython(fix_bases) 

* comment the lines :   bases=(parler.models.TranslatedFieldsModelMixin, models.Model), 

### Integration of django-parler with django rest :
use  django-parler-rest
* Use the mixin TranslatedSerializerMixin (https://github.com/django-parler/django-parler-rest/issues/26#issuecomment-666798305)  in your serializer
* Remember to send request on serializer's context  so that it can retrieve language from the header


----
Happy translating !
