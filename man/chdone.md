# NAME

chdone - mark the channel as closed

# SYNOPSIS

```c
#include <libdill.h>
int chdone(int ch);
```

# DESCRIPTION

This function is used to let all the users of the channel, that there will be no new messages on the channel, ever.

After `chdone` is called, all attempts to `chsend` or `chrecv` on the channel will fail with `EPIPE` error.

# RETURN VALUE

The function returns 0 in case of success. In case of failure it returns -1 and sets `errno` to one of the following values.

# ERRORS

* `EBADF`: Not a valid handle.
* `ENOTSUP`: Operation not supported. Presumably, the handle isn't a channel.
* `EPIPE`:  `chdone` was already called for this channel.

# EXAMPLE

```c
int result = chdone(ch);
if(result != 0) {
    perror("Channel cannot be terminated");
    exit(1);
}
printf("Channel successfully terminated.\n", val);
```

