
### 基础信息

#### 文件后缀

PowerShell的文件后缀为.ps1可以在VScode中先编写后再使用PoweShell执行

#### 变量
PowerShell中变量使用$开头并且最好（或者必须）给予一个初始值
```powershell
$Count = 0
```

#### replace
将数据中的对应数据进行删除
```powershell
$content = '你好！'
# 方法一
$content -replace "!", "。"
# 方法二
$content.replace("!", "。")
```

#### 管道操作符 "|"
就像管道一样，将"|"前面的数据作为输入放进“|”后面进行加工

```powershell
$content = '你好！'
$content | SetContent -path 'E:\123.txt'
```

#### 比较符
- -eq -> equals -> 等于
- -ne -> not equals -> 不等于
- -gt -> greater then -> 大于
- -ge -> greater than or equal -> 大于或等于
- -lt -> less than -> 小于
- -le -> less than or equal -> 小于或等于
- like -> 相似
- notlike -> 不相似
- match -> Returns true when string matches regex
#### if
和普通使用类似但是比较符需注意使用上面的比较符
```powershell
$count1 = 0
$count2 = 1
if($count1 -ne $count2){
	Write-Host "不等于"
} else {
	Write-Host "等于"
}
```

### 函数

#### Get-ChildItem
用于获取指定路径下的文件和文件夹
URL: [Get-ChildItem 教程](https://www.cnblogs.com/suv789/p/18148529)
参数：
- 使用 `-Path` 参数指定要检查的路径。
- 使用 `-Filter` 参数根据通配符模式过滤文件和文件夹。
- 使用 `-Include` 和 `-Exclude` 参数指定要包含或排除的文件和文件夹。
- 使用 `-Recurse` 参数递归地列出子目录中的文件和文件夹。
- 使用 `-File` 和 `-Directory` 参数只返回文件或文件夹对象。
```powershell
# 注意，路径后需添加*后面的Inclue才可以正常使用
Get-ChildItem -Path "D:\MyReact\src\*" -Recurse -Include *.js, *.jsx
```

#### Get-Content
用于读取指定路径的文件
URL:[PowerShell | Get-Conent](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.management/get-content?view=powershell-7.5)
参数：
- `-Path` 获取文件的URL
- `-Raw` 将获取的数据转换为一行显示（会显示换行符）
- `-Encoding` 读取数据采用的格式（一般为UTF-8）

```powershell
$conten = Get-Content -Path "E:\123.txt" -Raw -Encoding UTF-8
```

#### Set-Content
用于写入指定路径文件数据的操作
URL:[PowerShell Set-Content 命令](https://www.delftstack.com/zh/howto/powershell/powershell-set-content-cmdlet/)

| 参数              | 描述                                                     |
| --------------- | ------------------------------------------------------ |
| `-Path_to_file` | 您可以指定一个现有文本文件路径或在给定路径中创建一个新文件。                         |
| `-Value`        | 此参数用于传递您要写入的文本内容。                                      |
| `-Force`        | `-Force` 参数将替换只读文件中的内容。                                |
| `-Encoding`     | 目标文件的文本编码默认为 `utf8NoBOM`。                              |
| `-Exclude`      | 在此操作中需要排除的项目以字符串数组的形式指定。                               |
| `-Include`      | 这是 `-Exclude` 参数的相反。此参数指定需要包含在 `Set-Content` 操作中的项目数组。 |
| `-PassThru`     | 当指定 `PassThru` 参数时，命令输出已添加到文本文件的文本内容。                  |

```powershell
$content = "写入文件"
$content | Set-Content -path "E:\123.txt" -Encoding UTF-8
```
#### Write-Host
在powershell显示数据，类似console.log

```powershell
$content = "变量数据。"
Write-Host "你好！"
Write-Host $content
```

#### Read-Host
用于控制台的输入，也可用于PowerShell执行完成后不退出窗口的结束符
```powershell
# 用于结束后不退出窗口
Read-Host "Enter Any Key To Exit!"
# 将控制台输入另存为安全字符串
$count = Read-Host "Enter a count:"
# 另存为安全字符串
#本示例以提示显示字符串“输入密码：”。 当输入值时，星号（`*`）显示在主机上代替输入。 按下 Enter 键后，该值将作为 **SecureString** 对象存储在 `$pwd_secure_string` 变量中。
$count = Read-Host "Enter a passworld:" -AsSecureString
# 掩码输入和作为纯文本字符串
# 本示例以提示显示字符串“输入密码：”。 当输入值时，星号（`*`）显示在主机上代替输入。 按下 Enter 键时，该值以纯文本形式存储在 `$pwd_string` 变量中的 String **对象**。
$count = Read-Host "Enter a passworld:" -MaskInput
```

#### ForEach-Object 
类似map，其中循环的item为$_
```powershell
1000,2000,3000 | ForEach-Object -Process {$_/1000}

# return
# 1
# 2
# 3
```

### 实操

#### 批量修改文件
获取文件夹内所有的JS, JSX文件并且将`const`改为`let`
```powershell
# 用于计算执行成功几个文件
$Count = 0

Get-ChildItem -Path "D:\MyReact\src\*" -Recurse -Include *.js, *.jsx | ForEach-Object{
	# 获取数据
	$content = Get-Content -Path $_.FullName -Raw -Encoding UTF8
	# 修改数据
	 $newContent = $content -replace "const", "let"
	 
	# 如果文件被修改了则写入否则不做操作
	if($newContent -ne $content){
		# 写入文件
		$newContent | Set-Content -Path $_.FullName -Encoding UTF8
		# 执行成功文件数加1
		$Count = $Count + 1
		# 返回执行成功文件数
		Write-Host $Count
	}
}

# 防止执行完成直接页面关闭
Read-Host -Prompt "Enter to Exit..."
```