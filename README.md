# MSP libc printf/sprintf implementation

This is a small implementation of printf/sprintf family of functions taken from MSP libc library. It has built-in conversion code but it is not a standalone implementation. It depends on some libc functions and headers.

- strlen
- stdlib.h
- stdbool.h
- stdarg.h
- string.h
- stdint.h
- limits.h
- stdio.h
- features.h


### Compile time options


| Option name                            | Description  |
|----------------------------------------|--------------|
| MSP_PRINTF_ENABLE_LONGLONG | Enable support for 64-bit long long int. |
| MSP_PRINTF_ENABLE_LONG | Enable support for 32-bit long int. |
| PRINTF_USE_MSP | Enable standard libc function names as aliases to msp_* functions |


### Implemented functions

All functions have the same signature as in the libc (except the msp_ prefix and  non-standard function init_msp_printf):
```
void init_msp_printf(int (*putf) (int));
int msp_puts (const char *s);
int msp_vuprintf (void* outp, int (*write_char)(void*, int), const char *format, va_list args);
int msp_vprintf (const char *fmt, va_list argp);
int msp_vsprintf (char *buf, const char *fmt, va_list argp);
int msp_vsnprintf (char *buf, size_t size, const char *fmt, va_list argp);
int msp_uprintf (int (*func) (int c), const char *fmt, ...);
int msp_printf (const char *fmt, ...);
int msp_sprintf (char *buf, const char *fmt, ...);
int msp_snprintf (char *buf, size_t size, const char *fmt, ...);
```
Note that you first have to call `init_msp_printf()` to set I/O callback function like `putchar()` that will be used for actual printing.

### Standard libc function names

If you define compile time symbol PRINTF_USE_MSP all functions will we visible as the standard library's names, without msp_ prefix.


