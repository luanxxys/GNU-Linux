��dpkg�� �� ��Debian Packager�� �ļ�д��Ϊ ��Debian�� ר�ſ������׼�����ϵͳ����������İ�װ�����¼��Ƴ�������Դ�� ��Debian�� �� ��Linux�� ���а涼ʹ�� ��dpkg�������� ��Ubuntu������Knoppix����

1. ��װ���

	dpkg -i <file_name.deb>
		eg��dpkg -i sublime_text_x86.deb

2. ��װһ��Ŀ¼�������е������

	dpkg -R
		eg��dpkg -R /usr/local/src

3. �ͷ�����������ǲ���������

	dpkg �C-unpack package_file
	> �����-Rһ��ʹ�ã�����������һ��Ŀ¼

		eg��dpkg �C-unpack sublime_text_x86.deb

4. �������ú��ͷ������

	dpkg �Cconfigure package_file
	> �����-aһ��ʹ�ã�����������û�����õ������

		eg��dpkg �Cconfigure sublime_text_x86.deb

5. ɾ���������������������Ϣ��

	dpkg -r
		eg��dpkg -r avg71flm

6. ������������Ϣ

	dpkg �Cupdate-avail <Packages-file>

7. �ϲ��������Ϣ

	dpkg �Cmerge-avail <Packages-file>

8. ������������ȡ�������Ϣ

	dpkg -A package_file

9. ɾ��һ����������������Ϣ��

	dpkg -P

10. ��ʧ���е�Uninstall���������Ϣ

	dpkg �Cforget-old-unavail

11. ɾ���������Avaliable��Ϣ

	dpkg �Cclear-avail

12. ����ֻ�в��ְ�װ���������Ϣ

	dpkg -C

13. �Ƚ�ͬһ�����Ĳ�ͬ�汾֮��Ĳ��

	dpkg �Ccompare-versions ver1 op ver2

14. ��ʾ������Ϣ

	dpkg �Chelp

15. ��ʾdpkg��Licence

	dpkg �Clicence (or) dpkg �Clicense

16. ��ʾdpkg�İ汾��

	dpkg --version

17. ����һ��deb�ļ�

	dpkg -b directory [filename]

18. ��ʾһ��Deb�ļ���Ŀ¼

	dpkg -c filename

19. ��ʾһ��Deb��˵��

	dpkg -I filename [control-file]

20. ����Deb��

	dpkg -l package-name-pattern
		eg��dpkg -I vim

21. ��ʾ�����Ѿ���װ��Deb����ͬʱ��ʾ�汾���Լ����˵��

	dpkg -l

22. ����ָ������״̬��Ϣ

	dpkg -s package-name
		eg��dpkg -s ssh

23. ��ʾһ������װ��ϵͳ������ļ�Ŀ¼��Ϣ

	dpkg -L package-Name
		eg��dpkg -L apache2

24. ����ָ����������ļ���ģ����ѯ)

	dpkg -S filename-search-pattern

25. ��ʾ���ľ�����Ϣ

	dpkg -p package-name
		eg��dpkg -p cacti
