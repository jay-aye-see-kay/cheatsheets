# Models
## Basic example
```python
from django.db import models

class Customer(models.Model):
    name = models.CharField(max_length=30)
    address = models.TextField()
    email = models.EmailField()
    def __str__(self):
        return self.name
```

## Available relationships

* `ForeignKey` A many-to-one relationship. Requires two positional arguments: the class to which the model is related and the `on_delete` option. Common values for `on_delete` are `CASCADE` and `SET_NULL`, `SET_NULL` requires `null=True`.

* `ManyToManyField` A many-to-many relationship. Requires a positional argument: the class to which the model is related, which works exactly the same as it does for `ForeignKey`, including recursive and lazy relationships.

## Available model field types

### IDs and keys
* __`AutoField`__ An `IntegerField` that automatically increments according to available IDs
* __`BigAutoField`__ A 64-bit integer, much like an `AutoField`
* __`BigIntegerField`__ A 64-bit integer, much like an `IntegerField`
* __`UUIDField`__ Uses Python’s `UUID` class

### Text fields and inputs
* __`CharField`__ A string field, for small strings - requires `max_length` - default form widget is `TextInput`
* __`EmailField`__ A `CharField` that checks that the value is a valid email address
* __`TextField`__ A large text field - The default form widget is `Textarea`
* __`BooleanField`__ A true/false field - default form widget is `CheckboxInput`
* __`NullBooleanField`__ Like a `BooleanField`, but allows NULL as one of the options - The default form widget is `NullBooleanSelect`

### Time and date
* __`DateField`__ A date, represented in Python by a `datetime.date` instance - The default form widget is `TextInput`, in admin with JavaScript calendar
* __`DateTimeField`__ A date and time, represented in Python by a `datetime.datetime` instance - The default form widget is single `TextInput`. in admin two separate TextInput widgets with JavaScript shortcuts
* __`TimeField`__ A time, represented in Python by a `datetime.time` instance - The default form widget is `TextInput`, in admin with JavaScript calendar
* __`DurationField`__ A field for storing periods of time - modeled in Python by `timedelta`

### Numbers
* __`DecimalField`__ A fixed-precision decimal number, represented in Python by a `Decimal` instance - requires `max_digits` and `decimal_places`  - The default form widget is `NumberInput`
* __`FloatField`__ A floating-point number represented in Python by a `float` instance - The default form widget is `NumberInput`
* __`IntegerField`__ An integer, values from -2147483648 to 2147483647 - The default form widget is `NumberInput`
* __`PositiveIntegerField`__ Like an IntegerField, but must be either positive or zero
* __`PositiveSmallIntegerField`__ Like `PositiveIntegerField`, but only allows values up to 32767
* __`SmallIntegerField`__ Like `IntegerField`, but only allows values from -32768 to 32767

### Files and uploads
* __`FileField`__ A file-upload field - optional `upload_to` and `storage`
* __`FilePathField`__ A `CharField` whose choices are limited to the filenames in a certain directory on the filesystem - requires `path` several optional args
* __`ImageField`__ Inherits all attributes and methods from `FileField`, but also validates that the uploaded object is a valid image.

### Misc
* __`BinaryField`__ A field to store raw binary data
* __`GenericIPAddressField`__ An IPv4 or IPv6 address, in string format - The default form widget is `TextInput`
* __`SlugField`__ Newspaper term, short label for something, containing only letters, numbers, underscores or hyphens (generally used for URLs)
* __`URLField`__ A `CharField` for a URL - The default form widget is `TextInput`