windows 默认字符集是 GBK，Ubuntu 的默认字符集为 utf-8，这使得在用 telnet 登录远程服务器或查看 windows 文件时出现乱码。
则需要将 ubuntu 环境设置为 GBK 或  GB2312 ，或设置软件使其正确显示汉字。

下面以 GBK 字符集为例进行说明

- ### 修改 Ubuntu 默认字符集为 GBK

    1. 首先设置文件

            sudo vim /var/lib/locales/supported.d/local

        添加一行 zh_CN.GBK GBK

            sudo locale-gen
        > 生成locale

    2. 修改 ubuntu 的字符集

        方法一： 修改用户目录下的 .profile 文件，增加以下内容：
            LANGUAGE=”zh_CN:zh:en_US:en”
            LANG=zh_CN.GBK
        重新登录即可
        > 这个方法只对该用户有效

        方法二：修改 /etc/environment，增加以下内容：
            LANGUAGE=”zh_CN:zh:en_US:en”
            LANG=zh_CN.GBK
        然后重启X即可
        > 这个方法对没有设置 LANG 及 LANGUAGE 环境变量的用户有效

- ### 设置软件命名其正常显示 GBK

    系统环境支持 GB* 内码了，但用 vi, gedit 等工具访问文件还会继续乱码，需要针对不同的工具分别配置，使之自己检测支持范围内的编码。

    这需要软件本身支持多字符编码，最常见的是IE等浏览器，可以通过设置编码显示 GBK 字符集。Ubuntu 下的一些软件也支持此功能。

    以 ubuntu 的终端程序为例，使其正常显示 GBK 编码的方法是

        在 termial 窗口上点击菜单：终端->设置字符编码->选择 GBK

    - #### 解决文件名，mp3 标签，文本文件的中文乱码

        从 windows 转移到 ubuntu 的用户，常常会发现自己在 windows 下创建/下载/保存的文件经常性出现乱码问题（kubuntu 出现问题的可能性更高一些）。而使用默认播放器打开以往的音乐文件(mp3等)时，出现乱码的机会更是接近100%

        + 转换文件名由 GBK 为 UTF8

                sudo apt install convmv
                convmv -r -f cp936 -t utf8 –notest –nosmart *

        + 转换文件内容由 GBK 到 UTF8

                iconv -f gbk -t utf8 $i > newfile

        + 转换 mp3 标签编码

                sudo apt install python-mutagen
                find . -iname “\*.mp3” -exec dir mid3 iconv -e GBK {} \\;

    - #### vim 乱码

            sudo vi /etc/vim/vimrc

        加入以下配置参数
            let &termencoding=&encoding
            set fileencodings=utf-8,gb18030,gbk,GB2312,big5

    - #### gedit 乱码

        gedit 默认编码是 UTF8，打开 windows 下编辑的 GB2312 的文档都是乱码。

        解决方法之一就是把 gedit 的编码改为 GB2312 ，方法如下：
        
            1. 在 Applications 菜单上点右键，选择 EditMenu，在 MainMenu 的对话框中勾选 SystemTools－ConfigurationEditor，并从 Applications 菜单中开启。
            2. 依次开启 /apps/gedit-2/preferences/encodings/ 双击右侧 auto_detected, 在弹出对话框中点选 Add，添加 Values 值为 GB2312 ,确定后选中，点选 Up 按钮将其移至第一位。
            3. 同样方法，对 show_in_menu 进行设置，并将 GB2312 置于首位。

    还有一种方法是用 openoffice 打开 txt 文件时，会让你选择编码，选 GB2312 就行了。

