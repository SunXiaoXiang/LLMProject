## 3 Linux
### 3.1 文件管理
#### 3.1.1 touch

#### 命令：`touch`
用于创建新的空文件或更新现有文件的访问和修改时间戳。以下是 `touch` 命令的一些常见用法和选项：

**参数解释：**
- `-a`：仅更改访问时间。
- `-m`：仅更改修改时间。
- `-t`：使用指定的时间而不是当前时间。格式为 `[[CC]YY]MMDDhhmm[.ss]`。
- `-d`：使用指定的日期时间字符串而不是当前时间。

以下是touch命令的用法
```bash
pwd
ls        #显示文件
touch demo.log
ls -l     #显示隐藏文件和最后修改时间
ls -lu    #显示隐藏文件和最后访问时间
stat demo.log   #显示文件详细信息（包括最后访问时间、修改时间、文件状态变更时间）
show_times.sh demo.log
```

**显示修改时间**：
ls -l

**显示访问时间**：
ls -lu

 使用 `stat` 命令

`stat` 命令可以显示文件的详细信息，包括访问时间（Access）、修改时间（Modify）和更改时间（Change）。例如：
stat filename

当touch一个不存在的文件，不同命令查看文件的三个时间情况（注：show_time.sh 脚本将显示访问时间和修改时间）
![[Pasted image 20240712231849.png]]
当touch -a更新access time时：
![[Pasted image 20240712232221.png]]
当touch -m更新modify time时：
![[Pasted image 20240712232422.png]]

![[Pasted image 20240712232924.png]]
当touch指定时间更新时：
![[Pasted image 20240712233125.png]]
当使用touch -d指定修改时，将完整更新三个时间。
![[Pasted image 20240712233348.png]]

添加的Bash脚本，如下：
```bash
#!/bin/bash

for file in "$@"; do
    access_time=$(stat -c %x "$file")
    modify_time=$(stat -c %y "$file")
    echo "File: $file"
    echo "Access Time: $access_time"
    echo "Modify Time: $modify_time"
    echo "---------------------"
done
```

将这个脚本保存为 `show_times.sh`，然后运行：
```bash
chmod +x show_times.sh
./show_times.sh filename
```

你可以在 `~/.bashrc` 文件中添加脚本的路径，这样在任意目录下都可以执行这个脚本。以下是具体步骤：

1. **将脚本移动到某个目录**：  
    假设你将 `show_times.sh` 脚本放在了 `~/scripts` 目录下。
    
2. **修改 `~/.bashrc` 文件**：  
    打开 `~/.bashrc` 文件，并在文件末尾添加以下行：
    export PATH=$PATH:~/scripts
    
3. **使修改生效**：  
    保存并关闭 `~/.bashrc` 文件后，运行以下命令使修改生效：
    source ~/.bashrc
    
4. **验证路径是否添加成功**：  
    你可以通过以下命令来验证路径是否添加成功：
    echo $PATH
    
    你应该能在输出中看到 `~/scripts` 目录的路径。
    
5.**在任意目录下执行脚本**：  
    现在你可以在任意目录下执行 `show_times.sh` 脚本，例如：
    show_times.sh filename
    
通过这种方式，你可以确保在任意目录下都能执行 `show_times.sh` 脚本。



#### 3.1.2 mkdir 

#### 命令：`mkdir`
"make directory"，即创建目录。

**参数解释：**

- `-p`：递归创建目录，如果父目录不存在则自动创建。
- `-m`：设置目录的权限模式。
- `-v`：显示详细的创建过程。

创建一个新文件夹，使用tree查看目录树形（pip install tree，安装后可使用）。
![[Pasted image 20240712233929.png]]
创建多层文件夹，使用tree查看目录树形
![[Pasted image 20240712234048.png]]
创建文件夹并设置权限，使用tree查看目录树形
![[Pasted image 20240712234247.png]]
### 注意事项
- `mkdir` 命令默认情况下不会递归创建目录，如果父目录不存在，则会报错。使用 `-p` 选项可以避免这个问题。
- 创建目录时，默认的权限模式是 `rwxr-xr-x`（即 755），可以通过 `-m` 选项自定义权限。
#### 3.1.3 cd
#### 命令：`cd`
"change directory" ，即更换工作目录。

```bash
cd /path/to/dir  # 更换到指定目录
cd ~   # 更换到当前用户的主目录
cd     # 更换到当前用户的主目录
cd -   # 更换到之前的目录
cd ..  # 更换到上一级目录
cd /   # 更换到root 目录
```
执行截图。
![[Pasted image 20240713003414.png]]
#### 3.1.4 pwd
#### 命令：`pwd`
"print working directory"，即打印当前工作目录。

- `pwd`：这个命令会输出当前工作目录的完整路径。
- `pwd -L`：**`-L` (logical)**  会显示当前工作目录的逻辑路径，包括任何符号链接（软链接）。这是 `pwd` 命令的默认行为。
- `pwd -P`：**`-P` (physical)**会显示当前工作目录的物理路径，不包括任何符号链接（软链接）。如果当前目录是通过符号链接进入的，`-P` 参数会显示实际的物理路径

假设当前目录是 `/root/share`，并且 `/root/share` 是一个符号链接，指向 `/share`。

![[Pasted image 20240713003928.png]]

#### 3.1.5 cat
#### 命令：`cat`
"concatenate"，即连接。这个命令用于连接文件并打印到标准输出（通常是终端），也可以用于显示文件内容。
`cat` 是 "concatenate" 的缩写，意味着它可以用来显示文件内容、合并文件以及创建新文件。以下是 `cat` 命令的常用形式和常用参数：

### 常用形式

1. **显示文件内容**：
   ```bash
   cat filename
   ```
   这个命令会显示 `filename` 的内容。

2. **合并多个文件**：
   ```bash
   cat file1 file2 > combinedfile
   ```
   这个命令会将 `file1` 和 `file2` 的内容合并，并保存到 `combinedfile` 中。

3. **创建新文件**：
   ```bash
   cat > newfile
   ```
   这个命令会创建一个新文件 `newfile`，并允许你输入内容。按 `Ctrl+D` 结束输入。

4. **追加内容到文件**：
   ```bash
   cat >> existingfile
   ```
   这个命令会打开 `existingfile`，并允许你追加内容。按 `Ctrl+D` 结束输入。

### 常用参数

1. **`-n`**：显示行号。
   ```bash
   cat -n filename
   ```
   这个命令会显示 `filename` 的内容，并在每行前显示行号。

2. **`-b`**：显示行号，但不对空白行编号。
   ```bash
   cat -b filename
   ```
   这个命令会显示 `filename` 的内容，并在每行前显示行号，但不对空白行编号。

3. **`-s`**：压缩连续的空白行。
   ```bash
   cat -s filename
   ```
   这个命令会显示 `filename` 的内容，并将连续的空白行压缩为一个空白行。

4. **`-E`**：在每行结束处显示 `$`。
   ```bash
   cat -E filename
   ```
   这个命令会显示 `filename` 的内容，并在每行结束处显示 `$`。

5. **`-T`**：将制表符显示为 `^I`。
   ```bash
   cat -T filename
   ```
   这个命令会显示 `filename` 的内容，并将制表符显示为 `^I`。

### 示例

1. **显示文件内容并显示行号**：
   ```bash
   cat -n filename
   ```

2. **合并多个文件并显示行号**：
   ```bash
   cat -n file1 file2 > combinedfile
   ```

3. **创建新文件并显示行号**：
   ```bash
   cat -n > newfile
   ```

4. **追加内容到文件并显示行号**：
   ```bash
   cat -n >> existingfile
   ```

通过这些常用形式和参数，`cat` 命令可以灵活地用于各种文件操作。

#### 3.1.6 vim

### 3.1.7 cp和ln
#### 命令：`cp`

"copy"，即复制。这个命令用于复制文件或目录。

`cp` 命令是 Linux 系统中用于复制文件和目录的常用命令。以下是一些常用的示范和参数解释：

### 基本语法
```bash
cp [选项] 源文件 目标文件
```

### 常用选项
- `-i`：交互模式，如果目标文件已存在，会提示是否覆盖。
- `-f`：强制复制，如果目标文件已存在，会直接覆盖而不提示。
- `-r` 或 `-R`：递归复制，用于复制目录及其内容。
- `-v`：显示详细信息，复制过程中显示正在复制的文件。
- `-p`：保留文件的属性（如修改时间、权限等）。

### 示范

1. **复制文件**：
   ```bash
   cp file1.txt file2.txt
   ```
   这个命令会将 `file1.txt` 复制到 `file2.txt`。

2. **复制文件到目录**：
   ```bash
   cp file1.txt /path/to/directory/
   ```
   这个命令会将 `file1.txt` 复制到 `/path/to/directory/` 目录下。

3. **复制目录及其内容**：
   ```bash
   cp -r /path/to/source_directory/ /path/to/destination_directory/
   ```
   这个命令会将 `/path/to/source_directory/` 目录及其所有内容复制到 `/path/to/destination_directory/`。

4. **交互模式复制**：
   ```bash
   cp -i file1.txt file2.txt
   ```
   如果 `file2.txt` 已存在，会提示是否覆盖。

5. **强制复制**：
   ```bash
   cp -f file1.txt file2.txt
   ```
   如果 `file2.txt` 已存在，会直接覆盖而不提示。

6. **显示详细信息**：
   ```bash
   cp -v file1.txt file2.txt
   ```
   复制过程中会显示正在复制的文件。

7. **保留文件属性**：
   ```bash
   cp -p file1.txt file2.txt
   ```
   复制文件时会保留文件的修改时间、权限等属性。

### 综合示范
假设你有一个目录 `source_dir`，里面包含多个文件和子目录，你想将其复制到 `destination_dir`，并保留文件属性，同时显示详细信息：
```bash
cp -rvp /path/to/source_dir/ /path/to/destination_dir/
```

通过这些示范，你可以灵活地使用 `cp` 命令来复制文件和目录，并根据需要选择合适的选项。

![[Pasted image 20240716002338.png]]

![[Pasted image 20240716002547.png]]

![[Pasted image 20240716002942.png]]

"link"，即链接。这个命令用于创建链接文件，包括硬链接和符号链接（软链接）。链接文件类似于 Windows 中的快捷方式，可以指向另一个文件或目录。`ln` 命令有两种类型的链接：硬链接（hard link）和符号链接（symbolic link 或 soft link）。

### 硬链接（Hard Link）

硬链接是文件系统中的多个文件名指向同一个 inode（文件数据存储块）。硬链接不能跨越文件系统，也不能指向目录。

#### 创建硬链接
```bash
ln 目标文件 链接名
```

#### 特点
- 硬链接与原文件共享同一个 inode，因此它们具有相同的文件内容和属性。
- 删除原文件不会影响硬链接，因为硬链接仍然指向同一个 inode。
- 硬链接不能跨越文件系统。
- 硬链接不能指向目录。

### 符号链接（Symbolic Link 或 Soft Link）

符号链接是一个特殊的文件，它包含了指向另一个文件或目录的路径。符号链接可以跨越文件系统，也可以指向目录。

#### 创建符号链接
```bash
ln -s 目标文件 链接名
```

#### 特点
- 符号链接包含指向目标文件或目录的路径。
- 删除原文件会使符号链接失效，因为符号链接指向的路径不再存在。
- 符号链接可以跨越文件系统。
- 符号链接可以指向目录。

### 示例

1. **创建硬链接**：
   ```bash
   ln file1.txt file1_hardlink.txt
   ```
   这个命令会创建一个硬链接 `file1_hardlink.txt`，它指向 `file1.txt`。

2. **创建符号链接**：
   ```bash
   ln -s file1.txt file1_symlink.txt
   ```
   这个命令会创建一个符号链接 `file1_symlink.txt`，它指向 `file1.txt`。

3. **强制创建符号链接**：
   ```bash
   ln -sf file1.txt file1_symlink.txt
   ```
   这个命令会强制创建一个符号链接 `file1_symlink.txt`，如果 `file1_symlink.txt` 已存在，则会删除现有文件并创建新链接。

4. **交互模式创建符号链接**：
   ```bash
   ln -si file1.txt file1_symlink.txt
   ```
   这个命令会以交互模式创建一个符号链接 `file1_symlink.txt`，如果 `file1_symlink.txt` 已存在，则会提示用户是否覆盖。

5. **显示详细信息**：
   ```bash
   ln -sv file1.txt file1_symlink.txt
   ```
   这个命令会创建一个符号链接 `file1_symlink.txt`，并显示详细信息。

### 注意事项
- 硬链接不能跨越文件系统。
- 符号链接可以跨越文件系统，也可以指向目录。
- 删除原始文件后，硬链接仍然有效，因为它们指向相同的 inode。
- 删除原始文件后，符号链接将失效，因为它们指向的路径不再存在。

通过 `ln` 命令，你可以方便地创建和管理文件和目录的链接，提高文件系统的灵活性和效率。

#### 3.1.8 mv 和rm

`mv` 命令是 Linux 和 Unix 系统中的一个基本命令，用于移动文件或目录，也可以用于重命名文件或目录。以下是 `mv` 命令的常用示范和参数解释：

### 基本语法
```bash
mv [选项] 源文件或目录 目标文件或目录
```

### 常用选项
- `-i`：交互模式，如果目标文件已存在，会提示是否覆盖。
- `-f`：强制移动，如果目标文件已存在，会直接覆盖而不提示。
- `-v`：显示详细信息，移动过程中显示正在移动的文件。

### 示范

1. **移动文件**：
   ```bash
   mv file1.txt /path/to/destination/
   ```
   这个命令会将 `file1.txt` 移动到 `/path/to/destination/` 目录下。

2. **重命名文件**：
   ```bash
   mv file1.txt file2.txt
   ```
   这个命令会将 `file1.txt` 重命名为 `file2.txt`。

3. **移动目录**：
   ```bash
   mv /path/to/source_directory/ /path/to/destination_directory/
   ```
   这个命令会将 `/path/to/source_directory/` 目录及其所有内容移动到 `/path/to/destination_directory/`。

4. **交互模式移动**：
   ```bash
   mv -i file1.txt /path/to/destination/
   ```
   如果 `/path/to/destination/` 目录下已存在同名文件，会提示是否覆盖。

5. **强制移动**：
   ```bash
   mv -f file1.txt /path/to/destination/
   ```
   如果 `/path/to/destination/` 目录下已存在同名文件，会直接覆盖而不提示。

6. **显示详细信息**：
   ```bash
   mv -v file1.txt /path/to/destination/
   ```
   移动过程中会显示正在移动的文件。

### 综合示范
假设你有一个目录 `source_dir`，里面包含多个文件和子目录，你想将其移动到 `destination_dir`，并保留文件属性，同时显示详细信息：
```bash
mv -v /path/to/source_dir /path/to/destination_dir
```

通过这些示范，你可以灵活地使用 `mv` 命令来移动文件和目录，并根据需要选择合适的选项。

![[Pasted image 20240716004539.png]]

`rm` 命令是 Linux 和 Unix 系统中的一个基本命令，用于删除文件和目录。以下是 `rm` 命令的常用示范和参数解释：

### 基本语法
```bash
rm [选项] 文件或目录
```

### 常用选项
- `-i`：交互模式，删除每个文件前会提示确认。
- `-f`：强制删除，忽略不存在的文件，不提示确认。
- `-r` 或 `-R`：递归删除，用于删除目录及其内容。
- `-v`：显示详细信息，删除过程中显示正在删除的文件。

### 示范

1. **删除文件**：
   ```bash
   rm file1.txt
   ```
   这个命令会删除 `file1.txt`。

2. **删除多个文件**：
   ```bash
   rm file1.txt file2.txt file3.txt
   ```
   这个命令会删除 `file1.txt`、`file2.txt` 和 `file3.txt`。

3. **删除目录及其内容**：
   ```bash
   rm -r /path/to/directory/
   ```
   这个命令会删除 `/path/to/directory/` 目录及其所有内容。

4. **交互模式删除**：
   ```bash
   rm -i file1.txt
   ```
   删除每个文件前会提示确认。

5. **强制删除**：
   ```bash
   rm -f file1.txt
   ```
   忽略不存在的文件，不提示确认。

6. **显示详细信息**：
   ```bash
   rm -v file1.txt
   ```
   删除过程中会显示正在删除的文件。

### 综合示范
假设你有一个目录 `source_dir`，里面包含多个文件和子目录，你想将其删除，并保留文件属性，同时显示详细信息：
```bash
rm -rv /path/to/source_dir
```

通过这些示范，你可以灵活地使用 `rm` 命令来删除文件和目录，并根据需要选择合适的选项。请注意，`rm` 命令删除的文件和目录通常无法恢复，因此在使用时要格外小心。
![[Pasted image 20240716005032.png]]

#### 3.1.9 find

`find` 命令是 Linux 和 Unix 系统中的一个非常强大的工具，用于在文件系统中查找文件和目录。它可以根据各种条件进行搜索，并执行相应的操作。以下是 `find` 命令的常用示范和参数解释：

### 基本语法
```bash
find 路径 选项 表达式
```

### 常用选项
- `-name`：按文件名查找。
- `-iname`：按文件名查找（不区分大小写）。
- `-type`：按文件类型查找（`f` 表示文件，`d` 表示目录）。
- `-size`：按文件大小查找。
- `-mtime`：按修改时间查找。
- `-exec`：对找到的文件执行命令。
- `-print`：打印找到的文件路径（默认行为）。

### 示范

1. **按文件名查找**：
   ```bash
   find /path/to/search -name "file.txt"
   ```
   这个命令会在 `/path/to/search` 目录及其子目录中查找名为 `file.txt` 的文件。

2. **按文件名查找（不区分大小写）**：
   ```bash
   find /path/to/search -iname "file.txt"
   ```
   这个命令会在 `/path/to/search` 目录及其子目录中查找名为 `file.txt` 的文件，不区分大小写。

3. **按文件类型查找**：
   ```bash
   find /path/to/search -type f
   ```
   这个命令会在 `/path/to/search` 目录及其子目录中查找所有文件。

   ```bash
   find /path/to/search -type d
   ```
   这个命令会在 `/path/to/search` 目录及其子目录中查找所有目录。

4. **按文件大小查找**：
   ```bash
   find /path/to/search -size +100M
   ```
   这个命令会在 `/path/to/search` 目录及其子目录中查找大于 100MB 的文件。

5. **按修改时间查找**：
   ```bash
   find /path/to/search -mtime -7
   ```
   这个命令会在 `/path/to/search` 目录及其子目录中查找最近 7 天内修改过的文件。

6. **对找到的文件执行命令**：
   ```bash
   find /path/to/search -name "*.txt" -exec rm {} \;
   ```
   这个命令会在 `/path/to/search` 目录及其子目录中查找所有 `.txt` 文件，并删除它们。

### 综合示范
假设你想在 `/home/user` 目录下查找所有 `.log` 文件，并且这些文件的修改时间在最近 30 天内，然后删除它们：
```bash
find /home/user -name "*.log" -mtime -30 -exec rm {} \;
```

通过这些示范，你可以灵活地使用 `find` 命令来查找文件和目录，并根据需要执行相应的操作。`find` 命令非常强大，可以满足各种复杂的搜索需求。

![[Pasted image 20240716010146.png]]

#### 3.1.10 ls


`ls` 命令是 Linux 和 Unix 系统中最常用的命令之一，用于列出目录内容。以下是 `ls` 命令的常用示范和参数解释：

### 基本语法
```bash
ls [选项] [文件或目录]
```

### 常用选项
- `-l`：以长格式显示文件和目录的详细信息。
- `-a`：显示所有文件，包括隐藏文件（以`.`开头的文件）。
- `-h`：以人类可读的格式显示文件大小（例如，K、M、G）。
- `-R`：递归显示目录及其子目录中的所有文件。
- `-t`：按修改时间排序，最新的文件在前。
- `-r`：反向排序。
- `-S`：按文件大小排序，最大的文件在前。

### 示范

1. **列出当前目录下的文件和目录**：
   ```bash
   ls
   ```

2. **以长格式显示当前目录下的文件和目录**：
   ```bash
   ls -l
   ```

3. **显示所有文件，包括隐藏文件**：
   ```bash
   ls -a
   ```

4. **以人类可读的格式显示文件大小**：
   ```bash
   ls -lh
   ```

5. **递归显示目录及其子目录中的所有文件**：
   ```bash
   ls -R
   ```

6. **按修改时间排序，最新的文件在前**：
   ```bash
   ls -lt
   ```

7. **反向排序**：
   ```bash
   ls -lr
   ```

8. **按文件大小排序，最大的文件在前**：
   ```bash
   ls -lS
   ```

### 综合示范
假设你想列出当前目录下的所有文件和目录，包括隐藏文件，并以长格式显示详细信息，同时以人类可读的格式显示文件大小：
```bash
ls -lha
```

通过这些示范，你可以灵活地使用 `ls` 命令来列出目录内容，并根据需要选择合适的选项。`ls` 命令是日常使用中非常实用的工具，可以帮助你快速查看和管理文件和目录。

![[Pasted image 20240716010503.png]]
![[Pasted image 20240716010555.png]]


#### 3.1.11 sed
`sed`（Stream Editor）是一个强大的文本处理工具，广泛用于 Linux 和 Unix 系统中。它可以对文本进行查找、替换、删除、插入等操作。以下是 `sed` 命令的常用示范和参数解释：

### 基本语法
```bash
sed [选项] '命令' 文件
```

### 常用选项
- `-n`：仅显示处理后的结果。
- `-e`：允许多个命令。
- `-i`：直接修改文件内容。

### 常用命令
- `s/旧字符串/新字符串/`：替换字符串。
- `d`：删除行。
- `a`：在指定行后添加内容。
- `i`：在指定行前插入内容。
- `p`：打印行。

### 示范

1. **替换字符串**：
   ```bash
   sed 's/old/new/' file.txt
   ```
   这个命令会将 `file.txt` 中的每一行的第一个 `old` 替换为 `new`。

2. **全局替换字符串**：
   ```bash
   sed 's/old/new/g' file.txt
   ```
   这个命令会将 `file.txt` 中的所有 `old` 替换为 `new`。

3. **仅显示处理后的结果**：
   ```bash
   sed -n 's/old/new/p' file.txt
   ```
   这个命令会将 `file.txt` 中的 `old` 替换为 `new`，并仅显示处理后的结果。

4. **删除行**：
   ```bash
   sed '/pattern/d' file.txt
   ```
   这个命令会删除 `file.txt` 中包含 `pattern` 的行。

5. **在指定行后添加内容**：
   ```bash
   sed '/pattern/a new_line' file.txt
   ```
   这个命令会在 `file.txt` 中包含 `pattern` 的行后添加 `new_line`。

6. **在指定行前插入内容**：
   ```bash
   sed '/pattern/i new_line' file.txt
   ```
   这个命令会在 `file.txt` 中包含 `pattern` 的行前插入 `new_line`。

7. **直接修改文件内容**：
   ```bash
   sed -i 's/old/new/g' file.txt
   ```
   这个命令会直接修改 `file.txt` 中的内容，将所有 `old` 替换为 `new`。

### 综合示范
假设你想将 `file.txt` 中的所有 `apple` 替换为 `orange`，并且直接修改文件内容：
```bash
sed -i 's/apple/orange/g' file.txt
```

通过这些示范，你可以灵活地使用 `sed` 命令来处理文本，并根据需要选择合适的选项和命令。`sed` 命令是文本处理中非常实用的工具，可以帮助你快速完成各种复杂的文本操作。

![[Pasted image 20240716012114.png]]


### 3.2 进程管理

pstree执行时发现缺少，需要安装。
sudo apt-get install psmisc

关于各个命令使用示例：

- `ps`：列出当前系统中的进程。使用不同的选项可以显示不同的进程信息，例如：
    - ```shell
        ps aux  # 显示系统所有进程的详细信息
        ```
        
- `top`：动态显示系统中进程的状态。它会实时更新进程列表，显示CPU和内存使用率最高的进程。
    - ```shell
        top  # 启动top命令，动态显示进程信息
        ```
        
- `pstree`：以树状图的形式显示当前运行的进程及其父子关系。
    - ```shell
        pstree  # 显示进程树
        ```
        
- `pgrep`：查找匹配条件的进程。可以根据进程名、用户等条件查找进程。
    - ```shell
        pgrep -u username  # 查找特定用户的所有进程
        ```
        
- `nice`：更改进程的优先级。`nice` 值越低，进程优先级越高。
    - ```shell
        nice -n 10 long-running-command  # 以较低优先级运行一个长时间运行的命令
        ```
        
- `jobs`：显示当前终端会话中的作业列表，包括后台运行的进程。
    - ```shell
        jobs  # 列出当前会话的后台作业
        ```
        
- `bg` 和 `fg`：`bg` 将挂起的进程放到后台运行，`fg` 将后台进程调回前台运行。
    - ```shell
        bg  # 将最近一个挂起的作业放到后台运行
        fg  # 将后台作业调到前台运行
        ```
        
- `kill`：发送信号到指定的进程，通常用于杀死进程。
    - ```shell
        kill PID  # 杀死指定的进程ID
        ```
        
    - 注意，`kill` 命令默认发送 `SIGTERM` 信号，如果进程没有响应，可以使用`-9`使用`SIGKILL` 信号强制杀死进程：
        
    - ```shell
        kill -9 PID  # 强制杀死进程    
        ```
        

> `SIGTERM`（Signal Termination）信号是Unix和类Unix操作系统中用于请求进程终止的标准信号。当系统或用户想要优雅地关闭一个进程时，通常会发送这个信号。与`SIGKILL`信号不同，`SIGTERM`信号可以被进程捕获并处理，从而允许进程在退出前进行清理工作。

## 关卡任务
### linux闯关任务
vscode中remote-ssh连接后编辑代码hello_world.py。
![[Pasted image 20240716172644.png]]
在vscode，terminal中执行代码。
![[Pasted image 20240716175008.png]]
在ports中映射端口。
![[Pasted image 20240716175033.png]]
在本地电脑上就可以显示服务器的页面了。
![[Pasted image 20240716175111.png]]

### 可选任务1（linux基础命令）
如笔记上部分。

### 可选任务2（vscode远程开发并创建一个conda环境）
该conda环境名为demo。
![[Pasted image 20240716175420.png]]
创建完成，并激活环境demo。
![[Pasted image 20240716180024.png]]
### 可选任务3（创建并执行test.sh脚本）
在demo环境中，创建并激活test.sh脚本
![[Pasted image 20240716180930.png]]

