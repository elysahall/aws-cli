**Example 1: Creating a bucket in your default region**

The following ``mb`` command example creates the ``mybucket`` bucket using the region specified in the configuration file. ::

    aws s3 mb s3://mybucket

Output::

    make_bucket: s3://mybucket

**Example 2: Creating a bucket in the specified region**

The following ``mb`` command example creates the ``mybucket`` bucket in the ``us-west-1`` region using the ``--region`` parameter. ::

    aws s3 mb s3://mybucket \
        --region us-west-1

Output::

    make_bucket: s3://mybucket