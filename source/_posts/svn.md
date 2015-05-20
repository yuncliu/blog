title: "svn"
date: 2015-05-20 15:29:30
tags: svn
---


## revert subversion repository

- Check out a nice clean working copy.

- Merge (backwards) changes.
``` bash
svn merge -r100:70 http://repo.com/my/project/trunk
```

- Check sanity. Is your working copy exactly what you wanted? If so:
``` bash
    svn commit -m "rolled back to the good old days of r70
```

## create subversion server
- create server
``` bash
    sudo svnadmin create /home/svn/fitness
    svn co file:///home/svn/fitness
    svn co file://localhost/home/svn/fitness
```

- modify configure file
``` bash
    svnserve.conf passwd authz

    svnserve.conf:
    password-db = password
    authz-db = authz

    [general]
    anon-access = read
    auth-access = write
    password-db = passwd

    password:
    [users]
    mirze = 123456
    test1 = 123456
    test2 = 123456

    authz:
    [groups]
    admin = mirze,test1
    test = test2
    [/]
    @admin=rw
    *=r
```

- check out
``` bash
    svn co svn://localhost/
```

