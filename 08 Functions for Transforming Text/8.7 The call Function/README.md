# 8.7 The call Function

**$(call variable,param,param,…)**
- Sets each of the params as $(1), $(2), etc. $(0) is set as the variable name
    ```Makefile
    sweet_new_fn = Variable Name: $(0) First: $(1) Second: $(2) Empty Variable: $(3)

    all:
        # Outputs "Variable Name: sweet_new_fn First: go Second: tigers Empty Variable:"
        @echo $(call sweet_new_fn, go, tigers)
    ```
- Kết quả: 
    ```Bash
    Variable Name: sweet_new_fn First: go Second: tigers Empty Variable:
    ```