# sys.argv[]的使用方法


> sys.argv变量是一个字符串的列表。sys.argv包含了命令行参数 的列表，即使用命令行传递给你的程序的参数。

比如： 当执行`python using_sys.py we are arguments`时，使用python 命令运行`using_sys.py`模块，后面接着的内容视为参数传递给程序。

Python为我们把它存储在`sys.argv`变量中。

脚本的名称**总是**`sys.argv`列表的第一个参数。即`using_sys.py`是sys.argv[0]。这里，`we`是sys.argv[1]，`are`是sys.argv[2]，`arguments`是sys.argv[3]。另外，sys.startswith()是用来判断一个对象以什么开头的。如输入`'abcde'.startswith('ab')`就会返回True

### 实例
```Python
# 脚本名称：test.py 运行：python test.py --version help
#!/usr/bin/python
import sys
def readfile(filename):
    '''
    print a file to the standard output.
    '''
    f = file(filename)
    while True:
         line  = f.readline()
         if len(line) == 0:
             break
         print (line)
    f.close()
print ("sys.argv[0]------",sys.argv[0])
print ("sys.argv[1]------",sys.argv[1])
print ("sys.argv[2]------",sys.argv[2])
# script starts from here
if len(sys.argv) < 2:
    print ('No action specified.')
    sys.exit()
if sys.argv[1].startswith('--'):
    option = sys.argv[1][2:]
    # fetch sys.argv[1] but without the first two characters
    if option == 'version':
        print ('version 1.2')
    elif option == 'help':
        print (''' "This program prints files to the standard output.
        any number of files can be specified.
        options include:
        --version: prints the version number
        --help: display the help''')
    else:
        print ('Unknown option.')
        sys.exit()
else:
    for filename in sys.argv[1:]:
        readfile(filename)
```
 注意：sys.argv[1][2:]表示的意思是：从第二个参数，第三个字符开始截取到最后结尾，本例结果为：version