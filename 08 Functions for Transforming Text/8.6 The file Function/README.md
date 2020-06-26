# 8.6 The file Function

**$(file op filename[,text])**
- Trong đó `op`:
  - `>`: viết đè lên file
  - `>>`: thêm dòng mới vào ở cuối file
  - `<`: đọc file

    ```Makefile
    name := thanh.txt

    all: read
        @echo "done"

    read: write_appended
        text := $(file < $(name))
        @echo "read file $(text)"

    write_appended: write
        @echo "write appended to file $(name)"
        $(file >> $(name),"van son")

    write: create
        @echo "write to file $(name)"
        $(file > $(name),"thanh duong")

    create:
        @echo "create file $(name)"
        touch $(name)
    ```
- Kết quả: 
    ```Bash
    create file thanh.txt
    touch thanh.txt
    write to file thanh.txt
    write appended to file thanh.txt
    text := "thanh duong"
    ```