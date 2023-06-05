**Example 1: Copying an S3 object from one bucket to another**

The following ``cp`` command example copies the ``test.txt`` s3 object to the ``mybucket`` bucket. ::

    aws s3 cp s3://mybucket/test.txt s3://mybucket2/

Output::

    copy: s3://mybucket/test.txt to s3://mybucket2/test.txt

**Example 2: Copying an S3 object from one bucket to another and changing the key**

The following ``cp`` command example copies the ``test.txt`` s3 object to the ``mybucket`` bucket and changes the object to the key to ``test2.txt``. ::

    aws s3 cp s3://mybucket/test.txt s3://mybucket/test2.txt

Output::

    copy: s3://mybucket/test.txt to s3://mybucket/test2.txt

**Example 3: Copying a local file to S3**

The following ``cp`` command example copies the ``test.txt`` file in the current local directory to the ``mybucket`` bucket and changes the key to ``test2.txt``. ::

    aws s3 cp test.txt s3://mybucket/test2.txt

Output::

    upload: test.txt to s3://mybucket/test2.txt

**Example 4: Copying a local file to S3 with an expiration date**

The following ``cp`` command example copies the ``test.txt`` file in the current local directory to the ``mybucket`` bucket and changes the key to ``test2.txt`` that expires at the specified ISO 8601 timestamp. ::

    aws s3 cp test.txt s3://mybucket/test2.txt \
        --expires 2014-10-01T20:30:00Z

Output::

    upload: test.txt to s3://mybucket/test2.txt

**Example 5: Copying an S3 object to a local file**

The following ``cp`` command example copies the ``test.txt`` S3 object from the ``mybucket`` bucket to the current local directory and changes the key to ``test2.txt``. ::

    aws s3 cp s3://mybucket/test.txt test2.txt

Output::

    download: s3://mybucket/test.txt to test2.txt

**Example 6: Recursively copying S3 objects to a local directory**

The following ``cp`` command example uses the ``--recursive`` parameter to copy all objects under the ``mybucket`` bucket to the current local directory. The ``mybucket`` bucket contains objects ``test1.txt`` and ``test2.txt``. ::

    aws s3 cp s3://mybucket . \
        --recursive

Output::

    download: s3://mybucket/test1.txt to test1.txt
    download: s3://mybucket/test2.txt to test2.txt

**Example 7: Recursively copying local files to S3**

The following ``cp`` command example uses the ``--recursive`` parameter to copy all files and folder in the current local directory to the the ``mybucket`` bucket while excluding ``.jpg`` files. The ``myDir`` directory contains files ``test1.txt`` and ``test2.jpg``. ::

    aws s3 cp myDir s3://mybucket/ \
        --recursive \
        --exclude "*.jpg"

Output::

    upload: myDir/test1.txt to s3://mybucket/test1.txt

**Example 8: Recursively copying S3 objects to another bucket**

The following ``cp`` command example uses the ``--recursive`` parameter to copy all S3 objects in the ``mybucket`` bucket to the ``mybucket2`` bucket while excluding objects in the ``another`` prefix. The ``mybucket`` bucket has the objects ``test1.txt`` and ``another/test1.txt``. ::

    aws s3 cp s3://mybucket/ s3://mybucket2/ \
        --recursive \
        --exclude "another/*"

Output::

    copy: s3://mybucket/test1.txt to s3://mybucket2/test1.txt

**Example 9: Copying only S3 object that match a specified pattern**

The following ``cp`` command example uses the ``--recursive`` parameter to copy all ``.log`` files in the ``mybucket`` bucket to the ``mybucket2`` bucket while excluding all other S3 objects. ::

    aws s3 cp s3://mybucket/logs/ s3://mybucket2/logs/ \
        --recursive \
        --exclude "*" \
        --include "*.log"

Output::

    copy: s3://mybucket/logs/test/test.log to s3://mybucket2/logs/test/test.log
    copy: s3://mybucket/logs/test3.log to s3://mybucket2/logs/test3.log

**Example 10: Copying S3 objects and setting the Access Control List (ACL)**

The following ``cp`` command example copies the ``test.txt`` s3 object to the ``mybucket`` bucket and changes the object to the key to ``test2.txt`` while setting the ACL to ``public-read-write``. ::

    aws s3 cp s3://mybucket/test.txt s3://mybucket/test2.txt \
        --acl public-read-write

Output::

    copy: s3://mybucket/test.txt to s3://mybucket/test2.txt

Note that if you're using the ``--acl`` option, ensure that any associated IAM policies include the ``"s3:PutObjectAcl"`` action. ::

    aws iam get-user-policy \
        --user-name myuser \
        --policy-name mypolicy

Output::

    {
        "UserName": "myuser",
        "PolicyName": "mypolicy",
        "PolicyDocument": {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Action": [
                        "s3:PutObject",
                        "s3:PutObjectAcl"
                    ],
                    "Resource": [
                        "arn:aws:s3:::mybucket/*"
                    ],
                    "Effect": "Allow",
                    "Sid": "Stmt1234567891234"
                }
            ]
        }
    }

**Example 11: Granting permissions for an S3 object**

The following ``cp`` command example copies the ``test.txt`` file in the current local directory to the ``mybucket`` bucket and uses the ``--grants`` option to grant ``read`` access to all users and ``full control`` to a specific user identified by their URI. ::

    aws s3 cp file.txt s3://mybucket/ \
        --grants read=uri=http://acs.amazonaws.com/groups/global/AllUsers full=uri=79a59df900b949e55d96a1e698fbacedfd6e09d98eacf8f8d5218e7cd47ef2be

Output::

    upload: file.txt to s3://mybucket/file.txt

**Example 12: Uploading a local file stream to S3**

.. WARNING:: PowerShell may alter the encoding of or add a CRLF to piped input.

The following ``cp`` command example uploads a local file stream from standard input to the specified bucket and key. ::

    aws s3 cp - s3://mybucket/stream.txt

**Example 13: Uploading a local file stream that is larger than 50GB to S3**

The following ``cp`` command example uploads a 51GB local file stream from standard input to the specified bucket and key. The ``--expected-size`` option must be provided, or the upload may fail when it reaches the default part limit of 10,000. ::

    aws s3 cp - s3://mybucket/stream.txt \
        --expected-size 54760833024

**Example 14: Copying an S3 object as a local file stream**

.. WARNING:: PowerShell may alter the encoding of or add a CRLF to piped or redirected output.

The following ``cp`` command example copies an S3 object from the ``mybucket`` bucket to the local directory as a stream to standard output. Downloading as a stream is not currently compatible with the ``--recursive`` parameter. ::

    aws s3 cp s3://mybucket/stream.txt -

**Example 15: Copying to an S3 access point**

The following ``cp`` command example copies the ``mydoc.txt`` file from the current local directory to the to the ``myaccesspoint`` access point to the ``mykey`` key. ::

    aws s3 cp mydoc.txt s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/mykey

Output::

    upload: mydoc.txt to s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/mykey

**Example 16: Copying from an S3 access point**

The following ``cp`` command example copies the ``mykey`` object from the ``myaccesspoint`` access point to the ``mydoc.txt`` file in the current local directory. ::

    aws s3 cp s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/mykey mydoc.txt

Output::

    download: s3://arn:aws:s3:us-west-2:123456789012:accesspoint/myaccesspoint/mykey to mydoc.txt