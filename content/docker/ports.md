# Fix ports not available

The following error 

> Ports are not available: listen tcp 0.0.0.0/9999: bind: An attempt was made to access a socket in a way forbidden by its access permissions

Can be corrected on windows by running the following commands:

```batch
net stop winnat
net start winnat
```