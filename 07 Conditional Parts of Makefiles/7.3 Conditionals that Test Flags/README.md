# 7.3 Conditionals that Test Flags
- Chạy Makefile bên dưới với lệnh `make -i`
    ```Makefile
    bar =
    foo = $(bar)

    all:
    # Search for the "-i" flag. MAKEFLAGS is just a list of single characters, one per flag.
    # So look for "i" in this case.
    ifneq (,$(findstring i, $(MAKEFLAGS)))
        echo "i was passed to MAKEFLAGS"
    endif
    ```
- Kết quả: 
    ```Bash
    echo "i was passed to MAKEFLAGS"
    i was passed to MAKEFLAGS
    ```