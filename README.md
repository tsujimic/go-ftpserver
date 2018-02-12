# go-ftpserver

go-ftpserver CLI application

### Install
```
- C:\Users\takashi (ex. your home directory)
  |
  |-- go-ftpserver.exe
  |
  |-- .aws
  |    |-- credentials
  |    |-- config
  |    |-- ... etc.
  |
```

### Help
Print the go-ftpserver help.
```
C:\Users\takashi>go-ftpserver.exe --help
go-ftpserver application

Usage:
  go-ftpserver [flags]

Flags:
      --cert_file string        ssl cert file (default "cert.pem")
  -d, --debug                   enable debug logging
      --help                    Print usage
      --implicit                enable implicit mode
      --key_file string         ssl key file (default "key.pem")
      --listen_address string   listen address (default "::")
  -P, --listen_port int         listen port (default 21)
      --pasv_address string     pasv ip address
      --pasv_max_port int       pasv max port (default 65535)
      --pasv_min_port int       pasv min port (default 1024)
      --profile string          shared credentials file profile (default "default")
      --tls_enable              enable tls
      --tls_verify              verify tls
  -v, --version                 Print version information and quit
```
### Version
Print the version.
```
C:\Users\takashi>go-ftpserver.exe --version
version 0.18.2.9r2 windows/386 go1.9.4
```
### Start Server
Windows:
```
C:\Users\takashi>go-ftpserver.exe
                    __ _
  __ _  ___        / _| |_ _ __  ___  ___ _ ____   _____ _ __
 / _' |/ _ \ _____| |_| __| '_ \/ __|/ _ \ '__\ \ / / _ \ '__|
| (_| | (_) |_____|  _| |_| |_) \__ \  __/ |   \ V /  __/ |
 \__, |\___/      |_|  \__| .__/|___/\___|_|    \_/ \___|_|
 |___/                    |_|                                 0.18.2.9r2

{"level":"info","ts":"2018-02-12T16:02:46.088+0900","msg":"listen on [::]:21"}
```

Mac or Linux:
```
$ ./go-ftpserver --listen_port 2121
```

Mac or Linux (default port 21):
```
$ sudo ./go-ftpserver
```

### Stop Server
CTRL + C.  
Windows:
```
C:\Users\takashi>go-ftpserver.exe --debug
                    __ _
  __ _  ___        / _| |_ _ __  ___  ___ _ ____   _____ _ __
 / _' |/ _ \ _____| |_| __| '_ \/ __|/ _ \ '__\ \ / / _ \ '__|
| (_| | (_) |_____|  _| |_| |_) \__ \  __/ |   \ V /  __/ |
 \__, |\___/      |_|  \__| .__/|___/\___|_|    \_/ \___|_|
 |___/                    |_|                                 0.18.2.9r2

{"level":"info","ts":"2018-02-12T16:04:02.325+0900","msg":"listen on [::]:21"}
{"level":"debug","ts":"2018-02-12T16:04:03.639+0900","msg":"processing signal 'interrupt'"}
{"level":"debug","ts":"2018-02-12T16:04:03.644+0900","msg":"shutdown initiated"}
{"level":"debug","ts":"2018-02-12T16:04:03.645+0900","msg":"shutdown done"}
```

### Connect ftp client
anonymous or ftp user  
Windows:
```
C:\Users\Public>ftp localhost
XXX に接続しました。
220 Welcome to the Go FTP Server
200 Command okay.
ユーザー (XXX:(none)): anonymous
331 User name okay, need password.
パスワード:
230 User logged in, proceed.
ftp> dir
200 Command okay.
150 File status okay; about to open data connection.
226 Transfer complete.
ftp: 1983 バイトが受信されました 0.09秒 21.79KB/秒。
ftp> by
221 Goodbye.
```
Mac or Linux:
```
$ ftp localhost 2121
```

### Setting AWS credentials
A credentials is structured like this:
```
- C:\Users\takashi (ex. your home directory)
  |-- go-ftpserver.exe
  |
  |-- .aws
  |    |-- credentials
  |    |-- config
  |    |-- ... etc.
```

AWS credentials:
```
[default]
aws_access_key_id = ABCDEFGHIJKLMN
aws_secret_access_key = ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890

[other]
aws_access_key_id = ABCDEFGHIJKLMN
aws_secret_access_key = ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890
```

### Setting credentials profile options
Windows:
```
C:\Users\takashi>go-ftpserver.exe --profile other
```

### Setting Pasv options
Windows:
```
C:\Users\takashi>go-ftpserver --pasv_address 192.168.177.70 --pasv_min_port 60000 --pasv_max_port 60999
```
```
C:\Users\takashi>go-ftpserver --pasv_min_port 60000 --pasv_max_port 60100
```

### Setting SSL and Start
Windows:
```
C:\Users\takashi>openssl genrsa -out key.pem 2048
Generating RSA private key, 2048 bit long modulus
....+++
...................................+++
e is 65537 (0x010001)

C:\Users\takashi>openssl req -new -x509 -key key.pem -out cert.pem -days 3650
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:JP
State or Province Name (full name) [Some-State]:Tokyo
Locality Name (eg, city) []:Tokyo
Organization Name (eg, company) [Internet Widgits Pty Ltd]:myCompany
Organizational Unit Name (eg, section) []:myUnit
Common Name (e.g. server FQDN or YOUR name) []:localhost
Email Address []:

C:\Users\takashi>go-ftpserver --ssl_enable --cert_file cert.pem --key_file key.pem
```
### Setting Proxy server
Windows:
```
set HTTPS_PROXY=http://proxy1.aaaaa.com:8080
set HTTP_PROXY=http://proxy1.aaaa.com:8080
```
