Kurento Repository API Documentation 
====================================

The :java:package:`com.kurento.kmf.repository` package 
(`javadoc <../_static/index.html?com/kurento/kmf/repository/package-summary.html>`__)
includes the media repository offered by the Kurento Media Framework.

The API includes a :java:type:`Repository` interface, intended to
store media files. It has methods to :java:meth:`create <createRepositoryItem>`,
:java:meth:`find <findRepositoryItemById>` or :java:meth:`remove`
:java:type:`repository items <RepositoryItem>`. A :java:type:`RepositoryItem`
can act as an :java:type:`HTTP endpoint < RepositoryHttpEndpoint>`, that can
create :java:meth:`a recorder <RepositoryItem.createRepositoryHttpRecorder>` or 
:java:meth:`a player <RepositoryItem.createRepositoryHttpPlayer>`.

Javadoc
-------

`Javadoc of the Kurento Repository API  <../_static/index.html?com/kurento/kmf/repository/package-summary.html>`__ classes.

API Classes
-----------

.. toctree::
   :maxdepth: 2

   com/kurento/kmf/repository/package-index
