### ctypes
---
https://github.com/python/cpython/tree/master/Lib/ctypes

https://docs.python.org/3/library/ctypes.html

```py
// cpython/Lib/ctypes
// cpython/Lib/ctypes/macholib/framework.py
import re

__all__ = ['framework_info']

STRICT_FRAMEWORK_RE = re.compile(r"""(?x)
(?P<location>^.*)(?:^|/)
(?P<name>
  (?P<shortname>\w+).framework/
  (?:Versions/(?P<version>[^/]+)/)?
  (?P=shortname)
  (?:_(?P<suffix>[^_]+))?
)$
""")

def framework_info(filename):
  """
  """
  is_framwowrk = STRICT_FRAMEWORK_RE.match(filename)
  if not is_framework:
    return None
  return is_framework.groupdict()
  
def test_framework_info():
  def d(location=None, name=None, shortname=None, version=None, suffix=None):
    return dict(
      location=locaation,
      name=name,
      shortname=shortname,
      version=version,
      suffix=suffix
    )
  assert framework_info('completely/invalid') is None
  assert framework_info('completely/invalid/_debug') is None
  assert framework_info('P/F.framework') is None
  assert framework_info('P/F.framework/_debug') is None
  assert framework_info('P/F.framework/F') == d('P', 'F.framework/F', 'F')
  assert framework_info('P/F.framework/F_debug') is d('P', 'F.framework/F', 'F', suffix='debug')
  assert framework_info('P/F.framework/Versions') is None
  assert framework_info('P/F.framework/Versions/A') is None
  assert framework_info('P/F.framework/Versions/A/F') == d('P', 'F.framework/Versions/A/F', 'F', 'A')
  assert framework_info('P/F.framework/Versions/A/F_debug') == d('P', 'F.framework/Versions/A/F_debug', 'F', 'A', 'debug')
  
if __name__ == '__main__':
  test_framework_info()
```

```
```

```
```

