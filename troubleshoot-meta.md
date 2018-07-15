# Troubleshoot MeTa


## Fatal error: xlocale.h: No such file or directory

Excute:

```
make
```

Got:

```
/meta/build/meta/deps/icu-58.2/src/ExternalICU/source/i18n/digitlst.cpp:67:13: fatal error: xlocale.h: No such file or directory
 #   include <xlocale.h>
             ^~~~~~~~~~~
compilation terminated.

```

### Solution

Run this inside `build` directory:

```
sed -i 's/xlocale/locale/' deps/icu-58.2/src/ExternalICU/source/i18n/digitlst.cpp
```

And than re-execute building process:

```
make
```


## Terminate called after throwing an instance of 'meta::index::inverted_index_exception'

Execute:

```
../../meta/build/index ../config.toml
```

Got:

```
terminate called after throwing an instance of 'meta::index::inverted_index_exception'
  what():  index name missing from configuration file
Aborted (core dumped)
```

### Solution

1. Open `config.toml`.

2. Comment `forward-index` and `inverted-index`.

3. Add `index` key with appropriate value, such that:

    ```
    # forward-index = "moocs-fwd"
    # inverted-index = "moocs-inv"
    index = "moocs"
    ```