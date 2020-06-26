# 7.2 Syntax of Conditionals

1. **ifeq (arg1, arg2)**
- Nếu arg1 = arg2.
    ```Makefile
    libs_for_gcc = -lgnu
    normal_libs = normal

    ifeq ($(CC),gcc)
        libs = $(libs_for_gcc)
    else
        libs = $(normal_libs)
    endif

    all:
        @echo $(libs)
    ```
- Kết quả: 
    ```Bash
    normal
    ```

2. **ifneq (arg1, arg2)**
- Nếu arg1 != arg2.
    ```Makefile
    libs_for_gcc = -lgnu
    normal_libs = normal

    ifneq ($(CC),gcc)
        libs = $(libs_for_gcc)
    else
        libs = $(normal_libs)
    endif

    all:
        @echo $(libs)
    ```
- Kết quả: 
    ```Bash
    -lgnu
    ```

3. **ifdef variable-name**
- Nếu đã định nghĩa biến `variable-name`
    ```Makefile
    bar = true
    foo = bar
    ifdef $(foo)
        frobozz = yes
    else
        frobozz = false
    endif

    all:
        @echo $(frobozz)
    ```
- Kết quả: 
    ```Bash
    yes
    ```

4. **ifndef variable-name**
- Nếu chưa định nghĩa biến `variable-name`
    ```Makefile
    bar = true
    #foo = bar
    ifndef $(foo)
        frobozz = yes
    else
        frobozz = false
    endif

    all:
        @echo $(frobozz)
    ```
- Kết quả: 
    ```Bash
    yes
    ```
