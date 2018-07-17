# speech-to-speech-translator
This is a translator that compilate softwares and APIs to enable speech-to-speech translation.

Note that this is a compilation of softwares and APIs. By no means is this a standalone speech recognizor, translator, or speech synthesizer.

There are hardware prerequisites in addition to a computer. A microphone is needed for audio input and some form of audio output is needed.

Also, this STS translator is tested on linux with the "Raspberry Pi 2" but should work with other systems. Instructions for other systems are provided as well but might need some modifications.

Dependencies:

[pocketsphinx](https://github.com/cmusphinx/pocketsphinx) for speech recognition

[sphinxbase](https://github.com/cmusphinx/sphinxbase) for speech recognition

[flite](https://github.com/festvox/flite) for speech synthesizing

[ibm language-translator](https://www.ibm.com/watson/services/language-translator/) for translation

# Prerequisites 

1. Curl must be installed

# Linux/Unix installation
Begin with installing sphinxbase:
```python
git clone http://github.com/cmusphinx/sphinxbase
cd sphinxbase
./autogen.sh
./configure
make
sudo make install
```
Then, install pocketsphinx:
```python
git clone http://github.com/cmusphinx/pocketsphinx
cd pocketsphinx
./autogen.sh
./configure
make
sudo make install
```
To install flite:
```python
git clone http://github.com/festvox/flite
cd flite
./configure
make
make get_voices
sudo make install
```
To use IBM's translator, you must first create an account [here](https://www.ibm.com/watson/services/language-translator/). IBM allows an account to have a certain number of characters translated free for each month and does not require a credit card during sign up. We need the URL and API key provided after sign up. 

URL:

On line 68 of translate.cpp, replace (your URL) with the URL IBM provided (e.g.). 

API:

On line 65 of translate.cpp, replace (your key) with the API key IBM provided (e.g.).

Other ajustments:

For lines 75, 239, and 244, (wav file) must be replaced with a path for the creation, deletion, and input of a wav file (e.g.).

For lines 177, 183, and 62, (text file) must be replaced with a path for the creation, deletion, and input of a text file (e.g.).

# Changing language
To setup the language model used by pocketsphinx, first download the desired language model at https://sourceforge.net/projects/cmusphinx/files/Acoustic and Language Models/. In this example, we will use the Spanish language model. You can change this by swapping the language model pocketsphinx uses and changing IBM's settings. 

Open the folder containing the language model and note the following files: filename.dict, filename.lm.bin or filename.lm, and a folder containing the files feat.param, mdef... 

On line 62 of translate.cpp, replace (lm path) with the path to filename.lm.bin (e.g.). Replace (hmm path) with the folder containing the various files (e.g.). Replace (dict path) with the path to filename.dict (e.g.).

On line 68, "es-en" directs IBM translator to translate from Spanish to English. You must set this yourself for your desired language (e.g. en-es to translate from English to Spanish). Note that the language to be translated must match the language model you chose for pocketsphinx. 

# Speech output
Because Flite is used for speech synthesizing, the language in which speech outputs is limited by the selections Flute provide. Right now, the options are... Note that whatever the option, it must match the language chosen to be translated at IBM settings.

To direct Flite to use a specify voice package, 

# Bluetooth
translate.cpp assumes that you use Bluetooth earphones to receive audio output. If that is not the case, then comment out line
