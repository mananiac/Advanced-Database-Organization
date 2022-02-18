.PHONY: all
all: test_assign1

test_assign1: test_assign1_1.c storage_mgr.c dberror.c
	gcc -o test_assign1 test_assign1_1.c storage_mgr.c dberror.c 

.PHONY: clean
clean:
	rm -rf test_assign1 *.o