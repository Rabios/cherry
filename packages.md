# Working with packages in cherry

### Creating a package

To create a cherry package for example, Simply type `cherry new directory`.

Cherry will ask if your package is app, The difference is packages that serves as apps can't installed to projects/packages as libraries (Except by editing properties and this will explained in next sections).

### Installing a package to project/package

To install package to project/package, Simply type:

```
cherry get package-user/package-repo-name dir
```

> In this case, You would asked for direct installation and if so on, Input directory of installation when asked for, Else package will left downloaded in it's directory.

You can also set channel and branch, For example:

```
cherry get package-user/package-repo-name dir master github
```

> Channels available: `github`, `gitlab`, `bitbucket`, `mercurial`, Note that channels other than GitHub channel not tested yet!

### Removing a package

If a you installed package in package you made and it's valid you can remove it, Simply type `cherry remove package-name package-dir`.

Or if installed package is in folder... Use `cherry uninstall package-dir` to remove package.

### Running a package

If your package is app then simply run package by typing `cherry run package-directory`

Then package will runs if it's app from config.

> If package is not app then returns error but doesn't manipulates anything.

### Editing package properties

If you are creating or adding new files or you want to distribute your package over repository hosting website such as GitHub, You might need to edit properties of package in file named `.cherry`.

Here is what you find when you open an not edited package info:

```lua
return {
  _NAME = "package-name",
  _URL = "https://github.com/user/package-repo",
  _LICENSE = "package-license",
  _CODENAME = "package-codename",
  _AUTHOR = "package-author",
  _VERSION = "package-version-string",
  _BRANCH = "master",
  _APP = false,
  description = [[
    package-description
  ]],
  package = {
    src = {
	    "test.lua"
	  },
	  main = "test.lua",
  }
}
```

#### Required properties

- `_NAME` (string): Name of package.
- `_URL` (string): online site of package (Or repo link)
- `_AUTHOR` (string): Author of package.
- `_LICENSE` (string): License type.
- `_VERSION` (string): Version of package.
- `_CODENAME` (string): Codename of package.
- `_BRANCH` (string): Branch of package repository.
- `_APP` (bool): If package is app or library.
- `description` (string): Description of package.
- `package.src` (table): Table contains Lua files paths from package directory.
- `package.main` (string): Main file that can be run if package is app.

#### Optional properties

- `_LUA` (number): Lua version limit for package.
- `_CHERRY` (number): Cherry version limit for package.
- `_ARCH` (string): package architecture, `global` for all or a string possible to get via `ffi.arch`.
- `_OS` (string): package operating system, `global` for all or a string possible to get via `ffi.os`.
- `package.shared` (table): Table contains dll/dylib/so/lib/o/a files paths from package directory (In case you do bindings).
- `package.resources` (table): Table contains paths to any files that has other types than used by `package.src` and `lib.shared` and `lib.main`
- `package.dependencies` (table): Table contains dependencies (Packages that is downloaded and installed from internet)
- `package.licenses` (table): Table contains paths to licenses files.
- `package.readme` (string): README file.
- `package.external_files` (table): Single files downloaded and installed from internet!
- `package.on_install` (string/function): string to be executed by system or function to be called once package is installed.

### Distribution of package

Simply you can upload source as repository on GitHub and so it gets installed.
