---
title: Pythonhook
date: 2024-07-05T21:41:20+08:00
lastmod: 2024-07-05T21:41:20+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - category1
tags:
  - tag1
  - tag2
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
# python hook

```python
# -*- coding: utf-8 -*-

import sys
import types
from pathlib import Path
from importlib.machinery import ModuleSpec
from importlib.abc import MetaPathFinder, Loader
# sys.path.insert(0, 'module')


class DynamicLoader(Loader):
    def __init__(self, path):
        self.__path = path

    def create_module(self, spec):
        module = types.ModuleType(spec.name)
        return module

    def exec_module(self, module):
        print(self.__path)
        source = self.__path.read_bytes()
        exec(source, module.__dict__)


class DynamicFinder(MetaPathFinder):
    base_path = Path('module')

    def find_spec(self, fullname, path, target=None):
        if fullname in sys.modules: 
            return sys.modules[fullname]
        if self.base_path.joinpath(f'{fullname}.py').exists():
            abs_path = self.base_path / f'{fullname}.py'
        elif self.base_path.joinpath(fullname, '__init__.py').exists():
            abs_path = self.base_path / fullname / '__init__.py'
        else:
            return None
        return ModuleSpec('msg', DynamicLoader(abs_path))


def dynamic_hook(path):
    return DynamicFinder()


sys.meta_path.append(DynamicFinder())

#sys.path_hooks = [dynamic_hook]
sys.path_importer_cache.clear()


if __name__ == '__main__':
    import msg
    print(msg.message(sys.argv[1]))
```