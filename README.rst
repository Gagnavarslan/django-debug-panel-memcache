=============================
Django Debug Toolbar Memcache
=============================

This is a fork of Ross's excellent Memcache Debug Toolbar. It's an add-on for Django
Debug Toolbar for tracking memcached usage. It currently supports both the ``pylibmc``
and ``memcache`` libraries.

In this fork I'm refactoring the project to be more in line with django-debug-toolbar
panels. And I use its utilities and helpers to implement this panel. It is based on the
sql toolbar and has similar presentation and information.

These are some further technical differences from Memcache Debug Toolbar:

* No more inheriting client classes. Just using replace_call on the client methods. Which means explicit import is not needed
* Use utilities from debug_toolbar. Not sure why that would blow up.
* Record directly to panel instance instead of a Calls instance. Should be more thread safe.
* Collect and display template information from the stack trace.
* Display stacktrace and template info the same way sql panel does.
* Use same row toggle logic as sql panel, skip extra jquery.

Installation
============

#. Install and configure `Django Debug Toolbar <https://github.com/django-debug-toolbar/django-debug-toolbar>`_.

#. Add the ``debug_toolbar_memcache`` app to your ``INSTALLED_APPS``.

Configuration
=============

#. Add the ``memcache`` or ``pylibmc`` panel to ``DEBUG_TOOLBAR_PANELS``.

   You'll need to add the panel corresponding to the library you'll be using to
   the list of debug toolbar's panels in the order in which you'd like it to
   appear::

	DEBUG_TOOLBAR_PANELS = (
            ...
	    'debug_toolbar_memcache.panels.memcache.MemcachePanel',
	    # if you use pylibmc you'd include its panel instead
	    # 'debug_toolbar_memcache.panels.pylibmc.PylibmcPanel',
	)
