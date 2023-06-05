**Example 1: Deleting a single s3 object**

The following ``rm`` command example deletes a single s3 object. ::

    aws s3 rm s3://mybucket/test2.txt

Output::

    delete: s3://mybucket/test2.txt

**Example 2: Deleting all objects under the specified bucket**

The following ``rm`` command example uses the parameter ``--recursive``to delete all objects under the bucket ``mybucket``. The bucket ``mybucket`` contains the objects ``test1.txt`` and
``test2.txt``. ::

    aws s3 rm s3://mybucket \
        --recursive

Output::

    delete: s3://mybucket/test1.txt
    delete: s3://mybucket/test2.txt

**Example 3: Deleting all objects under the specified bucket excluding the specified file types**

The following ``rm`` command example uses the parameter ``--recursive`` to delete all objects under the specified bucket while excluding ``.jpg`` files using the ``--exclude`` parameter. The bucket ``mybucket`` has the objects ``test1.txt`` and ``test2.jpg``::

    aws s3 rm s3://mybucket/ \
        --recursive \
        --exclude "*.jpg"

Output::

    delete: s3://mybucket/test1.txt

**Example 4: Deleting all objects under the specified bucket excluding files under the specified prefix**

The following ``rm`` command example uses the parameter ``--recursive`` to delete all objects under a specified bucket while excluding files under the ``another`` prefix using the ``--exclude`` parameter. In this example, the bucket ``mybucket`` contains the objects ``test1.txt`` and ``another/test.txt``. ::

    aws s3 rm s3://mybucket/ \
        --recursive \
        --exclude "another/*"

Output::

    delete: s3://mybucket/test1.txt


**Example 5: Deleting an object from an S3 access point**

The following ``rm`` command example deletes a single object (``mykey``) from the access point (``myaccesspoint``). ::

    aws s3 rm s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/mykey

Output::

    delete: s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/mykey
