title: "git"
date: 2015-05-20 16:53:34
tags: git
---


- cancal add before commit
``` bash
git reset .
```

- Store http usname and password
``` bash
git config --global credential.helper cache
git config --global credential.helper store
```

- set http proxy
``` bash
git config global http.proxy http://user:pwd@proxy_addr:port
```
