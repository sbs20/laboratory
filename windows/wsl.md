# Windows subsystem for Linux

## Log in as root
If you foobar sudoers by being a wally, then in a command prompt:

```
ubuntu config --default-user root
```

Start bash, repair sudoers (or whatever) then configure back

```
ubuntu config --default-user {your_user}
```

[Reference](https://docs.microsoft.com/en-us/windows/wsl/user-support)

If you are on a later version and see `'ubuntu' is not recognized as an
internal or external command, operable program or batch file.` then you may
have installed a later version and something like this will work...

```
ubuntu1804 config --default-user {your_user}
```

You'll find out where ubuntu (or your distro) is installed somewhere in
`%USERPROFILE%\AppData\Local\Microsoft\WindowsApps`.

[Reference](https://github.com/Microsoft/WSL/issues/2586)

## Windows interoperability

https://docs.microsoft.com/en-us/windows/wsl/interop
