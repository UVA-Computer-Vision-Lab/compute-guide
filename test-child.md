---
title: Install git-lfs
parent: Nice Tricks
has_children: false
nav_order: 1
---

# Installation guide for git-lfs

```
cd
module load go
git clone https://github.com/git-lfs/git-lfs.git
cd git-lfs
make
cd
cp .bashrc .bash.back
echo 'export PATH=$PATH:~/git-lfs/bin' >> .bashrc
```

You can then either do a "source ~/.bashrc" to start using git-lfs immediately or it will be in your PATH the next time you re-open the terminal.

