---

Not always just to disable driver signing enforcement work in Windows. In Windows 10 when tried to start a driver after reboot with `bcdedit -set TESTSIGNING ON` I still got the `StartService FAILED 577: Windows cannot verify the digital signature for this file` message.

In order to start a driver non signed by Microsoft you still need some signature in the binary.

```
rem create the certificate
makecert -r -pe -ss PrivateCertStore -n CN=My.com(Test) -eku 1.3.6.1.5.5.7.3.3 MyTest.cer

rem install the certificate (run as admin)
certmgr /add MyTest.cer /s /r localMachine root

rem sign the driver
signtool sign /v /fd sha256 /s PrivateCertStore /n My.com(Test) /t http://timestamp.digicert.com MyDriver.sys
```


---
categories:
- writting
date: '2017-05-30'
link: https://www.imdb.com/title/tt6085362
tags:
- movies
title: Decanted
