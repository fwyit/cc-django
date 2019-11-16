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

此项目整合Celery项目

创建celery的job:

.. code-block:: bash

    cd cmdb
    celery -A config.celery_app worker -l info

请注意：鉴于import的特性，需要进入到项目路径下使用celery命令。以上步骤需要在**manage.py**同级目录下执行。

{% endif %}
{% if cookiecutter.use_mailhog == "y" %}

Email Server
^^^^^^^^^^^^
{% if cookiecutter.use_docker == 'y' %}

开发过程中，经常需要从程序中发送邮件。故本次使用docker容器创建一个本地SMTP服务 `MailHog`_ 。
当使用`docker-compose up`启动所有容器时，将自动启动mailhog服务。

更多详情，请参考 `cookiecutter-django Docker documentation`。

当mailhog启动时，可以通过打开浏览器访问``http://127.0.0.1:8025``来查看邮件信息。

.. _MailHog: https://github.com/mailhog/MailHog

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

Sentry是一个错误日志收集工具。可以通过 https://sentry.io/signup/?code=cookiecutter 来创建一个免费账户或者直接在本地进行安装。
程序将自动创建包括但不限于404登录以及与其他WSGI交互的应用程序。
生产环境上需要自定义 **DSN** 。

{% endif %}


部署
----------

以下将列举如何部署项目
{% if cookiecutter.use_heroku.lower() == "y" %}

Heroku
^^^^^^

详见 `cookiecutter-django Heroku documentation`_.

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

您可以自己选择bootstrap版本来进行CSS等样式选择。
使用npm，可以自动在``static/sass/custom_bootstrap_vars``文件中选择bootstrap v4版本所需要编译的组建。

可以通过 `in the bootstrap source`_ 查询所有可以使用的变量，或在 `Bootstrap docs`_ 中查看组建详情。

{% if cookiecutter.js_task_runner == 'Gulp' %}
Bootstrap的javasript将合并至一个统一文件``static/js/vendors.js``。
{% endif %}

.. _in the bootstrap source: https://github.com/twbs/bootstrap/blob/v4-dev/scss/_variables.scss
.. _Bootstrap docs: https://getbootstrap.com/docs/4.1/getting-started/theming/

{% endif %}
