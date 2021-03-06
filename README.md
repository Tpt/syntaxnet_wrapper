# A Python Wrapper for Google SyntaxNet

## Installation

#### Prerequisites

Install `bazel` and include `bazel` in `$PATH`.

```shell-script
wget https://github.com/bazelbuild/bazel/releases/download/0.4.3/bazel-0.4.3-installer-linux-x86_64.sh
chmod +x bazel-0.4.3-installer-linux-x86_64.sh
./bazel-0.4.3-installer-linux-x86_64.sh --user
rm bazel-0.4.3-installer-linux-x86_64.sh
export PATH="$PATH:$HOME/bin"
```

Install OpenJDK8.

```shell-script
add-apt-repository -y ppa:openjdk-r/ppa
apt-get -y update
apt-get -y install openjdk-8-jdk
```

Install system package dependencies.

```shell-script
apt-get -y install swig unzip
```

Install Python packages

```shell-script
pip install tensorflow protobuf asciitree mock
```


#### Start Installing

```shell-script
pip install git+ssh://git@github.com/livingbio/syntaxnet_wrapper.git#egg=syntaxnet_wrapper
```

## Usage

```python
from syntaxnet_wrapper import tagger, parser

print tagger['en'].query('this is a good day', returnRaw=True)
# 1       this    _       DET     DT      _       0       _       _       _
# 2       is      _       VERB    VBZ     _       0       _       _       _
# 3       a       _       DET     DT      _       0       _       _       _
# 4       good    _       ADJ     JJ      _       0       _       _       _
# 5       day     _       NOUN    NN      _       0       _       _       _
tagger['en'].query('this is a good day')  # in default, return splitted text

print parser['en'].query('Alice drove down the street in her car', returnRaw=True)
# 1       Alice   _       NOUN    NNP     _       2       nsubj   _       _
# 2       drove   _       VERB    VBD     _       0       ROOT    _       _
# 3       down    _       ADP     IN      _       2       prep    _       _
# 4       the     _       DET     DT      _       5       det     _       _
# 5       street  _       NOUN    NN      _       3       pobj    _       _
# 6       in      _       ADP     IN      _       2       prep    _       _
# 7       her     _       PRON    PRP$    _       8       poss    _       _
# 8       car     _       NOUN    NN      _       6       pobj    _       _

# use Chinese model
print tagger['zh'].query(u'今天 天氣 很 好', returnRaw=True)
# 1       今天    _       NOUN    NN      _       0       _       _       _
# 2       天氣    _       NOUN    NN      _       0       _       _       _
# 3       很      _       ADV     RB      _       0       _       _       _
# 4       好      _       ADJ     JJ      _       0       _       _       _

print parser['zh'].query(u'今天 天氣 很 好', returnRaw=True)
# 1       今天    _       NOUN    NN      _       4       nmod:tmod       _       _
# 2       天氣    _       NOUN    NN      _       4       nsubj   _       _
# 3       很      _       ADV     RB      _       4       advmod  _       _
# 4       好      _       ADJ     JJ      _       0       ROOT    _       _
```

### Language Selection

The default model is `'English-Parsey'`. This is
[announced by Google](https://research.googleblog.com/2016/05/announcing-syntaxnet-worlds-most.html)
on May, 2016.
Other models, includes `'English'`, are trained by [Universal Dependencies](http://universaldependencies.org/),
[announced by Google](https://research.googleblog.com/2016/08/meet-parseys-cousins-syntax-for-40.html)
on August, 2016.

```python
from syntaxnet_wrapper import language_code_to_model_name
language_code_to_model_name
# {'ar': 'Arabic',
#  'bg': 'Bulgarian',
#  'ca': 'Catalan',
#  'cs': 'Czech',
#  'da': 'Danish',
#  'de': 'German',
#  'el': 'Greek',
#  'en': 'English-Parsey',
#  'en-uni': 'English',
#  'es': 'Spanish',
#  'et': 'Estonian',
#  'eu': 'Basque',
#  'fa': 'Persian',
#  'fi': 'Finnish',
#  'fr': 'French',
#  'ga': 'Irish',
#  'gl': 'Galician',
#  'hi': 'Hindi',
#  'hr': 'Croatian',
#  'hu': 'Hungarian',
#  'id': 'Indonesian',
#  'it': 'Italian',
#  'iw': 'Hebrew',
#  'kk': 'Kazakh',
#  'la': 'Latin',
#  'lv': 'Latvian',
#  'nl': 'Dutch',
#  'no': 'Norwegian',
#  'pl': 'Polish',
#  'pt': 'Portuguese',
#  'ro': 'Romanian',
#  'ru': 'Russian',
#  'sl': 'Slovenian',
#  'sv': 'Swedish',
#  'ta': 'Tamil',
#  'tr': 'Turkish',
#  'zh': 'Chinese',
#  'zh-cn': 'Chinese',
#  'zh-tw': 'Chinese'}
```
