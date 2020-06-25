# 8.2 Functions for String Substitution and Analysiss

1. **$(subst from,to,text)**

- Hàm `subst` dùng để tìm trong chuỗi **text** có chuỗi **from** không, nếu có thì thay thế chuỗi **from** thành chuỗi **to**.  
Ví dụ: `$(subst ee,EE,feet on the street)` thì kết quả trả về là `fEEt on the strEEt`.

    ```Makefile
    from := ee
    to := EE
    foot := feet on the street
    bar := $(subst $(from),$(to),$(foot))
    all:
        @echo "(subst $(from), $(to),$(foot))"
        @echo "result $(bar)"
    ```
- Kết quả: 
    ```Bash
    (subst ee, EE,feet on the street)
    result fEEt on the strEEt
    ```

2. **$(patsubst pattern,replacement,text)**

    ```Makefile
    C_BIN := $(patsubst %.c, %.bin, xx.c yy.c zz.c)
    O_BIN := $(patsubst father/%.o,%.bin, father/tt.o father/uu.o father/vv.o)
    S_BIN := $(patsubst mom/son%.s,%.bin, mom/son/aa.s mom/son/bb.s mom/son/cc.s)

    all:
        @echo -n "C_BIN = "
        @echo $(C_BIN)
        @echo -n "O_BIN = "
        @echo $(O_BIN)
        @echo -n "S_BIN = "
        @echo $(S_BIN)
    ```
- Kết quả: 
    ```Bash
    C_BIN = xx.bin yy.bin zz.bin
    O_BIN = tt.bin uu.bin vv.bin
    S_BIN = /aa.bin /bb.bin /cc.bin
    ```

3. **$(strip string)**
- Hàm `strip` dùng để loại bỏ khoảng trắng
    ```Makefile
    TXT := "     a b    c d e"

    all:
        @echo "$(TXT)"
        @echo "result: dda$(strip $(TXT))b"
    ```
- Kết quả: 
    ```Bash
    a b c d e
    result: dda a b c d eb
    ```

4. **$(findstring find,in)**
- Tìm sự xuất hiện của chuỗi **find** trong chuỗi **in**. Nếu tìm được chuỗi *find* trong *in* thì kết quả trả về là `find`, còn tìm không được kết quả trả về là rỗng.
    ```Makefile
    all:
        @echo "find: $(findstring main.c, main.h bar.c main.c)"
        @echo "find: $(findstring main.h, main.h bar.c main.h main.c)"
        @echo "find: $(findstring main, foot bar)"
    ```
- Kết quả: 
    ```Bash
    find: main.c
    find: main.h
    find:
    ```

5. **$(filter pattern…,text)**
- Tìm sự xuất hiện của chuỗi **pattern** trong chuỗi **text**. Nếu tìm được chuỗi *pattern* trong *text* thì kết quả trả về là `pattern`
    ```Makefile
    src := foot.c bar.c baz.s ugh.h
    foot := $(filter %.c %.s, $(src))
    bar := $(filter bar.c, $(src))
    all:
        @echo $(foot)
        @echo $(bar)
    ```
- Kết quả: 
    ```Bash
    foot.c bar.c baz.s
    bar.c
    ```

6. **$(filter-out pattern…,text)**
- Trả về kết quả là ngoại trừ *pattern* trong *text*
    ```Makefile
    obj = main1.o foo.o main2.o bar.o thanh.o
    main = main1.o main2.o

    all:
        @echo $(filter-out $(main), $(obj))
    ```
- Kết quả: 
    ```Bash
    foo.o bar.o thanh.os
    ```

7. **$(sort list)**
- Sắp xếp chuỗi theo thứ tự abc.
    ```Makefile
    all:
        @echo $(sort foo bar lose)
        @echo $(sort foot bar lose foot)
    ```
- Kết quả: 
    ```Bash
    bar foo lose
    bar foot loses
    ```

8. **$(word n,text)**
- Trả về từ thứ `n` xuất hiện trong `text`.
    ```Makefile
    all:
	    @echo $(word 2, one foo bar baz haha)
    ```
- Kết quả: 
    ```Bash
    foo
    ```

9. **$(wordlist s,e,text)**
- Trả về danh sách từ trong chuỗi `text` bắt đầu từ vị trí `s` đến `e`
    ```Makefile
    all:
	    @echo $(wordlist 2, 5, foo bar baz txt vim bash)
    ```
- Kết quả: 
    ```Bash
    bar baz txt vim
    ```

10. **$(words text)**
- Trả về số lượng từ trong text
    ```Makefile
    txt = "van son thanh duong vs"
    wrd = $(words $(txt))
    all:
        @echo $(wrd)
    ```
- Kết quả: 
    ```Bash
    5
    ```

11. **$(firstword names…)**
- Trả về chuỗi đầu tiên cùng xuất hiện.
    ```Makefile
    all:
        @echo $(firstword foo bar baz)
    ```
- Kết quả: 
    ```Bash
    foo
    ```

12. **$(lastword names…)**
- Trả về chuỗi cuối cùng xuất hiện.
    ```Makefile
    all:
        @echo $(lastword foo bar baz)
    ```
- Kết quả: 
    ```Bash
    baz
    ```
