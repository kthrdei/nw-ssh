# nw-ssh
Simple ssh client with asyncssh for network devices.

```
import asyncio
from nw_ssh import connection

async def main():
    async with connection.SSHConnection(
            host='169.254.0.1',
            port=22,
            username='root',
            password='password',
            client_keys=[],
            passphrase=None,
            known_hosts_file=None,
            delimiter=r'#',
            timeout=10) as conn:

        print(conn.login_message)

        output = await conn.send(input='cli', delimiter=r'>')
        print(output)

        output = await conn.send(input='show interfaces fxp0 | no-more', delimiter=r'>')
        print(output)

        output = await conn.send(input='configure', delimiter=r'#')
        print(output)

        output = await conn.send(input='show interfaces', delimiter=r'#')
        print(output)

        output = await conn.send(input='commit', delimiter=r'#', timeout=10)
        print(output)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```


# License
MIT

