# 7.2 Syntax of Conditionals

1. **ifeq (arg1, arg2)**
- Nếu arg1 = arg2.
    ```Makefile
    foo = ok

    all:
    ifeq ($(foo), ok)
        @echo "foo equals ok"
    else
        @echo "nope"
    endif
    ```
- Kết quả: 
    ```Bash
    foo equals ok
    ```

2. **ifneq (arg1, arg2)**
- Nếu arg1 != arg2.
    ```Makefile
    foo = nope

    all:
    ifneq ($(foo), ok)
        @echo "foo not equals ok"
    else
        @echo "nope"
    endif
    ```
- Kết quả: 
    ```Bash
    foo not equals ok
    ```

3. **ifdef variable-name**
- Nếu đã định nghĩa biến `variable-name`
    ```Makefile
    bar =
    foo = $(bar)

    all:
    ifdef foo
        @echo "foo is defined"
    endif
    ifdef bar
        @echo "but bar is not"
    endif
    ```
- Kết quả: 
    ```Bash
    foo is defined
    ```

4. **ifndef variable-name**
- Nếu chưa định nghĩa biến `variable-name`
    ```Makefile
    bar =
    foo = $(bar)

    all:
    ifndef foo
        @echo "foo is defined"
    endif
    ifndef bar
        @echo "but bar is not"
    endif
    ```
- Kết quả: 
    ```Bash
    but bar is not
    ```
5. **Check if a variable is empty**
- Xem ví dụ bên dưới:
    ```Makefile
    nullstring =
    foo = $(nullstring) # end of line; there is a space here

    all:
    ifeq ($(strip $(foo)),)
        @echo "foo is empty after being stripped"
    endif
    ifeq ($(nullstring),)
        @echo "nullstring doesn't even have spaces"
    endif
    ```
- Kết quả: 
    ```Bash
    foo is empty after being stripped
    nullstring doesn't even have spaces
    ```