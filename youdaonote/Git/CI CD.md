CI（continuous integration） 持续集成 - CD（continuous delivery）持续交付

CD（continuous deploy）持续部署：是将持续交付的过程自动化



- Jenkins是一个比较流行的持续集成工具

- GitLab是存储镜像的镜像仓库

     







.gitlab-ci.yml文件结构





.gitlab-ci.yml 是指定了 CICD 相关配置的 YAML 文件。（YAML 是专门用来写配置文件的语言，简洁强大，和 python 一样用缩进代表层级，表达能力和 JSON 基本一致，但格式更方便。



一般而言，CICD 过程会包含如下最外层的 key：

- stages: 定义整个 CICD pipeline 的 job 数量和名称

- variables: 定义 CICD 流程中的一些环境变量

- before_scripts: 在每个 job 的 scripts 执行前进行的命令集，一般是创建目录，打印 context 目录等操作，可类比 unittest 的 setUp 方法

- stage: 定义了一个 job 的具体流程，可以在前面加上名称

- script:
     - <build related command here>

- artifacts：定义 job 的产出，比如我们让 test_stage 产出一个 html 格式的报告，显示每个单元测试的执行情况（报告生成相关代码写在项目内）。 数组内的 paths 和 when 分别定义报告的路径和产出场景

- when：表示何时在在 Gitlab 上触发。always，manual手动触发

- only：指明了 job 的执行场景，可以是分支名，表明只有 master 分支可以执行 build，如果要用排除法反向指定，可以用 except。

