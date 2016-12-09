How Repo Works
===
repo init -u url -b branch -m xmlfile
---
> it will create a **.repo** folder
> **url** points to a **manifest** repository that describes the whole sources
> a **manifest** repository is a special project with a default.xml file

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