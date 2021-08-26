# windows自定义右键新建md文件

1. 安装Typora, 一个md文件编辑器

2. win + R

3. 输入regedit, 确定

4. 定位到`HKEY_CLASSES_ROOT\.md`

5. 点击`.md`文件夹, 双击右侧`(默认)`项编辑字符串

6. 将`数值数据`改为`Typora.exe`

7. 右键`.md`文件夹 => 新建 => 项

8. 把新建的项命名为`ShellNew`

9. 右键`ShellNew` => 新建 => 字符串项

10. 把新建的字符串项的名称改为`NullFile`

