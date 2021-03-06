Forked from https://github.com/InAnimaTe/docker-vsftpd-anon

## WARNING

This fork is somewhat more dangerous than InAnimaTe/docker-vsftpd-anon because **IT ALLOWS ANONYMOUS UPLOADS**.

Thus, you will need to be extra vigilant to ensure any volumes you don't want to allow uploads to have *:ro* at the end of their bind mount declaration!


----


### vsftpd-anon: An quick, anonymous ftp server docker image

This image is meant for running something like a public read-only share. User accounts are *not* supported and all data access is meant to be read only via ftp anonymous login.

#### Up-and-Running

View the included `docker-compose.yml` for a runtime configuration example or check the below one-liner for a quick launch!

```
docker run -d -p 20-21:20-21 -p 65500-65515:65500-65515 -v /tmp:/var/ftp:ro mikenye/vsftpd-anon-uploads
```

#### Runtime Configuration Options

There are a series of available variables you can tune at your own discretion. The defaults are most likely acceptable for most use cases.

* `ANON_ROOT` - The directory in the container which vsftpd will serve out (default: `/var/ftp`)
* `MAX_PORT` - The maximum port for pasv communiation (default: `65515`)
* `MIN_PORT` - The minimum port for pasv communication (default: `65500`)
* `MAX_PER_IP` - The maximum connections from one host (default: `2`)
* `MAX_LOGIN_FAILS` - Maximum number of login failures before kicking (default: `2`) 
* `MAX_CLIENTS` - Maximum number of simultaneously connected clients (default: `50`)
* `MAX_RATE` - Maximum bandwidth allowed per client in bytes/sec (default: `6250000`)
* `FTPD_BANNER` - An ftpd banner displayed when a client connects (default: `Welcome to an awesome public FTP Server`)


#### Notes

* Ensure you use *:ro* at the end of your bind mount declaration for non incoming directorites!
* Ensure you don't use *:ro* at the end of your incoming dir mount declaration!
* We utilize ftp passive mode so we can define the ports we need and not have to use `--net=host`. This is the preferred way to use ftp!
* You can find some great documentation on configuration options and other vsftpd information on the [Archwiki](https://wiki.archlinux.org/index.php/Very_Secure_FTP_Daemon) and in the [man page](https://security.appspot.com/vsftpd/vsftpd_conf.html)
