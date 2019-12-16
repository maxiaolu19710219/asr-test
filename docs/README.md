---
主题: asr测试
描述: 提供语音转化成文本(asr)和图像识别(ocr)功能
作者: 马路
标签: asr,ocr
颜色: light yellow
建立时间:  2019/12/16
修改时间: 2019/12/16
---
*zyasr*是一个采用在[PaddlePaddle]平台的端到端自动语音识别（ASR）引擎，具体原理参考这篇论文(http://proceedings.mlr.press/v48/amodei16.pdf)。
愿景是为语音识别在医疗行业，提供易于使用、高效和可扩展的工具，包括自动标注，自我训练，推理，测试模块，以及 快速 部署。

## 目录
- [目标](#目标)
- [准备](#准备)
- [预训练模型](#预训练模型)
- [计划](#计划)
- [下阶段目标](#下阶段目标)


## 目标
1. 训练过语音模型的字错率(正确数/总字数)
2. 未训练过语音模型的字错率(正确数/总字数)
3. 高并发服务器语音解析性能(吞吐量)

## 准备
1.请确保以下库或工具已安装完毕：`xshell`, `filezliia`, `notepad++`,  可以在tools文件夹中找到安装文件。
```server地址：192.168.0.60
  系统用户名：mxl
  系统密码：mxl
  ftp用户名：sunftp
  ftp密码：zhiying
 ```
2. 工具使用说明
```
  cd /mnt/md0/opt/tools
  ls -l
```
其中
asr_start.sh---启动相关服务：kafka，asr引擎，nlp引擎，zookeeper，ak工作流
asr_stop.sh---停止相关服务：同上
status.sh   --- 查看目前asr执行状况，包括未解析记录数，总共要解析记录数。消息监控窗口
3. 相关执行脚本：
启动业务引擎生产者服务
```
kafka-console-producer.sh --broker-list deepspeed:9092 --topic next
```
启动业务引擎消费者服务
```
kafka-console-consumer.sh --bootstrap-server deepspeed:9092 --from-beginning --topic send
```
启动asr消费者服务
````
kafka-console-consumer.sh --bootstrap-server deepspeed:9092 --from-beginning --topic next
````

## 预训练模型
```
cd /mnt/md0/opt/DeepSpeech/dataset/aishell/data_aishell/wav
ls
```
其中dev,test,train三个目录下存放已经训练好的数据，可自行编辑
## 计划
参看plan目录

## 下阶段目标
- 自训练机制(自我标注--自我训练--网格--误差曲面绘制)
<p align="center">
<img src="docs/images/tuning_error_surface.png" width=550>
<br/>
</p>

- 通过热词(表单标签+内容)的积累，通过word2vector模型训练，进行语义推测


