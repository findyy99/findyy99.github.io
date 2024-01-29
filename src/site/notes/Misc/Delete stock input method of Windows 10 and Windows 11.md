---
{"dg-publish":true,"permalink":"/Misc/Delete stock input method of Windows 10 and Windows 11/","tags":["Windows"],"noteIcon":"","created":"2024-01-03T16:05:17.402+08:00","updated":"2024-01-03T16:12:34.182+08:00"}
---

由于中文输入法自带了中英文切换，而windows安装后自动又加了一个英语的输入法，导致在切换输入法及切换中英文时出现很烦人的情况，故查了很多网页，找了一个可以自动删除自带输入法的脚本。
# 1.  新建删除脚本
脚本内容如下，将其复制到NotePad中，保存，后缀改为`.xml` ，类似：`Remove_en-US.xml`.
```xml
<gs:GlobalizationServices xmlns:gs="urn:longhornGlobalizationUnattend">

    <!--User List-->

    <gs:UserList>

        <gs:User UserID="Current"/>

    </gs:UserList>

    <!--input preferences--> 

    <gs:InputPreferences>

        <!--add en-US keyboard input-->

        <gs:InputLanguageID Action="add" ID="0409:00000409"/>

        <!--remove en-US keyboard input-->

        <gs:InputLanguageID Action="remove" ID="0409:00000409"/>

    </gs:InputPreferences>

</gs:GlobalizationServices>
```

# 2. 新建批处理文件执行删除脚本
内容如下：
```bash
control intl.cpl,, /f:"\\Mac\Home\Desktop\windows11\delete_input\Remove_en-US.xml"
```
将上述内容复制到NotePad中，保存为`bat`文件，类似：`Remove_en-US.bat`。*请将`\\Mac`后的内容改为`Remove_en-US.xml`的路径。*
