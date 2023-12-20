# Pytorch-alphazero

## 如何理解?
由于我们未来将使用1步,2格选1这类,因此mcts近乎无用
注意,reformat.py写入文件时用了多线程,仔细看看


## 我们需要运行它
以便简单的设定断点调试,查看数据

## 调整:
1. 注意修改.gitignore,增加:
cclr/
cclr-data/
*.pgn
避免因为这些文件,git会监控,导致转换速度下降
1. chess.pgn
pip install chess
注意不是python-chess
然后可以引用:from chess import pgn 或者 import chess.pgn
1. 下载数据集
https://lczero.org/blog/2018/09/a-standard-dataset/
 You can download the dataset in pgn- format (539M) and v3-format (11G).
 我们当然下载较小的版本 539m那个
 会显示无法安全下载,我们可在下载项目中,选择保留,仍然保留

1. 将ccrl-pgn.tar.bz2文件拷贝到项目根目录
   使用winrar解压到当前目录,会增加一个cclr文件夹

1. 修改reformat.py
主要是目录,我们放在项目根目录下,所以
ccrl_dir = 'cclr/train'
#the new dir
reformat_dir = 'cclr'
这样转换后的数据就在cclr目录下了
然后简单运行reformat.py
这个过程很慢,大体要1-2小时

1. 之后就运行train
先设置文件夹:
ccrl_dir = 'ccrl'
我们需要理解其模型训练的过程,比如策略头和价值头的特征和标签是什么,输出又是什么
需要注意,训练过程中mcts并没有作用
它只在play时有用,由于没有self-play,而是直接使用国际象棋对局训练,因此mcts仅仅用于play
