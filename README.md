# bump-version
No frills, simple semantic version bumping for python projects.

bump-version stores the version in yourmodule/__init__.py under the __version__ field. It also uses git to commit the new version and tag it. 

## Install:

Just download the bump-version executable and place into your vendor/scripts/bin directory of your project
or stick it in your $HOME/bin or /usr/local/bin directory:

```
curl -O https://raw.githubusercontent.com/jzellman/bump-version/master/bump-version
```

## Usage:

### Example setup
```
mkdir project
cd project
git init .
mkdir bin
pushd bin
curl -O https://raw.githubusercontent.com/jzellman/bump-version/master/bump-version
popd
```

### Create example python project

```
./bin/bump-version
Error! No init files found!

mkdir mymod
touch mymod/__init__.py
mkdir tests
touch tests/__init__.py
mkdir docs
git add bin/ mymod/
git commit -m 'Initial commit.'
./bin/bump-version
Usage: ./bin/bump-version <major|minor|patch>
Current version: Unknown
```

### Lets mark the initial release
```
./bin/bump-version major
Bumping major version in library: 0.0.0 -> 1.0.0
```

### Check tags and commits
```
git log --pretty=oneline
# should see something like:
4042ff92ae5a719e6b755950cafd2098ccb5233b release: bump version to 1.0.0
91d2a145c2f959e42cdcbe13d51e4c468e5bf587 Initial commit.

git tag
1.0.0

cat mymod/__init__.py
__version__ = '1.0.0'
```




