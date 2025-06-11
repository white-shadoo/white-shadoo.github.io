---
title: "Thndr Internship CTF"
date: 2025-06-11 00:00:00
categories: [CTF]
tags: [CTF,Pentesting,WEB]
image: 
  path: images/studying/wifi/LOGO-Yellow.png

---

# thndr

- first look

![image.png](images/CTF/thndr/image%200.png)

- mmm

![image.png](images/CTF/thndr/image%201.png)

- let’s try sql injection , after tries i didn’t find any sort of error
- i was running the fuzzer in the background and i found that

```bash
dirsearch -u 'http://18.195.238.165/' -x 403

[22:07:35] 200 -   35B  - /.bash_history
[22:07:36] 200 -   35B  - /.cache
[22:07:43] 200 -   35B  - /.password
[22:09:04] 200 -  587B  - /login.php
[22:09:49] 301 -  317B  - /upload  ->  http://18.195.238.165/upload/
[22:09:49] 200 -    0B  - /upload/
```

![image.png](images/CTF/thndr/image%202.png)

![image.png](images/CTF/thndr/image%203.png)

- all roads forward to roma , so let’s try the credentials
- bingo , i got first flag

![image.png](images/CTF/thndr/image%204.png)

- while looking at the site i found that

![image.png](images/CTF/thndr/image%205.png)

- while investigating why it’s not visible , i found that the parent div is invisible

![image.png](images/CTF/thndr/image%206.png)

- and after editing `display` value from none to block , i got this

![image.png](images/CTF/thndr/image%207.png)

- after trying to upload image i got that i am not and admin

![image.png](images/CTF/thndr/image%208.png)

- so let’s see how the server decides if i am admin or not
- i found in the request `jwt` token

![image.png](images/CTF/thndr/image%209.png)

- and after decoding it `base64` , i found that in the payload section `admin:0` , so let’s change it to `1` but the problem is how the server will deal with the modification of the jwt

![image.png](images/CTF/thndr/image%2010.png)

- first i tried to remove the token and the server redirected me to the login page
- after removing the signature i got that error

![image.png](images/CTF/thndr/image%2011.png)

- i will try removing signature attack by changing the algorithm to `none` and that will generate no signature (so now i can generate any token i want), and it worked

![image.png](images/CTF/thndr/image%2012.png)

- and bingo look at me , i am the admin now

![image.png](images/CTF/thndr/image%2013.png)

![image.png](images/CTF/thndr/image%2014.png)

- after escalating to admin privilege , now i can upload files , and let’s try to achieve rce from the uploaded file
- i will use `php` files as we know that the server is working with php files (we knew from the previous fuzzing , and from response of the server `apache` and from `wappalyzer`)

![image.png](images/CTF/thndr/image%2015.png)

![image.png](images/CTF/thndr/image%2016.png)

- i wrote this simple code for RCE

```php
<?php system($_GET["cmd"])?>
```

- then let’s try to upload it , lol the file is upload easily !!! (no mime type filter or filter on name)

![image.png](images/CTF/thndr/image%2017.png)

- mmmm but php didn’t execute

![image.png](images/CTF/thndr/image%2018.png)

- so i will assume that extension is allowed but with disabling of running php code , so i will try other extensions supported by the apache server `phps` didn’t work alsoo
- i will try to not use `system` , after using `phpinfo` the same thing no thing worked
- i upload normal png and it’s rendered succefully , i don’t know what is the problem with the php
- i think that php is disallowed to run in that directory
- i found that which mean the the server disables php from running

![image.png](images/CTF/thndr/image%2019.png)

- so the server disables the execution of php files and the PNG files is rendered proberly , and that is as i think because `.htaccess` in the upload directory that has a rule to disable php execution in that directory and subdirectories.
- so i wanted to update the `.htaccess` as it’s for the current directory , but the uploading directory is changing each request so if i updated the `.htaccess` the next request of the file will change , i tried to upload both files in the same request but it didn’t work , so i don’t know until now what to do here by `1/6/2025 by 11:00pm`
- after more and more searching i found that i can bypass the `.htaccess`

![image.png](images/CTF/thndr/image%2020.png)

- i found that https://httpd.apache.org/docs/2.4/howto/htaccess.html?source=post_page-----ca06d7e9ebd7---------------------------------------
- i have an idea , what about running the rce from the `.htaccess` file as after  trying to upload the `.htaccess` file it’s uploaded and i got  forbidden , which means that this file uploaded successfully and i can’t access it .

![image.png](images/CTF/thndr/image%2021.png)

- and after a lot of searching i solved it el 7amdullah

![image.png](images/CTF/thndr/image%2022.png)

![image.png](images/CTF/thndr/image%2023.png)

- and here is the flag

![image.png](images/CTF/thndr/image%2024.png)

![image.png](images/CTF/thndr/image%2025.png)

![image.png](images/CTF/thndr/image%2026.png)

-
