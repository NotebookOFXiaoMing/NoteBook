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
