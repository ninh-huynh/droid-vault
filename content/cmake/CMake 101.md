## Config project

```shell
cmake -S <source_dir> -B <build_dir>
```

### Override make program

```shell
cmake -S <source_dir> -B <build_dir> -DCMAKE_MAKE_PROGRAM=<path_to_ninja>
```

### Override cpp flag

```shell
cmake -S <source> -B <build_dir> -DCMAKE_CXX_FLAGS="-std=c++11"
cmake -S <source> -B <build_dir> -DCMAKE_CXX_STANDARD=11
```

### Override custom variable

```shell
cmake -S <source> -B <build_dir> -D MY_VARIABLE=foo
``` 

### Override install prefix

```shell
cmake -S <source> -B <build_dir> -DCMAKE_INSTALL_PREFIX=./install_dir
```


## Build project

```shell
cmake --build <build_dir>
```

Install project

```shell
cmake --install <build_dir>
```