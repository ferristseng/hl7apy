# NYGC Fork of https://github.com/crs4/hl7apy - for use in Bessemer

Fork of https://github.com/crs4/hl7apy Addresses missing Withdrawn (WD) fields and segment fields which cause false positive errors during message parsing.

For example, field PID_28 is missing:

* https://github.com/crs4/hl7apy/blob/v1.3.4/hl7apy/v2_8_2/fields.py#L1676-L1677
* https://github.com/crs4/hl7apy/blob/v1.3.4/hl7apy/v2_8_2/segments.py#L1980-L1981

Will perhaps make a pull request on Github once all missing fields are encountered and addressed...

$ git clone ssh://git@bitbucket.nygenome.org:7999/prod/hl7apy-forked.git ; cd hl7apy-forked
# fork the repo
$ git remote add sync https://github.com/crs4/hl7apy.git

$ git remote -v
origin	ssh://git@bitbucket.nygenome.org:7999/prod/hl7apy-forked.git (fetch)
origin	ssh://git@bitbucket.nygenome.org:7999/prod/hl7apy-forked.git (push)
sync	https://github.com/crs4/hl7apy.git (fetch)
sync	https://github.com/crs4/hl7apy.git (push)

$ git fetch --tags sync
remote: Enumerating objects: 588, done.
remote: Counting objects: 100% (42/42), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 588 (delta 28), reused 40 (delta 28), pack-reused 546
Receiving objects: 100% (588/588), 1022.72 KiB | 5.47 MiB/s, done.
Resolving deltas: 100% (380/380), completed with 11 local objects.
From https://github.com/crs4/hl7apy
 * [new branch]      develop     -> sync/develop
 * [new branch]      gh-pages    -> sync/gh-pages
 * [new branch]      ihic2015    -> sync/ihic2015
 * [new branch]      master      -> sync/master
 * [new tag]         v1.0.0      -> v1.0.0
 * [new tag]         v1.0.0-rc.1 -> v1.0.0-rc.1
 * [new tag]         v1.0.0-rc.2 -> v1.0.0-rc.2
 * [new tag]         v1.0.1      -> v1.0.1
 * [new tag]         v1.1.0      -> v1.1.0
 * [new tag]         v1.1.1      -> v1.1.1
 * [new tag]         v1.1.2      -> v1.1.2
 * [new tag]         v1.2.0      -> v1.2.0
 * [new tag]         v1.3.0      -> v1.3.0
 * [new tag]         v1.3.1      -> v1.3.1
 * [new tag]         v1.3.2      -> v1.3.2
 * [new tag]         v1.3.3      -> v1.3.3
 * [new tag]         v1.3.4      -> v1.3.4

$ git push --tags origin
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To ssh://bitbucket.nygenome.org:7999/prod/hl7apy-forked.git
 * [new tag]         v1.0.0 -> v1.0.0
 * [new tag]         v1.0.0-rc.1 -> v1.0.0-rc.1
 * [new tag]         v1.0.0-rc.2 -> v1.0.0-rc.2
 * [new tag]         v1.0.1 -> v1.0.1
 * [new tag]         v1.1.0 -> v1.1.0
 * [new tag]         v1.1.1 -> v1.1.1
 * [new tag]         v1.1.2 -> v1.1.2
 * [new tag]         v1.2.0 -> v1.2.0
 * [new tag]         v1.3.0 -> v1.3.0
 * [new tag]         v1.3.1 -> v1.3.1
 * [new tag]         v1.3.2 -> v1.3.2
 * [new tag]         v1.3.3 -> v1.3.3
 * [new tag]         v1.3.4 -> v1.3.4

# create master-nygc branch from v1.3.4 (this is only done once to establish the branch with the patched changes)
# make the patch changes like missing PID_28, etc. to this 
$ git checkout -b master-nygc v1.3.4
$ git add --all
$ git commit -m "patched missing PID, OBR fields in v2_8_2/fields.py and v2_8_2/segments.py"
$ git push origin master-nygc

# create new branch to test changes on the new version
$ git checkout -b feature/v1.3.4-nygc v1.3.4
# merge in our patch into the new versioned feature branch
$ git merge --no-ff master-nygc
# TEST the feature branch!  If all goes well merge feature/v1.3.4-nygc back into master-nygc
$ git push origin feature/v1.3.4-nygc
$ git checkout master-nygc
$ git merge --no-ff feature/v1.3.4-nygc
$ git push origin master-nygc
$ git tag v1.3.4-nygc
$ git push origin v1.3.4-nygc

---

HL7apy is a lightweight Python package to intuitively handle [HL7](http://www.hl7.org) v2 messages according to HL7 specifications.

The main features includes:

 * Message parsing
 * Message creation
 * Message validation following the HL7 xsd specifications
 * Access to elements by name, long name or position
 * Support to all simple and complex datatypes
 * Encoding chars customization
 * Message encoding in ER7 format and compliant with MLLP protocol
 * Support to message profile
 * Support to Z-Elements
 * Simple MLLP server implementation

Currently supported HL7 versions are: 2.1, 2.2, 2.3, 2.3.1, 2.4, 2.5, 2.5.1, 2.6, 2.7, 2.8, 2.8.1, 2.8.2

Current version is __1.3.4__

This project is not affiliated with the HL7 organization: the library is just consistent with their specification.

Documentation can be found [here](http://crs4.github.io/hl7apy/).

Installation
------------

HL7apy is platform independent and supports Python 2.7 and Python 3.4, 3.5, 3.6, 3.7

To install it get the latest release from [GitHub](https://github.com/crs4/hl7apy/releases) and launch the following command:

```bash
  python setup.py install
```

Alternatively you can use pip to install it from [PyPI](https://pypi.python.org/pypi/hl7apy/)

```bash
  pip install hl7apy
```

[![Build Status](https://travis-ci.org/crs4/hl7apy.png)](https://travis-ci.org/crs4/hl7apy)

[![Code Health](https://landscape.io/github/crs4/hl7apy/develop/landscape.svg?style=flat)](https://landscape.io/github/crs4/hl7apy/develop)

[![Coverage Status](https://coveralls.io/repos/crs4/hl7apy/badge.svg)](https://coveralls.io/r/crs4/hl7apy)

External Links
--------------

Michael Sarfati wrote an interesting 2-parts article on his blog about HL7apy with useful examples and tutorials. 
You can read it [here](https://msarfati.wordpress.com/2015/06/20/python-hl7-v2-x-and-hl7apy-introduction-and-parsing-part-1/). 
Thanks a lot Michael for your contribution.


License
-------

HL7apy is released under the MIT License.

Copyright (c) 2012-2018, CRS4

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

