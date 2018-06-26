# `django-admin` and `manage.py`
`django-admin` and `manage.py` are basically the same program, with `django-admin` being install globally it's used to create a project, then each project has a `manage.py` that will load up any project specific settings, so this is normally used for everything else.

* Create a project `django-admin startproject mysite`
* Create an application (inside a project) `python manage.py startapp myapp`
* Start the dev server `python manage.py runserver`
* Create a super user `python manage.py createsuperuser`
* Make migrations `python manage.py makemigrations myapp`
* Run migrations `python manage.py migrate`

# Models
## Basic example
_For more details: https://docs.djangoproject.com/en/2.0/ref/models/fields/_

```python
from django.db import models

class Customer(models.Model):
    name = models.CharField(max_length=30)
    email = models.EmailField()
    def __str__(self):
        return self.name

class Order(models.Model):
    customer = models.ForeignKey(Customer, on_delete=CASCADE)
    details = ...
    def __str__(self):
        return self.id
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

## Abstract base classes
Abstract base classes are useful when you want to put some common information into a number of other models. You write your base class and put abstract=True in the Meta class. This model will then not be used to create any database table. 

Example
```python
from django.db import models

class Person(models.Model):
    name = models.CharField(max_length=100)
    age = models.PositiveIntegerField()

    class Meta:
        abstract = True

class Student(CommonInfo):
    home_group = models.CharField(max_length=5)
```

# Django API/shell
Open an interactive shell `python manage.py shell`

Example: Working with database data through models
```python
from myapp.models import Customer

# show all customers
Customer.objects.all()

# Add a customer
new_cust = Customer(name"Dave", email="dave@email.com")
new_cust.save()

# Search through customers (returns QuerySet)
Customer.objects.filter(id=1)
Customer.objects.filter(question_text__startswith='D')

# Get one customer (raises exception if not found)
Customer.objects.get(id=2)
# Or the same lookup via primary key
second_cust = Customer.objects.get(pk=2)

# Display related info for customers (Customer hasMany Orders)
second_cust.order_set.all()
# Add an order manually
second_cust.order_set.create(details="pants, hat, ...")

# Delete above order
temp_order = second_cust.order_set.filter(details__startswith="pants")
temp_order.delete()
```

# Routes
By default Django seems to pass all http verbs through routes to controllers. For a get/post only route, use a decorator as below. See also https://docs.djangoproject.com/en/2.0/topics/http/decorators/

```python
from django.views.decorators import require_POST, require_GET

@reuire_GET
def index():
    ...

@require_POST
def destroy():
    ...
```