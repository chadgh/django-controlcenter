Welcome to django-controlcenter!
================================

Get all your project models on one single page with charts and whistles.

.. image:: https://cloud.githubusercontent.com/assets/1560043/14309295/b8c9aad0-fc05-11e5-96d0-44293d2d07ff.png
    :alt: django-controlcenter


Rationale
---------

Django-admin_ is a great tool to control your project activity: new orders, comments, replies, users, feedback -- everything is here. The only struggle is to switch between all that pages constantly just to check them out for new entries.

With django-controlcenter you can have all your models on one single page and build beautiful charts with Chartist.js_. Actually they don't even have to be a django model, get your data from wherever you want: RDBMS, NOSQL, text file or even from an external web-page, it doesn't matter.


Quickstart
----------

Install django-controlcenter:

.. code-block:: console

    pip install -U django-controlcenter

Create a dashboard file with unlimited number of widgets and dashboards:

.. code-block:: python

    from controlcenter import Dashboard, widgets
    from project.app.models import Model

    class ModelItemList(widgets.ItemList):
        model = Model
        list_display = ('pk', 'field')

    class MyDashboard(Dashboard):
        widgets = (
            ModelItemList,
        )

Update settings file:

.. code-block:: python

    INSTALLED_APPS = [
        ...
        'controlcenter',
        ...
    ]

    CONTROLCENTER_DASHBOARDS = (
        'project.dashboards.MyDashboard',
    )

Plug in urls:

.. code-block:: python

    from django.conf.urls import url
    from django.contrib import admin
    from controlcenter.views import controlcenter

    urlpatterns = [
        url(r'^admin/', admin.site.urls),
        url(r'^admin/dashboard/', controlcenter.urls),
        ...
    ]

Open ``/admin/dashboard/0/`` in browser.


Documentation
-------------

Check out docs_ for more complete examples.


Compatability
-------------

.. image:: https://travis-ci.org/byashimov/django-controlcenter.svg?branch=master
    :alt: Build Status
    :target: https://travis-ci.org/byashimov/django-controlcenter

.. image:: https://codecov.io/github/byashimov/django-controlcenter/coverage.svg?branch=master
    :alt: Codecov
    :target: https://codecov.io/github/byashimov/django-controlcenter?branch=master

Tested on py 2.7, 3.4, 3.5 with django 1.8, 1.9, 1.10.


Credits
-------

This project uses Chartist.js_, Masonry.js_ and Sortable.js_.


Changelog
---------

Only worthy changes are listed in here.

0.2.1
~~~~~
- Django 1.10 support. Tested in tox *only*.

0.2.0
~~~~~
- Unlimited dashboards support.
- Configuration constructor is moved to a separate project -- django-pkgconf_. It's a dependency now.

0.1.2
~~~~~
- Chart ``i`` series color fix. Thanks to @uncleNight.
- Docs. Finally.

0.1.1
~~~~~
- Better responsive experience.

0.1.0
~~~~~
- First public release.

.. _Chartist.js: http://gionkunz.github.io/chartist-js/
.. _Masonry.js:  http://masonry.desandro.com/
.. _Sortable.js: http://github.hubspot.com/sortable/docs/welcome/
.. _Django-admin: https://docs.djangoproject.com/en/stable/ref/contrib/admin/
.. _django-pkgconf: https://github.com/byashimov/django-pkgconf
.. _docs: http://django-controlcenter.readthedocs.io/en/latest/