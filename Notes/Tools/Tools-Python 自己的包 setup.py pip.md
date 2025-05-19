

```
from setuptools import setup
import setuptools

setup(
    name="datautils",
    version="0.1.0",
    description="数据工具库",
    author="yangyu",
    author_email="your.email@example.com",
    packages=setuptools.find_packages(),
)

```

`python setup.py test`

`pip setup.py check`

`python setup.py sdist`
`pip install xxx.tar.gz`