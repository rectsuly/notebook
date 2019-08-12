# pyenv install 3.6.6 - zipimport.ZipImportError: can't decompress data; zlib not available

> macOS + Homebrew + Pyenv

## Issue

```shell
$ pyenv install 3.6.6
python-build: use openssl from homebrew
python-build: use readline from homebrew
Installing Python-3.6.6...
python-build: use readline from homebrew

BUILD FAILED (OS X 10.14 using python-build 20180424)

Inspect or clean up the working tree at /var/folders/9s/4dz5cwfj0dv6j_1_k8nlnd5m0000gn/T/python-build.20181028140503.9082
Results logged to /var/folders/9s/4dz5cwfj0dv6j_1_k8nlnd5m0000gn/T/python-build.20181028140503.9082.log

Last 10 log lines:
  File "/private/var/folders/9s/4dz5cwfj0dv6j_1_k8nlnd5m0000gn/T/python-build.20181028140503.9082/Python-3.6.6/Lib/ensurepip/__main__.py", line 5, in <module>
    sys.exit(ensurepip._main())
  File "/private/var/folders/9s/4dz5cwfj0dv6j_1_k8nlnd5m0000gn/T/python-build.20181028140503.9082/Python-3.6.6/Lib/ensurepip/__init__.py", line 204, in _main
    default_pip=args.default_pip,
  File "/private/var/folders/9s/4dz5cwfj0dv6j_1_k8nlnd5m0000gn/T/python-build.20181028140503.9082/Python-3.6.6/Lib/ensurepip/__init__.py", line 117, in _bootstrap
    return _run_pip(args + [p[0] for p in _PROJECTS], additional_paths)
  File "/private/var/folders/9s/4dz5cwfj0dv6j_1_k8nlnd5m0000gn/T/python-build.20181028140503.9082/Python-3.6.6/Lib/ensurepip/__init__.py", line 27, in _run_pip
    import pip._internal
zipimport.ZipImportError: can't decompress data; zlib not available
make: *** [install] Error 1
```

## Fix

### Install zlib

```
brew install zlib
```

### Add the following to your `~/.zshrc` (if you use zsh)

> the following content partly from the output of `brew install zlib`

DO NOT FORGET TO ADD `${LDFLAGS}`, `${CPPFLAGS}`, `${PKG_CONFIG_PATH}`!

```shell
# For compilers to find zlib you may need to set:
export LDFLAGS="${LDFLAGS} -L/usr/local/opt/zlib/lib"
export CPPFLAGS="${CPPFLAGS} -I/usr/local/opt/zlib/include"

# For pkg-config to find zlib you may need to set:
export PKG_CONFIG_PAGH="{PKG_CONFIG_PATH} /usr/local/opt/zlib/lib/pkgconfig"
```

## Other solution

You don't need to add anything permanently to your dotfiles, the flags just need to be set during compile time. So just set the environment variables in your shell session. This worked for me:

```shell
$ brew install zlib
$ brew install sqlite
$ export LDFLAGS="${LDFLAGS} -L/usr/local/opt/zlib/lib"
$ export CPPFLAGS="${CPPFLAGS} -I/usr/local/opt/zlib/include"
$ export LDFLAGS="${LDFLAGS} -L/usr/local/opt/sqlite/lib"
$ export CPPFLAGS="${CPPFLAGS} -I/usr/local/opt/sqlite/include"
$ export PKG_CONFIG_PATH="${PKG_CONFIG_PATH} /usr/local/opt/zlib/lib/pkgconfig"
$ export PKG_CONFIG_PATH="${PKG_CONFIG_PATH} /usr/local/opt/sqlite/lib/pkgconfig"
$ pyenv install 3.6.8
```



