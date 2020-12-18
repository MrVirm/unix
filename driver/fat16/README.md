# FAT16 driver


## Build instructions

```sh
$ make
```
This creates a shared library ```libfat16_driver.so``` in the ```lib``` folder.
The test suite must be run as root:

```sh
$ sudo ./bin/run_test
```

## Examples

Printing content of a file:
```c
void print_file_content(void)
{
    int fd = fat16_open("DATA.TXT", 'r');
    if (fd < 0) {
        fprintf(stderr, "Failed to read DATA.TXT\n");
        return;
    }

    while (1) {
        char buffer[256];
        int i, n;
        n = fat16_read(fd, buffer, sizeof(buffer));
        if (n == 0) {   /* End of file reached */
            break;
        } else if (n < 0) {
            fprintf(stderr, "Error %d while reading\n", -n);
            break;
        } else {
            for (i = 0; i < n; ++i)
                printf("%c", buffer[i]);
        }
    }

    fat16_close(fd);
}
```

Listing files in root directory:
```c
void list_files(void)
{
    char filename[13];
    uint32_t i = 0;
    while(fat16_ls(&i, filename, "/") == 1) {
        printf("%s\n", filename);
    }
}
```
