# socket_pair
The socketpair() call creates an unnamed pair of connected sockets in the specified domain, of the specified type, and using the optionally specified protocol.

模拟linux的socketpair函数实现跨平台的socketpair实现，支持单listen生成多个accept

```
#include "socket_pair.h"

int main() {
    SOCKET fd[2];
    uint64_t handle;
    handle = SocketPair::instance()->create_pair(fd);
    if (handle == 0) {
        // fail
        SocketPair::release();
        return -1;
    }

    send(fd[0], ...);    
    recv(fd[0], ...);

    send(fd[1], ...);
    recv(fd[1], ...);

    SocketPair::instance()->delete_pair(handle);

    SocketPair::release();
    return 0;
}

```