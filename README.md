# bump-version
No frills, simple semantic version bumping for python 2 & 3 projects.

bump-version stores the version in ```yourmodule/__init__.py``` under the ```__version__``` field. If you store your ```__version__``` field elsewhere, bump-version can use that too. bump-version uses git to commit the new version and tag it. 

## Install:

Just download the bump-version executable and place into your vendor/scripts/bin directory of your project
or stick it in your $HOME/bin or /usr/local/bin directory:

```
curl -O https://raw.githubusercontent.com/jzellman/bump-version/master/version
```

## Usage:

### Example setup
```
mkdir project
cd project
git init .
mkdir bin
pushd bin
curl -O https://raw.githubusercontent.com/jzellman/bump-version/master/version
chmod +x version
popd
```

### Example python project

```
# lets check the help:

./bin/version -h
usage: version [-h] [-f VERSION_FILE_PATH] [-b BUMP_TYPE] [--verbose]

Bump versions semantically. Example: ./bin/version -b patch

optional arguments:
  -h, --help            show this help message and exit
  -f VERSION_FILE_PATH  optional version file path
  -b BUMP_TYPE          major,minor,patch
  --verbose, -v

./bin/version
Error! No __init__ files found!

# this is expected, lets create a module along with the typical support files:


mkdir mymod
touch mymod/__init__.py
mkdir tests
touch tests/__init__.py
mkdir docs
git add bin/ mymod/
git commit -m 'Initial commit.'

./bin/version
Unknown

# verbose version
./bin/version -v
Current version in 'mymod/__init__.py': Unknown
```

### Lets mark the initial release
```
./bin/version -b major
Bumping major version in 'mymod/__init__.py': 0.0.0 -> 1.0.0
```

### Verify tags and commits
```
# lets check that the version command knows about the current version:
./bin/version
1.0.0

# and now verbosely
./bin/version -v
Current version in 'mymod/__init__.py': 1.0.0

# lets check the git log:
git log --pretty=oneline
# should see something like:
4042ff92ae5a719e6b755950cafd2098ccb5233b release: bump version to 1.0.0
91d2a145c2f959e42cdcbe13d51e4c468e5bf587 Initial commit.

# lets check the tags:
git tag
1.0.0

# lets see where the __version__ attribute is stored:
cat mymod/__init__.py
__version__ = '1.0.0'
```

### patches and minor changes
```
# uh oh a bug was found!
./bin/version -b patch
Bumping patch version in library: '1.0.0' -> 1.0.1

# a minor enhancement!
./bin/version -b minor
Bumping minor version in library: '1.0.1' -> 1.1.0
```

## Specifying the version file
```
./bin/version -f mymod/__init__.py
1.1.0

./bin/version -f mymod/__init__.py -b major
Bumping major version in 'mymod/__init__.py': 1.1.0 -> 2.0.0

./bin/version -f mymod/__init__.py
2.0.0
```

## Additional features

### Support for running a command after version is bumped but before tagging is complete

A good use is updating a changelog that uses git tags for reference. If we update the 
changelog after ```version``` is ran, the changelog won't be part of the tag. 
Here is how you can handle that:

```
./bin/version -b minor -c 'make changelog'
Bumping minor version in library: '1.1.0' -> 1.2.0
Running make changelog before tagging...
```



