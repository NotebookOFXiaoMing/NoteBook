# linux杂七杂八的知识点

linux 复制文件重命名

```
cp file.txt file01.txt
```

用命令行将服务器端文件下载到本地

```
scp xiaoming@124.70.145.183:/tmp/dir_Gl_VKU_cp/Gl_VKU_cp.tar.gz D:\Bioinformatics_Intro\
```


关于slurm集群任务调度系统，参考 https://help.cropdiversity.ac.uk/slurm-overview.html

关于slurm参考链接 

- https://zhuanlan.zhihu.com/p/345387783

- https://docs.hpc.sjtu.edu.cn/job/slurm.html

- http://hmli.ustc.edu.cn/doc/linux/slurm-install/slurm-install.html#id31

- https://zhuanlan.zhihu.com/p/356415669 这个写的挺详细的

查看所有节点的信息 `sinfo -N`

- idle unused 未被使用
- mix partially used by running jobs 局部使用
- alloc completed occupied 完全被占用

使用其中的某一个节点

`srun --pty bash` by default 1 CPU and 1.5 GB of memory

使用其中某一个节点，指定CPU和MEM

```
srun --cpus-per-task=8 --mem=16G --pty bash
```

使用指定分区的节点

```
srun --cpus-per-task=16 --mem=32G --partition=tcum256c128Partition --pty bash
```

查看自己账号下的运行任务

```
squeue -u username
```

取消任务

```
scancel jobid
scancel -u  username
```

提交任务的脚本

```
#!/bin/bash

#SBATCH --job-name="pomeRTD"
#SBATCH --mail-user=mingyan24@126.com
#SBATCH --mail-type=BEGIN,END,FAIL
#SBATCH --cpus-per-task=8
#SBATCH --mem=16G

source activate snakemake
snakemake --cluster "sbatch --output=/snakemake_pipeline/slurm.out/%j.out \
--error=/snakemake_pipeline/slurm.out/%j.out --cpus-per-task={threads} \
--mail-type=END,FAIL --mail-user=mingyan24@126.com --mem={resources.mem}" \
--jobs 12 -s pomeRTD_snakemake_v01.py

```

查看每个节点的信息 (cpu和内存)

```
sinfo -o "%n %e %m %a %c %c"
```

查看作业信息 参考链接 https://hpc.pku.edu.cn/_book/guide/slurm/sacct.html

```
scontrol show job
```

显示正在运行的任务信息

```
scontrol show job 476717
```
加上具体的任务号显示特定的任务

```
sacct -j 7454119
```
输出内容会包括，作业号，作业名，分区，计费账户，申请的CPU数量，状态，结束代码

JobID    JobName  Partition    Account  AllocCPUS      State ExitCode
最后介绍如何通过sacct按照指定格式输出作业信息；

入下所示，指定输出内容为：作业号，作业名，分区，运行节点，申请核数，状态，作业结束时间；
```
format=jobid,jobname,partition,nodelist,alloccpus,state,end
sacct --format=$format -j 7454119
```

mamba 这个软件

```
mamba repoquery search samtools
mamba repoquery depends samtools
```

mamba 安装软件最开始很顺畅，最近一直会有报错，报错很长，暂时看不懂是什么原因，还是使用回conda, 运行完conda install software会卡很久，查了一下原因，有人说需要对conda进行更新，有人说可以使用离线模式进行安装，首先是到 https://anaconda.org/ 找到对应的安装包，然后使用命令 `conda install --offline fastp-0.23.2-h5f740d0_3.tar.bz2`进行安装，安装成功，但是fastp不能用，报错是 `fastp: error while loading shared libraries: libisal.so.2: cannot open shared object file: No such file or directory`,我猜可能的原因是离线安装，软件的依赖问题不能很好的解决，瞎说的，不确定

临时添加环境变量

```
export PATH=/home/myan/biotools/bamtools/build/src/:$PATH
```

两台服务器之间拷贝数据

```
scp username@ipaddress:/home/folder/file.txt /home/folder/
```

conda 可用的镜像汇总 https://zhuanlan.zhihu.com/p/584580420
