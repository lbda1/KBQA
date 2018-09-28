# KBQA
KBQA(基于匹配度的)
附件是代码和结果文件，详细说明如下
---------------------------------------------------------------------------------------------------------------
代码和数据都已经共享到https://pan.baidu.com/s/1duD_o6ZdmTOTlJqj2lCGwg
代码文件也挺大的，最好直接从网盘下载使用。
代码是CCKS_LEQA_code.zip
数据是data.rar
下载这两个文件之后直接在同一目录解压即可。
------------------------------------------------------------------------------------------
第一种执行方式：数据预处理好的以及train好的模型执行说明（进入代码中BiMPM文件夹下）
1 环境说明
    Linux    
    python3
    tensorflow 1.3
    Cuda 8.0
2 执行步骤
(1)sh test_pipline_8_25_first.sh
(2)sh test_pipline_15_25_second.sh
(3)sh answer_merge_third.sh

3 输入 
输入：BiMPM目录下CCKS_KBQA_Data_0719_8_25或者CCKS_KBQA_Data_0719_15_25

4 输出
输出答案：BiMPM/src/answer_unique_last_submit.txt

注意：如果想要重新训练可以执行sh train_pipline.sh（但是最好把BiMPM/data/word_char_fix/model中保存的模型删除）
------------------------------------------------------------------------------------------------
第二种执行方式：数据预处理到最后模型整体流程
1环境说明
    Linux    
    python3
    tensorflow 1.3
    Cuda 8.0
    scikit-learn
    jieba分词
    Hanlp
    apache maven
    apache poi
    jdk1.8

2 候选triple选取和预排序
注意：直接使用的是我们编译好的jar包，并且用shell串联起来。
我们也提供了源码文件KBQA.rar（在网盘的data.rar中https://pan.baidu.com/s/1mOJ-gZ0aY5sMxEgmhTNRMA密码h83z），可以自己打包。
源码编译打包方式见http://bglmmz.iteye.com/blog/2058785。
下载数据data.rar解压缩之后放入根目录下。
2.1 执行步骤
sh CandidatePath.sh
2.2 特别注意
必须使用jdk1.8
需要使用80g运行内存（用于知识库加载和处理）
2.3 输入
输入问题路径：data/COQA/question
其中task4coqa_train.txt, task4coqa_valid.txt,test.questions 这三个文件不可缺少
2.4 输出谓词选择模型的training data和test data
out/rank/test_rank2.txt
out/rank/train_rank2.txt

3 候选triple数据格式转换（进入data_transfer_for_BiMPM目录）
直接执行 python data_transfer_for_BiMPM/CCKS_data_process_2018_SPO_0715.py
输入是上一步的输出
输出在data_transfer_for_BiMPM/data_CCKS/input_2_mpcnn中
training.txt
test.txt
train_prob_1.txt
test_prob_1.txt
test_answer_2.txt

4 谓词选择模型
首先将上模块生成的数据放入BiMPM/CCKS_KBQA_Data_0719_8_25
然后可以按照第一种方式进行执行了
