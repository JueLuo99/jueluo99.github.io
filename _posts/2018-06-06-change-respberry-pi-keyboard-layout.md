---
layout: post
title: 修改树莓派键盘布局
date: 2018-06-06 22:43
category: 树莓派
tags: [linux, raspberry-pi]
---

树莓派默认使用的是英国键盘布局，在直接用键盘连接至树莓派时，可能会出现部分符号屏幕显示与键盘显示不一致的情况。

<!--more-->

1. 使用如下命令进入配置修改键盘布局界面
    ```
    dpkg-reconfigure keyboard-configuration
    ```

2. 根据自己的键盘选择键盘模型（Keyboard model）

    我这里使用的是 ikbc F108，所以选择 ```Generic 104-key PC```

3. 选择键盘布局（Keyboard layout）
    
    默认是英国键盘布局所以会看到
    ```
    English (UK)
    English (UK) - English (UK, Colemak)
    English (UK) - English (UK, Dvorak with UK punctuation)
    English (UK) - English (UK, Dvorak)
    ...
    ```
    这样一排英式键盘布局，选择最后一个 ```Other```

4. 选择键盘对应的国家或地区（Country of origin for the keyboard）

    这里我选择了 ```Chinese``` ，其实我们中国大陆用的键盘通常都是沿用美式键盘标准的，所以选择 ```English (US)``` 也是可以的。

    （好像有规定中式键盘上的 ```v``` 键要印刷成 ```ü``` 的？）

5. 选择键盘布局（Keyboard layout）

    前面选择的是 ```Chinese``` 的话，这个界面选择 ```Chinese``` 即可。
    
    前面选择的是 ```English (US)``` 的话，这个界面选择 ```English (US) - English (US, alternative international)``` 即可。

    （中国大陆以外的键盘视实际情况选择）

6. 选择作为 ALT 按键的键（Key to functions as AltGr）

    一般位置的 ALT 键选择默认的 ```The default for the keyboard layout``` 即可。

7. 选择 Compose 键（Compose key）

    Compose 键用于输入不在键帽上的字符（如汉语拼音里带音调的字母等）
    
    我这里不需要，选择 ```No compose key```

8. 重启树莓派，新的键盘布局生效