# Linux

## 1 文件篇

### 1.1 统计文件大小

```markdown
du [option]... [file]

-c 显示总计
-h 人类可读
-s 对每个参数只显示总大小
-t 值为正时，排除小于该值，否则，排除大于该值
```

#### 1.1.1 例子

```bash
# 查看文件夹子级大小
du -shc /*
```

### 1.2 文件状态

```
stat [file]

输出:
Access 最后读取时间
Modify 文件内容最后修改时间
Change 文件元数据最后修改时间
```

### 1.3 查找文件

```
find

1. 按类型查找：
	-type f 普通文件, d 目录

2. 按文件状态查找：
  +n 大于
  -n 小于

  Access状态
  -atime n*24小时前
  -amin  n分钟前

  Modify状态
  -mtime n*24小时前
  -mmin  n分钟前
  -newermt t时间后
  ! -newermt t时间前
  -newer 比f新
  ! -newer 比f老

  Change状态
  -ctime n*24小时前
  -cmin  n分钟前

3. 按名称查找
	--name pattern

4. 查找后执行
	-exec [command] '{}' +
	其中
	'{}'为查找结果占位符
	+ 为分隔符，可用 \; 代替
```

#### 1.3.1 例子

```bash
# 查找30天前修改的文件
find . -type f -mtime +30

# 查找30天内修改的文件
find . -type f -mtime -30

# 查找2021-06-01后修改的文件
find . -type f -newermt '2021-06-01'

# 查找2021-06-01前修改的文件
find . -type f ! -newermt '2021-06-01'

# 查找比1.txt文件修改时间新的文件
find . -type f -newer 1.txt

# 查找后显示文件信息
find . -type f -exec ls -lh '{}' +
```

