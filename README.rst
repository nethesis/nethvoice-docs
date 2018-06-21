========================
NethVoice documentation
========================

Available documents:

* admin-manual

Inside each document directory there are some specials files:

* conf.py: Sphinx configuration
* Makefile: Sphinx build makefile
* index.rst: document structure

All other ``.rst`` files are chapters of the manual.
If you wish to add a new chapter, create a new file and add it to the index.rst file.

Branches
========

The manual should be develped on **master** branch and merged to current released version.

Available branches:

- master: developing branch
- v11: NethVoice 11
- v14: NethVoice 14

Alpha branches are marked by appending **a** to the branch name, eg: v14a.

Beta branches are marked by appending **b** to the branch name, eg: v14b.


How to contribute
=================

The easiest way to contribute is by forking and editing the repository
directly on GitHub:

* Create a GitHub account if you don't already have it
* Go to https://github.com/nethesis/nethvoice-docs and fork the project
* You can now edit any page using GitHub web interface and see a live preview of the output
* When you're done, simply create a new pull request
* A new automatic build is launched after the pull request is merged by a developer

You can also use the traditional way by cloning nethvoice-docs
repository (https://github.com/nethesis/nethvoice-docs ) to your
machine and sending patches to the mailing list.

While editing, please follow below guidelines.

Editing guidelines
------------------

The document must start with a title such as ::

    ==============
    Document title
    ==============

Next headers levels are::

    First level
    ===========

    Second level
    ------------

    Third level
    ^^^^^^^^^^^

    Fourth level
    ~~~~~~~~~~~~

Use the \* character for unordered list ::

    * First element
    * Second element

Use a definition list when describing fields ::

    My field
        This is my description

A field description can also contain a bullet list ::

    My field
        This is my description

        * First element
        * Second element

Highlight important words ::

    This is and *important* word.

Add notes with ::

    .. note:: Highlight this text

Add warnings with ::

    .. warning:: Warning text fragments



You can find more info about **RST Inline Markup** here: rst-cheatsheet_

.. _rst-cheatsheet: https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst


Do not use *NethVoice* name inside documentation. Any time you need to add the product name,
use the *product* macro::

  |product| has this amazing feature!

Output will be::

  NethVoice has this amazing feature!

The same applies to *download_site* macro.

Use semantic markup whenever possible. Recommended RST roles are:

* guilabel
* file
* command
* menuselection

Remember to emphasize system object with *:dfn:*, only the first time you mention them inside a section.
For example if you are naming a system user::

 The :dfn:`admin` user is mighty powerful.

Also take care of indexing important content. You must index a word only one time per section::

 The :dfn:`admin` user is mighty powerful.
 Remember to change the :index:`admin` password.

The output will be a paragraph where the first *admin* word will be italic, the latter will use standard font
but it will be indexed.

See also: http://sphinx-doc.org/markup/inline.html

Use a spell checker program before submitting a pull request. For instance run ::

  hunspell -d en_US <filename>

Build documentation
===================

Whenever there are modifications, a build process will be launched from Read the Docs site.

If you wish to build documentation locally on your machine, make sure to install all Sphinx packages.

First clone the repository, directory and type ::

   cd admin-manual/
   make html

Output files will be generated inside the *_build* directory.

The source language is Italian. To build the English manual: ::

   make -e SPHINXOPTS="-D language='en'" html

Requirements::

   pip install sphinx sphinx_rtd_theme sphinx_bootstrap_theme

Localization
============

The localization workflow is based on Zanata.

https://translate.zanata.org/project/view/nethvoice-docs

Install client
--------------

On Fedora: ::

  dnf install zanata-client

To configure the client for the first time see: http://docs.zanata.org/en/release/client/configuration/

Workflow
--------

The source language is Italian. To build the ``.pot`` files under
``_bulid/locale`` run ::

   make gettext

Upload ``.pot`` files to Zanata: ::

    zanata-cli push --src-lang it

Download tranlations from Zanata: ::

    zanata-cli pull

.. warning::

    Remember to commit the downloaded translations!

