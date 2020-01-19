# How to get AIDE to run on Oracle Linux, CentOS, Suse or Fedora.

## Admin Notes:- 

I did get acl attribute to work but still could NOT get xattr attribute to be accepted in aide.conf; (work around towards success - removed xattr from aide.conf).I also checked config.log and I can see that support check for xattr resulted as "yes". 

### Step1: Install all dependencies 
Way greedy approach here; but depending on your system's current state, you might already have some of these installed, in that case yum will anyway ignore that package from the list. Just in case you still see errors, review config.log and resolve it
```
sudo yum install -y bison flex pcre pcre-devel.x86_64 zlib zlib-devel.x86_64 libgcrypt-devel.x86_64 libgcrypt.x86_64 mhash-devel.x86_64 libcryptui-devel.x86_64 gettext-0.19.8.1-2.el7.x86_64 glibc glibc-devel glibc-static libacl libacl-devel libselinux libselinux-devel 
```
### Step2: ran configure script with these options - 
```
./configure --with-zlib --with-posix-acl --with-xattr --without-mhash --with-selinux --disable-static --with-gcrypt
```
### Step3: make (if make throws fatal or ld errors, It'd be good to resolve and rerun make, before "make install").
### Step4: ```sudo make install```

## Validations
### Step5: ```aide --version```
### Step6: ```sudo aide --init```
(assumption : you already have a valid aide.conf present at the path listed for CONFIG in above command"
### Step7: Rename aide.db.new file to aide.db 
### Step8: Make a change in a directory which is monitored under aide.conf
### Step9: ```sudo aide --check```
