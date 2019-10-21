{{cookiecutter.project_name}}
{{ '=' * cookiecutter.project_name|length }}

{{cookiecutter.description}}

.. image:: https://img.shields.io/badge/built%20with-Cookiecutter%20Django-ff69b4.svg
     :target: https://github.com/pydanny/cookiecutter-django/
     :alt: Built with Cookiecutter Django
.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
     :target: https://github.com/ambv/black
     :alt: Black code style
{% if cookiecutter.open_source_license != "Not open source" %}

:License: {{cookiecutter.open_source_license}}
{% endif %}

配置
--------

本项目基于 cookiecutter-django 进行二次开发，具体项目配置可以参考: settings_.

.. _settings: http://cookiecutter-django.readthedocs.io/en/latest/settings.html

基本命令
--------------

Setting Up Your Users
^^^^^^^^^^^^^^^^^^^^^

* 直接使用页面中的"注册"链接，创建 **普通用户** 。
    当提交时，将进入"邮件验证"页面，通过控制台查看模拟发送的邮件内容。
    复制地址至浏览器，点击验证后即注册成功。

* 通过下面命令创建 **超级管理员** ::

    $ python manage.py createsuperuser

通常，你可以通过在chrome中登录普通用户，在firefox(或其他)中登录超级管理员。这样您可以方便查看两者的区别。


类型监测
^^^^^^^^^^^

可以通过mypy来监测当前类型:

::

  $ mypy nbsync


覆盖测试
^^^^^^^^^^^^^

运行下述命令可以进行覆盖测试，并生成一份HTML的测试结果::

    $ coverage run -m pytest
    $ coverage html
    $ open htmlcov/index.html

运行测试用例 py.test
~~~~~~~~~~~~~~~~~~~~~~~~~~

::

  $ pytest

自加载以及Sass CSS编译
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

请查看 `Live reloading and SASS compilation`_.

.. _`Live reloading and SASS compilation`: http://cookiecutter-django.readthedocs.io/en/latest/live-reloading-and-sass-compilation.html


{% if cookiecutter.use_celery == "y" %}

Celery
^^^^^^

This app comes with Celery.

To run a celery worker:

.. code-block:: bash

    cd {{cookiecutter.project_slug}}
    celery -A config.celery_app worker -l info

Please note: For Celery's import magic to work, it is important *where* the celery commands are run. If you are in the same folder with *manage.py*, you should be right.

{% endif %}
{% if cookiecutter.use_mailhog == "y" %}

Email Server
^^^^^^^^^^^^
{% if cookiecutter.use_docker == 'y' %}
In development, it is often nice to be able to see emails that are being sent from your application. For that reason local SMTP server `MailHog`_ with a web interface is available as docker container.

Container mailhog will start automatically when you will run all docker containers.
Please check `cookiecutter-django Docker documentation`_ for more details how to start all containers.

With MailHog running, to view messages that are sent by your application, open your browser and go to ``http://127.0.0.1:8025``
{% else %}
In development, it is often nice to be able to see emails that are being sent from your application. If you choose to use `MailHog`_ when generating the project a local SMTP server with a web interface will be available.

#. `Download the latest MailHog release`_ for your OS.

#. Rename the build to ``MailHog``.

#. Copy the file to the project root.

#. Make it executable: ::

    $ chmod +x MailHog

#. Spin up another terminal window and start it there: ::

    ./MailHog

#. Check out `<http://127.0.0.1:8025/>`_ to see how it goes.

Now you have your own mail server running locally, ready to receive whatever you send it.

.. _`Download the latest MailHog release`: https://github.com/mailhog/MailHog/releases
{% endif %}
.. _mailhog: https://github.com/mailhog/MailHog
{% endif %}
{% if cookiecutter.use_sentry == "y" %}

Sentry
^^^^^^

Sentry is an error logging aggregator service. You can sign up for a free account at  https://sentry.io/signup/?code=cookiecutter  or download and host it yourself.
The system is setup with reasonable defaults, including 404 logging and integration with the WSGI application.

You must set the DSN url in production.
{% endif %}


部署
----------

以下将列举如何部署项目
{% if cookiecutter.use_heroku.lower() == "y" %}

Heroku
^^^^^^

See detailed `cookiecutter-django Heroku documentation`_.

.. _`cookiecutter-django Heroku documentation`: http://cookiecutter-django.readthedocs.io/en/latest/deployment-on-heroku.html
{% endif %}
{% if cookiecutter.use_docker.lower() == "y" %}

Docker
^^^^^^

详见 `cookiecutter-django Docker documentation`_.

.. _`cookiecutter-django Docker documentation`: http://cookiecutter-django.readthedocs.io/en/latest/deployment-with-docker.html

{% endif %}

{% if cookiecutter.custom_bootstrap_compilation == "y" %}
Custom Bootstrap Compilation
^^^^^^

The generated CSS is set up with automatic Bootstrap recompilation with variables of your choice.
Bootstrap v4 is installed using npm and customised by tweaking your variables in ``static/sass/custom_bootstrap_vars``.

You can find a list of available variables `in the bootstrap source`_, or get explanations on them in the `Bootstrap docs`_.

{% if cookiecutter.js_task_runner == 'Gulp' %}
Bootstrap's javascript as well as its dependencies is concatenated into a single file: ``static/js/vendors.js``.
{% endif %}

.. _in the bootstrap source: https://github.com/twbs/bootstrap/blob/v4-dev/scss/_variables.scss
.. _Bootstrap docs: https://getbootstrap.com/docs/4.1/getting-started/theming/

{% endif %}
