homebrew-pymol
==========

The simplest way to install [Pymol][pymol] with [Homebrew][hb] is with
the following method (incomplete install):

**Requirements:** The latest available XQuartz (at least 2.7.2) build of
X11.

```
# make sure that brew is up to date
brew update

# if you don't already have pmw (check with `python -c "import Pmw"`)
brew tap sameuljohn/python
brew install pmw

# install pymol
brew tap scicalculator/pymol
brew install pymol
```

However, this method does not give access to Pymol's "External GUI"
because Pymol doesn't use the main thread for it's external gui's. To
get that working, please following the more complex installation below.
The *main GUI* works without problems, but the "external GUI" does not
yet work out of the box. There are some ways I have devised to get it to
work, but it is currently not yet as simple as I had hoped. People are
working on it :)

```
# reset if necessary (only necessary if you previsouly installed tk,tcl, or python)
brew uninstall python
brew uninstall tk
brew uninstall tcl

# get the modified tcl library (a pull-request that may be unnecessary if we can fix it from python)
brew install https://raw.github.com/scicalculator/homebrew-dupes/fix_tcl_library_path_var/tcl.rb --enable-threads
brew install tk --enable-threads

# get the modified python install with the new option (currently a pull request with a possible need for further revision)
brew install https://raw.github.com/samueljohn/homebrew/341a2961eff7665a4f8c219ab907fdc2c40ba598/Library/Formula/python.rb --with-brewed-tk

# don't have pmw yet? get it here:
brew tap samueljohn/python
brew install pmw

# now you can get pymol up and running like before
brew tap scicalculator/pymol
brew install pymol
```

When all the hubub about getting python working out of the box with
tk-tcl is done and over, this should be good for incorporation into the
[Homebrew/science][hbsci] repository.


[hb]:http://mxcl.github.com/homebrew/
[hbsci]:https://github.com/Homebrew/homebrew-science
[pymol]:http://pymol.org
