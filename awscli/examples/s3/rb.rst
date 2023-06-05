**Example 1: Deleting a bucket**

The following ``rb`` command example removes the bucket ``mybucket``. Note that the bucket must be empty in order to be removed. ::

    aws s3 rb s3://mybucket

Output::

    remove_bucket: mybucket

**Example 2: Deleting a bucket and all its contents**

The following ``rb`` command example uses the ``--force`` parameter to remove all of the objects in the bucket ``mybucket`` and then remove the bucket itself. The contents of ``mybucket`` are ``test1.txt`` and ``test2.txt``. ::

    aws s3 rb s3://mybucket \
        --force

Output::

    delete: s3://mybucket/test1.txt
    delete: s3://mybucket/test2.txt
    remove_bucket: mybucket