URL
/django

settings.py

  DATABASES = {
	    'default': {
		'ENGINE': 'django.db.backends.mysql', # Add 'postgresql_psycopg2', 'mysql', 'sqlite3' or 'oracle'.
		'NAME': 'aticle',                      # Or path to database file if using sqlite3.
		# The following settings are not used with sqlite3:
		'USER': 'django',
		'PASSWORD': 'django',
		'HOST': '',                      # Empty for localhost through domain sockets or '127.0.0.1' for localhost through TCP.
		'PORT': '3306',                      # Set to empty string for default.
	    }
	}

	TEMPLATE_LOADERS = (
	    '/root/django/templates'


urls.py

	urlpatterns = patterns('',
	    url(r'^hello$', 'aticle.views.hello'),


/django/hello/modes.py

	from django.db import models

	# Create your models here.
	class Article(models.Model):
	    title = models.CharField(max_length=200)
	    body = models.TextField()
	    pub_date = models.DateTimeField('data published')
	    likes = models.IntegerField()

	    def __unicode__(self):
		return self.title


/django/hello/view.py

	from django.http import HttpResponse

	def hello(request):
		name = "Jack"
		html = "<html><body>Hi %s this TEMPLATE seems to have worked!</body></html>" % name
		return HttpResponse(html)

/django/hello/view.py

<html>
<body>
	Hi {{ name }},  this TEMPLATE seems to have worked!
</html>
</html>


/django/hello/view.py

	from django.http import HttpResponse

	def hello(request):
		name = "Jack"
		html = "<html><body>Hi %s this TEMPLATE seems to have worked!</body></html>" % name
		return HttpResponse(html)


	from django.http import HttpResponse
	from django.template.loader import get_template
	from django.template import Context

	def hello(request):
		name = "Jack"
		t = get_template('hello.html')
		html = t.render(Context({'name': name}))
		return HttpResponse(html)
