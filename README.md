# chatbot

Python版本不能太新，一些旧版本的依赖包跟不上python最新版本，3.6比较好
而且要下64位的，32位内存可能不够

安装spacy，要以管理员身份运行cmd，再在里面执行命令
pip install spacy
python -m spacy download en_core_web_md
https://blog.csdn.net/u012436149/article/details/79321112
检测：import spacy；import en_core_web_md

安装rasa_nlu以及相应的依赖包
https://github.com/RasaHQ/rasa_nlu
https://stackoverflow.com/questions/46713653/installing-rasa-on-windows
检测：
先克隆到本地git clone https://github.com/RasaHQ/rasa_nlu.git
然后看看能不能顺利运行下面的语句
from rasa_nlu.training_data import load_data
from rasa_nlu.config import RasaNLUModelConfig
from rasa_nlu.model import Trainer
from rasa_nlu import config
trainer = Trainer(config.load(“D:\\...\\rasa_nlu\\sample_configs\\config_spacy.yml”))
training_data = load_data(“D:\\...\\rasa_nlu\\data\\examples\\rasa\\demo-rasa.json”)
interpreter = trainer.train(training_data)
如果是英文版聊天，这个就够了，只需要自己再写一个自己专用的.json文件就可以了

下面是中文版：
安装jieba

安装cmake和mitie（git命令要在gitbash里面运行，cmd无法运行）
https://blog.csdn.net/m0_37407756/article/details/79790417
https://blog.csdn.net/ld326/article/details/80965689

下载total_word_feature_extractor_zh.dat（total_word_feature_extractor_chi.dat），是个300多兆的训练集，下面网址里有提到的百度网盘里面有
http://www.crownpku.com/2017/07/27/用Rasa_NLU构建自己的中文NLU系统.html

clone rasa_nlu_chi：还是上面那个网址

打开rasa_nlu_chi 的sample_configs文件夹，找到config_jieba_mitie_sklearn.yml，将里面model后面的内容改成300多兆.dat文件的详细路径，如：
"D:/EE/data/total_word_feature_extractor_zh.dat"

自己编写.json训练数据
