.. _schemaregistry_deletion:

Schema Deletion Guidelines
==========================

|sr| The API supports deleting a specific schema version or all versions of a subject. Because the API only deletes the version, the underlying schema ID remains available for any lookup. The following examples show various schema deletion options:

.. sourcecode:: bash

    # Deletes all schema versions registered under the subject "Kafka-value"
      curl -X DELETE http://localhost:8081/subjects/Kafka-value/[1]

    # Deletes version 1 of the schema registered under the subject "Kafka-value"
      curl -X DELETE http://localhost:8081/subjects/Kafka-value/versions/1

    # Deletes the most recently registered schema under the subject "Kafka-value"
      curl -X DELETE http://localhost:8081/subjects/Kafka-value/versions/latest

The schema deletion options listed above are intended primarily for use in an environment where it's common to go through iterations before finalizing a schema. While it's not generally recommended that you use these APIs in a production environment, you can safely use them in the following scenarios:

- To register a new schema that has compatibility issues with one of the existing schema versions
- To register an old version of the schema again for the same subject 
- To register schemas that are used only in real-time streaming systems (in which older versions are absolutely no longer      required)
- To recycle a topic

Important: Any registered compatibility settings for the subject are deleted when using Delete Subject or when deleting the only available schema version.
