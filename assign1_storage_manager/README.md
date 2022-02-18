# ********** SPRING 2022 - 1ST ASSIGNMENT - STORAGE MANAGER ********** #

#  GROUP MEMBER INFO #

    1. KOMAL BODHANKAR - A20492705 - kbodhankar@hawk.iit.edu
    2. MANAN SAGAR - A20496941 - msagar@hawk.iit.edu
    3. RAVISHANKAR SIVAGNANAM - A20503091 - rsivagnanam@hawk.iit.edu

# ********************************************************************* #

# Files in the storage manager #

###  1. C files:
 > - storage_mgr.c
 > - storage_mgr.h
 > - test_assign1.c
###  2. Header files
 > - test_helper.h
 > - dberror.c
 > - dberror.h
###   3. Makefile
###   4. README

# ********************************************************************* #

# STEPS TO START THE SCRIPT #

0. Start the Linux system
1. Open terminal and go to the project root
2. We can run the `ls` command to view the files to ensure if we are in the right directory
3. Then we run the command `make clean` to clean the preexisting output files
4. To execute the file, we then run the `make` or the `makeall` command.

After we execute the 4th step, a new file named `test_assign1_1.c` will be generated.

5. Run the `./test_assign1_1` command to run the newly generated file. 


# ********************************************************************* #

# FUNCTION DESCRIPTIONS: #

1.  Functions that will manipulate the file pages like creating, opening, closing and destroying 
 
    a. createPageFile():
       > - This function will create a new page. Only one page will be the starting size of the page. The page will be filled by '0' bytes.
       > - fopen() function in C enables read and the write operations 
    
    b. openPageFile():
       > - This function will open a page file that is already existing. If the file does not exist, ' RC_FILE_NOT_FOUND ' will be returned. 
       > - The second argument that the function takes is the existing file handle. 
       > - If the file is opened, the informtion of the file must be initialized in the fields of the file manager. 
       > - To enable read only operations, we use the fopen() function in r mode. 
       > - It also calculates the total pages and stres them. Also the current page position and name of the file is stored. 

    c. closePageFile():
       > - It will close the file with the fclose() function 
       > - RC_OK will be returned if the operation of closing the file is successful and RC_FILE_NOT_FOUND if it is not successful. 

    d.  destroyPageFile():
       > - The remove function will be used to  delete the file
       > - RC_OK will be returned if the operation of destroying the file is successful and RC_FILE_NOT_FOUND if it is not successful. 


2.  Functions that will be used to read the blocks from the disc

    a. readBlock():
       > - We check if the page already exists
       > - Then fseek is used to set the pointer of the file if the page already exists
       > - fread is then used to read the file and allocate the position of the current page to the recently read page

    b. getBlockPos():
       > - fhandle is used to return the current position of the page

    c. readFirstBlock():
       > - If we find that the value of fhandle is not NULL, and the value of total pages is more than 0, then the first block is read

    d. readPreviousBlock():
       > - If the value of fhandle is not found to be NULL,  the pointer value is set towards the previous page or else an error will be displayed.
       > - If the preceding block does not fall within the bracket of the page limit, then an error is thrown.
       > - If the  preceding block is well within the page limit bracket, then it is read and the current position of the page is updated by reducing the value by 1. 

    e. readCurrentBlock():
       > - If the value of fhandle is not NULL, then the current page is called by getBlockPos()
       > - fhandle is used to read the present file

    f. readNextBlock():
       > - If the value of fhandle is not NULL, then pointer position is updated by increasing the current value by 1. 
       > - The next block contents are read

    g. readLastBlock():
       > - If fhandle is not NULL, then the pointer position is allocated towards the last page
       > - fread is used to read the last page contents

3.  Functions that will be used to write the blocks for a page file

    a. writeBlock():
       > - It will check if pageNum is larger than the total number of pages or not. If it is, then an error will be thrown and check if the fhandle is empty.
       > - The write function is executed when we have to write on the condition than fhandle is not NULL
       > - totalNumPages is updated by 1

    b. writeCurrentBlock():
       > -getBlockPos() is used for getting the current block. 
       > -writeBlock() is used for writing at the current block
       > - If successful, RC_OK is returned else RC_WRITE_FAILED

	c. appendEmptyBlock():
       > - It is checked if the file is available or not available and if it is, it can be opened in the read mode. Then fseek is used to set the file pointer to the end
       > - File handle variable is updated after writing an enpty block

    d. ensureCapacity():
       > - It will check if the new size is  is larger than the current size
       > - If it is, the pages are added using appendEmptyBlock()


# ********************************************************************* #

*An error message will be provided whenever we encounter an error which will be envoked from the dberror.c file*    