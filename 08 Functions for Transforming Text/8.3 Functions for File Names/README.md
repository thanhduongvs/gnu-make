# 8.3 Functions for File Names

1. **$(dir names…)**
- Trả về tên thư mục.
    ```Makefile
    all:
	    @echo $(dir src/main.c inc/main.h inc/common/common.h hacks)
    ```
- Kết quả: 
    ```Bash
    src/ inc/ inc/common/ ./
    ```

2. **$(notdir names…)**
- Trả về tên file name.
    ```Makefile
    all:
	    @echo $(notdir src/main.c inc/main.h inc/common/common.h hacks)
    ```
- Kết quả: 
    ```Bash
    main.c main.h common.h hacks
    ```

3. **$(suffix names…)**
- Trả về tên định dạng của file.
    ```Makefile
    all:
	    @echo $(suffix src/main.c inc/main.h inc/common/common.h hacks)
    ```
- Kết quả: 
    ```Bash
    .c .h .h
    ```

4. **$(basename names…)**
- Kết quả trả về  sẽ bỏ qua định dạng của file.
    ```Makefile
    all:
	    @echo $(basename src/main.c inc/main.h inc/common/common.h hacks)
    ```
- Kết quả: 
    ```Bash
    src/main inc/main inc/common/common hacks
    ```

5. **$(addsuffix suffix,names…)**
- Thêm hậu tố `suffix` vào mỗi `names`.
    ```Makefile
    all:
	    @echo $(addsuffix .c,foo bar src/main)
    ```
- Kết quả: 
    ```Bash
    foo.c bar.c src/main.c
    ```

6. **$(addprefix prefix,names…)**
- Thêm tiền tố `prefix` vào mỗi `names`.
    ```Makefile
    all:
	    @echo $(addprefix src/,foo bar)
    ```
- Kết quả: 
    ```Bash
    src/foo src/bar
    ```

6. **$(join list1,list2)**
- Kết quả trả về sẽ nối `list1`và `list2` theo từng từ 1.
    ```Makefile
    all:
	    @echo $(join a b x,.c .o .s)
    ```
- Kết quả: 
    ```Bash
    a.c b.o x.s
    ```

7. **$(wildcard pattern)**
- Kết quả sẽ trả về  liệt kê danh sách các file có trong thư mục đó.
- Giả sử ta có thư mục như bên dưới:
    ```
    ├── father
    │   ├── son
    │   │   ├── aa.s
    │   │   ├── bb.s
    │   │   └── cc.s
    │   ├── tt.h
    │   ├── uu.h
    │   └── vv.h
    ├── Makefile
    ├── xx.c
    ├── yy.c
    └── zz.c
    ```
- Ta có Makefile như bên dưới:
    ```Makefile
    C_FILE := $(wildcard *.c)
    O_FILE := $(wildcard father/*.o)
    S_FILE := $(wildcard father/son/*.s)

    all:
        @echo -n "C_FILE = "
        @echo $(C_FILE)
        @echo -n "O_FILE = "
        @echo $(O_FILE)
        @echo -n "S_FILE = "
        @echo $(S_FILE)
    ```
- Kết quả: 
    ```Bash
    C_FILE = yy.c zz.c xx.c
    O_FILE = father/vv.o father/tt.o father/uu.o
    S_FILE = father/son/cc.s father/son/bb.s father/son/aa.s
    ```

8. **$(realpath names…) và $(abspath names…)**
- Trả về đường dẫn tuyệt đối của từng file `names`,
- Xem ví dụ bên dưới để thấy được sự khác biệt giữa `realpath` với `abspath`.
- Gõ lệnh `ln -s xx.c xx_link.c`
- Sử dụng lại thư mục bên trên, ta có Makefile như bên dưới:
    ```Makefile
    all:
        @echo $(abspath xx.c)
        @echo $(abspath xx_link.c)
        @echo $(realpath xx.c)
        @echo $(realpath xx_link.c)
    ```
- Kết quả: 
    ```Bash
    /home/vanson/working/gnu-make/xx.c
    /home/vanson/working/gnu-make/xx_link.c
    /home/vanson/working/gnu-make/xx.c
    /home/vanson/working/gnu-make/xx.c
    ```
