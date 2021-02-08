Transifex Translations
======================

Add transifex configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~
Fist of all, run the following command in order to set transifex token,

.. code:: sh

     export TX_TOKEN=api_token


Then we have to pull latest strings (e.g. Arabic) from tranisfex by the following command:

.. code:: sh

    tx pull -l ar


Add new strings to the project and push them to Transifex
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
After changing files or development, go to ``lms-shell``, then run the following command:

.. code:: sh

    make extract_translations

**NOTE:** This command will automatically extract strings from changed files, put them in multiple file segments (i.e. django-partial.po, mako.po and so on) and put them to the source language folder (i.e. conf/locale/en).

Merge these new string files to our target translation language (e.g. Arabic) folder (i.e. conf/locale/ar) by the following command:

.. code:: sh

    msgmerge conf/locale/ar/LC_MESSAGES/django-partial.po conf/locale/en/LC_MESSAGES/django-partial.po --update && msgmerge conf/locale/ar/LC_MESSAGES/django-partial.po conf/locale/en/LC_MESSAGES/django-partial.po --update && msgmerge conf/locale/ar/LC_MESSAGES/django-studio.po conf/locale/en/LC_MESSAGES/django-studio.po --update && msgmerge conf/locale/ar/LC_MESSAGES/djangojs-partial.po conf/locale/en/LC_MESSAGES/djangojs-partial.po --update && msgmerge conf/locale/ar/LC_MESSAGES/djangojs-studio.po conf/locale/en/LC_MESSAGES/djangojs-studio.po --update && msgmerge conf/locale/ar/LC_MESSAGES/mako.po conf/locale/en/LC_MESSAGES/mako.po --update && msgmerge conf/locale/ar/LC_MESSAGES/mako-studio.po conf/locale/en/LC_MESSAGES/mako-studio.po --update && msgmerge conf/locale/ar/LC_MESSAGES/underscore.po conf/locale/en/LC_MESSAGES/underscore.po --update && msgmerge conf/locale/ar/LC_MESSAGES/underscore-studio.po conf/locale/en/LC_MESSAGES/underscore-studio.po --update && msgmerge conf/locale/ar/LC_MESSAGES/wiki.po conf/locale/en/LC_MESSAGES/wiki.po --update

Generate ``i18n`` files by the following command:

.. code:: sh

     paver i18n_fastgenerate

**NOTE:** If You facing any errors in above ``i18n_fastgenerate`` command, then run ``django-admin.py compilemessages --locale=ar`` and resolve the errors manually and again run above command.

Generate ``i18n`` static js file `lms/static/js/i18n/ar/djangojs.js` by the following command:

.. code:: sh

    ./manage.py lms --settings=devstack_docker compilejsi18n
    ./manage.py cms --settings=devstack_docker compilejsi18n

Push the new string to the transifex by the following command:

.. code:: sh

   tx push -s -t
