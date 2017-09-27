“dpkg” 是 “Debian Packager” 的简写。为 “Debian” 专门开发的套件管理系统，方便软件的安装、更新及移除。所有源自 “Debian” 的 “Linux” 发行版都使用 “dpkg”，例如 “Ubuntu”、“Knoppix”等

1. 安装软件

	dpkg -i <file_name.deb>
		eg：dpkg -i sublime_text_x86.deb

2. 安装一个目录下面所有的软件包

	dpkg -R
		eg：dpkg -R /usr/local/src

3. 释放软件包，但是不进行配置

	dpkg –-unpack package_file
	> 如果和-R一起使用，参数可以是一个目录

		eg：dpkg –-unpack sublime_text_x86.deb

4. 重新配置和释放软件包

	dpkg –configure package_file
	> 如果和-a一起使用，将配置所有没有配置的软件包

		eg：dpkg –configure sublime_text_x86.deb

5. 删除软件包（保留其配置信息）

	dpkg -r
		eg：dpkg -r avg71flm

6. 替代软件包的信息

	dpkg –update-avail <Packages-file>

7. 合并软件包信息

	dpkg –merge-avail <Packages-file>

8. 从软件包里面读取软件的信息

	dpkg -A package_file

9. 删除一个包（包括配置信息）

	dpkg -P

10. 丢失所有的Uninstall的软件包信息

	dpkg –forget-old-unavail

11. 删除软件包的Avaliable信息

	dpkg –clear-avail

12. 查找只有部分安装的软件包信息

	dpkg -C

13. 比较同一个包的不同版本之间的差别

	dpkg –compare-versions ver1 op ver2

14. 显示帮助信息

	dpkg –help

15. 显示dpkg的Licence

	dpkg –licence (or) dpkg –license

16. 显示dpkg的版本号

	dpkg --version

17. 建立一个deb文件

	dpkg -b directory [filename]

18. 显示一个Deb文件的目录

	dpkg -c filename

19. 显示一个Deb的说明

	dpkg -I filename [control-file]

20. 搜索Deb包

	dpkg -l package-name-pattern
		eg：dpkg -I vim

21. 显示所有已经安装的Deb包，同时显示版本号以及简短说明

	dpkg -l

22. 报告指定包的状态信息

	dpkg -s package-name
		eg：dpkg -s ssh

23. 显示一个包安装到系统里面的文件目录信息

	dpkg -L package-Name
		eg：dpkg -L apache2

24. 搜索指定包里面的文件（模糊查询)

	dpkg -S filename-search-pattern

25. 显示包的具体信息

	dpkg -p package-name
		eg：dpkg -p cacti
