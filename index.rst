.. GWM Redesign documentation master file, created by
   sphinx-quickstart on Tue Oct  7 11:05:20 2014.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

GWM Redesign
============

Ganeti Web Manager is a home-grown project from the Oregon State
University Open Source Lab for managing Ganeti clusters.

This document describe plans for a redesigned and rewritten GWM.

Infrastructure
--------------

Django
    Used to implement the HTTP API. Only outputs JSON data.

PostgreSQL
    Relational datastore to hold Ganeti cluster, instance, node, and job data.

Celery
    Asynchronous Job workers for updating the PostgreSQL database with
    Ganeti information.

RabbitMQ
    Job queue manager which acts as the mediary between celery workers
    and Ganeti clusters.

Keystone Auth
    Authorization provider that can talk to optional LDAP backend.
    Provides tokens to application for talking to the HTTP API.

.. image:: _static/img/proposed_infra.png
    :scale: 200%


Releases
--------

.. note::
    There are no plans to support any users deploying the application,
    until the project comes out of alpha/beta status. Support will be
    provided to contributors: those activly developing, documenting, or
    testing the application.

The application will follow a rolling release (continuous deployment)
cycle. Versions will be tagged every three months, as the majority of
the team will be made up of OSL students.

After each release the API will be frozen, beginning with **/v1.0**. All
modifications to the API must be added to the next version (ex.
**/v2.0**). If the API is found to contain a bug (the implementation
does not match the documentation), a point release will be issued to
that API version.

*master* will be the default branch with anything in *master* being
deployable. Tags will be annotated and signed by a maintainer's GPG key.
Tags will have the form of **vYYYYMM** (ex.  **v201409**). This is
assured to be a monotonically increasing number.

All contributions should be made through pull requests or git patch
emails, and will be reviewed before being merged in.
