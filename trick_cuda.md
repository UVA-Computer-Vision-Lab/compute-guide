---
title: Install cuda-toolkit
parent: Nice Tricks
has_children: false
nav_order: 2
---

# Installation guide for cuda-toolkit


When installing packages, if you encounter the error `OSError: CUDA_HOME environment variable is not set. Please set it to your CUDA install root.`, you'll need to install a compatible CUDA Toolkit version. Use `module avail` to list available versions. To install, for example, CUDA Toolkit 12.4.0, execute:

```
module load cuda-toolkit-12.4.0
```

This setup should address the installation error by properly configuring the CUDA environment.