Using webpack-dev-server and HMR
================================

While developing, instead of using ``yarn encore dev --watch``, you can use the
`webpack-dev-server`_:

.. code-block:: terminal

    $ yarn encore dev-server

This serves the built assets from a new server at ``http://localhost:8080`` (it does
not actually write any files to disk). This means your ``script`` and ``link`` tags
need to change to point to this.

If you're using the ``encore_entry_script_tags()`` and ``encore_entry_link_tags()``
Twig shortcuts (or are :ref:`processing your assets through entrypoints.json <load-manifest-files>`
in some other way), you're done: the paths in your templates will automatically point
to the dev server.

You can also pass options to the ``dev-server`` command: any options that are supported
by the normal `webpack-dev-server`_. For example:

.. code-block:: terminal

    $ yarn encore dev-server --https --port 9000

This will start a server at ``https://localhost:9000``.

.. note::

    This Webpack server is independent from
    :doc:`Symfony's development web server </setup/built_in_web_server>` and
    you need to run both separately.

Using dev-server inside a VM
----------------------------

If you're using ``dev-server`` from inside a virtual machine, then you'll need
to bind to all IP addresses and allow any host to access the server:

.. code-block:: terminal

    $ ./node_modules/.bin/encore dev-server --host 0.0.0.0 --disable-host-check

You can now access the dev-server using the IP address to your virtual machine on
port 8080 - e.g. http://192.168.1.1:8080.

Hot Module Replacement HMR
--------------------------

Encore *does* support `HMR`_, but only in some areas. To activate it, pass the ``--hot``
option:

.. code-block:: terminal

    $ ./node_modules/.bin/encore dev-server --hot

HMR currently works for :doc:`Vue.js </frontend/encore/vuejs>`, but does *not* work
for styles anywhere at this time.

.. _`webpack-dev-server`: https://webpack.js.org/configuration/dev-server/
.. _`HMR`: https://webpack.js.org/concepts/hot-module-replacement/
