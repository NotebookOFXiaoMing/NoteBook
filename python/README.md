# python杂七杂八的知识点

python 统计某个目录下符合特定命名的文件数量

```
import glob
glob.glob("/tmp/dir_*")
len(glob.glob("/tmp/dir_*"))
glob.glob("/tmp/dir_*/*_cp.gbf")
```

pip 安装模块指定清华源

```
pip install bcbio-gff -i https://pypi.tuna.tsinghua.edu.cn/simple
```

python 写脚本的时候生成参数

之前自己是使用argparse这个模块，今天看到了一个click模块 链接 https://click.palletsprojects.com/en/8.1.x/

用起来比argparse 这个模块更简单，官方文档上给出的例子

```
import click

@click.command()
@click.option('--count', default=1, help='Number of greetings.')
@click.option('--name', prompt='Your name',
              help='The person to greet.')
def hello(count, name):
    """Simple program that greets NAME for a total of COUNT times."""
    for x in range(count):
        click.echo(f"Hello {name}!")

if __name__ == '__main__':
    hello()
```

我将这个文件命名为`try_click.py`,如果执行`python try_click.py` 不加参数执行 会让你一行一行输入参数 也可以直接加参数执行  `python .\try_click.py --count 8 --name xiaoming`
