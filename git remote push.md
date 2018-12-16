###  学习记录：git remote push 报错

Github只允许上传最大100MB的文件，如果超过，则会被server reject

```
Administrator@lx-PC MINGW32 /e/Martin_Huang (master)
$ git push -u origin master
Warning: Permanently added the RSA host key for IP address '13.250.177.223' to the list of known hosts.
Enumerating objects: 304, done.
Counting objects: 100% (304/304), done.
Delta compression using up to 4 threads
Compressing objects: 100% (297/297), done.
Writing objects:   2% (7/304), 40.55 MiB | 313.00 KiB/s
Writing objects: 100% (304/304), 288.15 MiB | 311.00 KiB/s, done.
Total 304 (delta 49), reused 0 (delta 0)
remote: Resolving deltas: 100% (49/49), done.
remote: warning: File ChromePortable_71.0.3573.0.zip is 85.43 MB; this is larger than GitHub's recommended maximum file size of 50.00 MB
remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
remote: error: Trace: 8d2f46a7e6d441eeaf7cf907382f4356
remote: error: See http://git.io/iEPt8g for more information.
remote: error: File theme/catfish-master.zip is 133.63 MB; this exceeds GitHub's file size limit of 100.00 MB
To github.com:comniuer/basyjdse1.git
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'git@github.com:comniuer/basyjdse1.git'

```

需要进行以下操作,即将提示过大的文件进行处理方可 push：

1. git filter-branch --force --index-filter "git rm --cached --ignore-unmatch theme/catfish-master.zip"  --prune-empty --tag-name-filter cat -- --all

2. git commit --amend -CHEAD

3. git push -u origin master

注意：

第一步是将报错的文件进行处理 *theme/catfish-master.zip*