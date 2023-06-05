**Example 1: Moving a file to the specified bucket**

The following ``mv`` command example moves a single object to the ``mybucket`` bucket. ::

    aws s3 mv s3://mybucket/test.txt s3://mybucket2/

Output::

    move: s3://mybucket/test.txt to s3://mybucket2/test.txt

**Example 2: Moving a file to the specified bucket and key**

The following ``mv`` command example moves a single file to the ``mybucket`` bucket and renaming to the ``test2.txt`` key. ::

    aws s3 mv test.txt s3://mybucket/test2.txt

Output::

    move: test.txt to s3://mybucket/test2.txt

**Example 3: Moving an S3 object to the specified bucket**

The following ``mv`` command example moves a single S3 object to the ``mybucket`` bucket and renaming to the ``test2.txt`` key. ::

    aws s3 mv s3://mybucket/test.txt s3://mybucket/test2.txt

Output::

    move: s3://mybucket/test.txt to s3://mybucket/test2.txt

**Example 4: Moving an S3 object to a local file**

The following ``mv`` command example moves a single object to a the current local directory a renames it to ``test2.txt``. ::

    aws s3 mv s3://mybucket/test.txt test2.txt

Output::

    move: s3://mybucket/test.txt to test2.txt


**Example 5: Moving all object under the specified bucket to the local directory**

The following ``mv`` command example uses the ``--recursive`` parameter to move all objects under the specified bucket to the current local directory. In this example, the bucket ``mybucket`` contains the objects
``test1.txt`` and ``test2.txt``. ::

    aws s3 mv s3://mybucket . \
        --recursive

Output::

    move: s3://mybucket/test1.txt to test1.txt
    move: s3://mybucket/test2.txt to test2.txt

**Example 6: Moving all objects under the specified bucket to the local**

The following ``mv`` command example uses the parameter ``--recursive`` to move all objects under the specified directory to the specified bucket while excluding ``.jpg`` files using the ``--exclude`` parameter. In this example, the directory ``myDir`` contains the files ``test1.txt`` and ``test2.jpg``. ::

    aws s3 mv myDir s3://mybucket/ \
        --recursive \
        --exclude "*.jpg"

Output::

    move: myDir/test1.txt to s3://mybucket2/test1.txt

**Example 6: Moving S3 objects to the specified while excluding object under the specified prefix**

The following ``mv`` command example uses the parameter ``--recursive`` to move all objects under the specified bucket to another bucket while excluding files under the ``another`` prefix using the ``--exclude`` parameter. In this example, the bucket ``mybucket`` has the objects ``test1.txt`` and ``another/test1.txt``::

    aws s3 mv s3://mybucket/ s3://mybucket2/ \
        --recursive \
        --exclude "mybucket/another/*"

Output::

    move: s3://mybucket/test1.txt to s3://mybucket2/test1.txt

**Example 7: Moving S3 objects to the specified bucket and setting the ACL**

The following ``mv`` command example moves a single object to a specified bucket and key while setting the ACL to ``public-read-write``. ::

    aws s3 mv s3://mybucket/test.txt s3://mybucket/test2.txt \
        --acl public-read-write

Output::

    move: s3://mybucket/test.txt to s3://mybucket/test2.txt

**Example 8: Moving an S3 object to the specified bucket and granting ACL permissions**

The following ``mv`` command example moves a local file to the specified S3 bucket and uses the ``--grants`` option to grant read access to all users and full control to a specific user identified by their email address. ::

    aws s3 mv file.txt s3://mybucket/ \
        --grants read=uri=http://acs.amazonaws.com/groups/global/AllUsers full=emailaddress=user@example.com

Output::

    move: file.txt to s3://mybucket/file.txt

**Example 9: Moving a local file to an S3 access point**

The following ``mv`` command example moves the ``mydoc.txt` local file ` to the ``myaccesspoint`` access point at the ``mykey`` key. ::

    aws s3 mv mydoc.txt s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/mykey

Output::

    move: mydoc.txt to s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/mykey