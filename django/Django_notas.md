# Anotaciones varias en Django:

## Usar el sistema de mensajes de Django:
* Importar el módulo correspondiente:

 from django.contrib import messages

* Añadimos el mensaje:
 messages.add_message(request, messages.ERROR, 'El usuario no existe.')

* Para añadir en el template y mostrar los mensajes:

{% if messages %}
<ul class="messages">
    {% for message in messages %}
    <li{% if message.tags %} class="{{ message.tags }}"{% endif %}>{{ message }}</li>
    {% endfor %}
</ul>
{% endif %}

* Mensaje y redirect:
messages.add_message(request, messages.ERROR, 'No se envió el correo')  
redirect('account')

Cuando en un formulario, hay un problema o se finaliza, es bueno, realizar una redirección a otra página para que un usuario no pueda recargar la pagina y puedan producirse errores inesperados.

* A la hora de usar e importar módulos: Para hacer referencia a uno mismo dentro de la misma aplición 

from .forms import LoginForm, UserForm, ChangePasswordForm, RemindPasswordForm
from .models import UserProfile

Con el punto, hacemos referencia al paquete en el que está las vistas o elementos a importar. De esta forma, un cambio en el nombre del módulo sería transparente a nuestra aplicación.

* Controlar si los objetos que usemos pueden no existir:
281     try:
282         profile = user.profile
283     except UserProfile.DoesNotExist:
284         profile = None



## Plantillas.
* Acostumbrarse a usar herencia de plantillas, de forma que tengamos una plantilla base donde se van definiendo estructura y bloques comunes, y en los template de las vistas solo el código correspondiente, y redefinir los bloques que sean necesario. 

{% extends "base.html" %}
{% block content %}
 
{{ error }}
 
{% endblock %}

## Formularios:

Esquema básico para el tratamientos de formularios.
   data = None
161     context = {}
162     if request.method == 'POST':
163         data = request.POST
164     form = RemindPasswordForm(data=data)
165     if form.is_valid():
166         import ipdb; ipdb.set_trace()
167         email = form.cleaned_data['email']
168         user = is_user_exit(email)
169         if user:
                form.save()
TODO: Añadir más ejemplos y tipos de formularios que podemos usar.

## Documentación:

Para generar la documentación, se necesita el paquete python-sphinx

  docutils-common docutils-doc libjs-sphinxdoc libjs-underscore
python-docutils python-jinja2 python-lxml python-pygments python-roman
  python-sphinx sphinx-common sphinx-doc

Posicionandote en el directorio:
proyectos/docs/

 make html

y el html generado lo encontrarás en (o algo parecido dependiendo del proyecto)
/docs/build/html/install.html


## Listado de ciudades españolas (y otros elementos culturales de paises.)

* A la hora de definir el modelos de datos:
from django.contrib.localflavor.es.es_provinces import PROVINCE_CHOICES

* Definimos el campo:
provincia = models.CharField(verbose_name="Provincia", max_length=20, choices=PROVINCE_CHOICES)

* Recuerda hacer un syncdb una vez definido.

Más información: https://docs.djangoproject.com/en/1.4/ref/contrib/localflavor/


