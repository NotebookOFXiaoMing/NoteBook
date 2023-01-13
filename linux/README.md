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
