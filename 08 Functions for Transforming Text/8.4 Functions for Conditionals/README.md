# 8.4 Functions for Conditionals

1. **$(if condition,then-part[,else-part])**
- Xem cách dùng bên dưới.
    ```Makefile
    foo := $(if this-is-not-empty,then!,else!)
    empty :=
    bar := $(if $(empty),then!,else!)

    all:
        @echo $(foo)
        @echo $(bar)
    ```
- Kết quả: 
    ```Bash
    then!
    else!
    ```

2. **$(or condition1[,condition2[,condition3…]])**
- Xem cách dùng bên dưới.
    ```Makefile
    LINUX_TARGET := 2
    OSX_TARGET := 0
    WIN_TARGET := 0
    all:
        @echo $(or $(LINUX_TARGET),$(OSX_TARGET))
        @echo $(or $(WIN_TARGET),$(OSX_TARGET))
    ```
- Kết quả: 
    ```Bash
    2
    0
    ```

3. **$(and condition1[,condition2[,condition3…]])**
- Xem cách dùng bên dưới.
    ```Makefile
    LINUX_TARGET := 2
    OSX_TARGET := 1
    WIN_TARGET := 0
    all:
        @echo $(and $(LINUX_TARGET),$(OSX_TARGET))
        @echo $(and $(WIN_TARGET),$(OSX_TARGET))
    ```
- Kết quả: 
    ```Bash
    1
    0
    ```
