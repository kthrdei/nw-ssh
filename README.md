# nw-ssh
Simple ssh client with asyncssh for network devices.

```
import asyncio
import nw_ssh

async def main() -> None:
    async with nw_ssh.SSHConnection(
        host='169.254.0.1',
        port=22,
        username='root',
        password='password',
        client_keys=[],
        passphrase=None,
        known_hosts_file=None,
        delimiter=r'#',
        timeout=10,
    ) as conn:

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

asyncio.run(main())
```

# Requirements
- Python >= 3.7
- asyncssh


# Installation
```
pip install nw-ssh
```


# License
MIT
