How Repo Works
===
repo init -u url -b branch -m xmlfile
---
> it will create a **.repo** folder
> **url** points to a **manifest** repository that describes the whole sources
> a **manifest** repository is a special project with a default.xml file
> after it clone **manifest** repository, it checkouts the specified **branch**
> it then creates a symbolic link **.repo/manifest.xml** pointing to specified **xmlfile** in **.repo/manifests**
> if **xmlfile** is not specified, by default, using **.repo/manifests/default.xml**

roughly as follows:
```
  repo init -u $URL -b $BRANCH -m $MANIFEST
  --------------------
  mkdir .repo; cd .repo
  git clone https://android.googlesource.com/tools/repo
  git clone --bare $URL manifests.git
  mkdir -p manifests/.git; cd manifests/.git
  for i in ../../manifests.git/*; do ln -s $ı .; done
  cd ..
  git checkout $BRANCH -- .
  cd ..
  ln -s manifests/$MANIFEST manifest.xml  
```

> `repo --trace init..` will print what is happening.

what's in .repo
---
> **repo**: the actual code of repo tool
> **projects**: it holds the .git structures of every projects
> **manifests**: it holds the **manifest** repository
>  **manifest.xml**: the main manifest.xml, it generally links to **manifests/default.xml**

[NOTE] read **.repo/repo/doc/manifest-format.txt**

What does **fetch=".."** mean
---
It should be relative to the parent directory of the **manifests/**
for example
``` 
repo init -u https://android.googlesource.com/platform/manifest
fetch=".." in the manifest.xml is equal to "https://android.googlesource.com/platform/../"
```

repo sync
---
```
repo sync clones git repositories to .repo/projects for each project in manifest.xml and local_manifest.xml
creates working directories with .git having symlinks to the corresponding bare repository
checks out the branch specified in the manifest
and updates .repo/project.list
The case where the projects are already there is slightly different, essentially performing a git pull --rebase.
```
