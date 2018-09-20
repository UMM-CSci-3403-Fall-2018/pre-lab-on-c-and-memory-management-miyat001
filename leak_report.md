# Leak report
==19791==     in use at exit: 46 bytes in 6 blocks
==19791==   total heap usage: 7 allocs, 1 frees, 1,070 bytes allocated

 46 bytes in 6 blocks are definitely lost in loss record 1 of 1
==19831==    at 0x4C2FB55: calloc (in /usr/lib/valgrind/vgpreload_memcheck-amd64-linux.so)
==19831==    by 0x400708: strip (check_whitespace.c:41)
==19831==    by 0x400773: is_clean (check_whitespace.c:62)
==19831==    by 0x40080A: main (check_whitespace.c:87)

46 bytes are lost. It is allocated by calloc. The predictable leaked codes are 41, 62, 87.
The memory leak happen because the calloc keeps(allocate) the memory for string.
I need to release the memory on the last function that is handed the value from calloc. 
In this case, "is_clean" is the last function. However,when I write "free()" in "is_clean", I get error from program.
Therefore, I write "free()" in char*strip function.

I added free(result) to code.




_Use this document to describe whatever memory leaks you find in `clean_whitespace.c` and how you might fix them. You should also probably remove this explanatory text._

