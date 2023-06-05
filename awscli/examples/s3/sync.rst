**Example 1: Sync objects from the local directory to the specified bucket**

The following ``sync`` command syncs objects from a local diretory to the specified prefix and bucket by
uploading the local files to s3.  A local file will require uploading if the size of the local file is different than
the size of the s3 object, the last modified time of the local file is newer than the last modified time of the s3
object, or the local file does not exist under the specified bucket and prefix.  In this example, the user syncs the
bucket ``mybucket`` to the local current directory.  The local current directory contains the files ``test.txt`` and
``test2.txt``.  The bucket ``mybucket`` contains no objects. ::

    aws s3 sync . s3://mybucket

Output::

    upload: test.txt to s3://mybucket/test.txt
    upload: test2.txt to s3://mybucket/test2.txt

**Example 2: Sync objects between two specified buckets**

The following ``sync`` command example syncs objects from the bucket ``mybucket`` to the bucket ``mybucket2``. The bucket ``mybucket`` contains the objects ``test.txt`` and ``test2.txt``.  The bucket ``mybucket2`` contains no objects. ::

    aws s3 sync s3://mybucket s3://mybucket2

Output::

    copy: s3://mybucket/test.txt to s3://mybucket2/test.txt
    copy: s3://mybucket/test2.txt to s3://mybucket2/test2.txt

**Example 3: Sync objects from the specified bucket to the local directory**

The following ``sync`` command example syncs the current local directory to the bucket ``mybucket`` which contains the objects ``test.txt`` and ``test2.txt``. The current local directory has no files. ::

    aws s3 sync s3://mybucket .

Output::

    download: s3://mybucket/test.txt to test.txt
    download: s3://mybucket/test2.txt to test2.txt

**Example 4: Sync**

The following ``sync`` command example syncs the bucket ``mybucket`` to the local current directory.  The local current directory contains the files ``test.txt`` and ``test2.txt``. The bucket ``mybucket`` contains the object ``test3.txt``.

The ``--delete`` parameter deletes any files existing under the bucket ``mybucket`` that is not existing in the local directory. ::

    aws s3 sync . s3://mybucket \
        --delete

Output::

    upload: test.txt to s3://mybucket/test.txt
    upload: test2.txt to s3://mybucket/test2.txt
    delete: s3://mybucket/test3.txt

**Example 5: Sync object from the specified bucket to the local directory excluding .jpg files**

The following ``sync`` command syncs the bucket ``mybucket`` to the local current directory. The local current directory contains the files ``test.jpg`` and ``test2.txt``. The bucket ``mybucket`` contains the object ``test.jpg`` of a different size than the local ``test.jpg``. 

The ``--exclude`` parameter exludes all ``.jpg`` files matching the pattern existing both in s3 and locally from the sync. ::

    aws s3 sync . s3://mybucket \
        --exclude "*.jpg"

Output::

    upload: test2.txt to s3://mybucket/test2.txt

**Example 6: Sync**

The following ``sync`` command example syncs the local current directory to the bucket ``mybucket``. The local current directory contains the files ``test.txt`` and ``another/test2.txt``.  The bucket ``mybucket`` contains the objects ``another/test5.txt`` and ``test1.txt``.

The ``--exclude`` parameter excludes the directory and s3 prefix named ``another`` from the ``sync`` command. ::

    aws s3 sync s3://mybucket/ . \
        --exclude "*another/*"

Output::

    download: s3://mybucket/test1.txt to test1.txt

**Example 7: Sync two buckets in different regions**

The following ``sync`` command example syncs files between two buckets in different regions. ::

    aws s3 sync s3://my-us-west-2-bucket s3://my-us-east-1-bucket \
        --source-region us-west-2 \
        --region us-east-1


**Example 8: Sync to an S3 access point**

The following ``sync`` command example syncs the current directory to the access point ``myaccesspoint``. ::

    aws s3 sync . s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/

Output::

    upload: test.txt to s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/test.txt
    upload: test2.txt to s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/test2.txt