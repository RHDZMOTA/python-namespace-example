# Python Namespace Packages: A simple example

This repo contains a very simple example demonstrating the usage of
python namespace packages.

**What is a python namespace package?** In short, it just like a python module
but without an `__init__.py` file. This tells python that you intend to create
a namespace package and allow you to share the "module name" with different
python packages!

You can read more about namespace packages [here](https://packaging.python.org/guides/packaging-namespace-packages/).

## Example: Description

For this example, we have 2 python packages:
* `package-1`: Contains a `hello_world.py` python module.
* `package-2`: Contains a `hola_mundo.py` python module.

These two packages share a common namespace: `my_package`

This means that to access the respective `hello_world` and `hola_mundo` you have to
go through the same namespace:

```python
from my_package import hello_world
from my_package import hola_mundo
```

You can test it out, but first install the modules:
* `pip install -e package-1`
* `pip install -e package-2`

Now run the `test-namespace.py` script!

```commandline
python test-namespace.py
```

You should see a `Hello, world!` and `¡Hola, mundo!` in your terminal!


## How does this works?

Notice the `package-1` and `package-2` directory structure: 

```text
package-1
├── setup.py
└── src
    └──  my_package
        └── hello_world.py
```

```text
package-2
├── setup.py
└── src
    └──  my_package
        └── hola_mundo.py
```

Both are independent modules, but share the `my_package` directory. By using the `setuptools.find_namespace_packages` 
function in the `setup.py`, Python is able to identify the `my_package` directory as a namespace package. 

Of course, you can have `package-1` without `package-2` and vice-verse. But once installed, the submodules from both
packages will share a common namespace.
