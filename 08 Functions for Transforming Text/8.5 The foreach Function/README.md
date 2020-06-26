# 8.5 The foreach Function

**$(foreach var,list,text)**
- Sẽ chuyển đổi mỗi từ trong `list` thành `text`. Trong đó `var` như biến `i` trong vòng lặp for.
    ```Makefile
    foo := who are you
    # For each "word" in foo, output that same word with an exclamation after
    bar := $(foreach wrd,$(foo),$(wrd)!)

    all:
        # Output is "who! are! you!"
        @echo $(bar)
    ```
- Kết quả: 
    ```Bash
    who! are! you!
    ```