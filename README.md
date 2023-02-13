# Debian Hello Test
This is an example for adding a new executable script into "hello" debian sourcode and repackage it.

## 1. Download the debian source code
```
     ~$ mkdir Test; cd Test
~/Test$ apt-get source hello
```
## 2. Write new script and add it into package 
Create new executable script (_**Testing.sh**_)
```Ruby
#!/bin/bash
echo "New for Testing"
```
And put _**Testing.sh**_ under /hello-2.10
```
Test
├── hello_2.10-2ubuntu2.dsc
├── hello-2.10
│   ├── debian
│   │   ├── copyright
│   │   └── ...
│   ├── doc
│   │   └── ...
│   ├── maint.mk
│   ├── Makefile.in
│   └── testing.sh
└── ...
```
Create new install configuration (_**install**_)
```Ruby
testing.sh usr/bin
```
And put _**install**_ under /hello-2.10/debian
```
Test
├── hello_2.10-2ubuntu2.dsc
├── hello-2.10
│   ├── debian
│   │   ├── copyright
│   │   ├── install
│   │   └── ...
│   ├── doc
│   │   └── ...
│   ├── maint.mk
│   ├── Makefile.in
│   └── testing.sh
└── ...
```
## 3. Add new **_postinst_**(script) to print logs when installing hello debian package
Create new script (_**postinst**_)
```Ruby
#!/bin/bash
echo "New for Testing"
```
And put _**postinst**_ under /hello-2.10/debian
```
Test
├── hello_2.10-2ubuntu2.dsc
├── hello-2.10
│   ├── debian
│   │   ├── copyright
│   │   ├── install
│   │   ├── postinst
│   │   └── ...
│   ├── doc
│   │   └── ...
│   ├── maint.mk
│   ├── Makefile.in
│   └── testing.sh
└── ...
```
## 4. Rebuild whole package as a new package
```
~/Test/hello-2.10$ debuild -b -us -uc
```
## 5. Install new re-build package
```
~/Test/hello-2.10$ cd ..
           ~/Test$ sudo dpkg --install hello_2.10-2ubuntu2_amd64.deb
```
## 6. Test new script
```
~/Test$ testing.sh
```



