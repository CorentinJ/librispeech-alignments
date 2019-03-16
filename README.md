# LibriSpeech Alignments

This repo contains links to download word alignments for [LibriSpeech](http://www.openslr.org/12/), generated using the [Montreal Forced Aligner](https://montreal-forced-aligner.readthedocs.io/).

The following datasets are included:
 - LibriSpeech/dev-clean
 - LibriSpeech/dev-other
 - LibriSpeech/test-clean
 - LibriSpeech/test-other
 - LibriSpeech/train-clean-100
 - LibriSpeech/train-clean-360
 - LibriSpeech/train-other-500

## Download links

The prepared alignments come in two formats:
 - A simple, condensed format (a .txt file for all utterances of a book), all words are mapped from the ground truth. [Google drive link]( https://drive.google.com/file/d/1WYfgr31T-PPwMcxuAq09XZfHQO5Mw8fE/view?usp=sharing) (70mb archive, 173mb contents) **[recommended]**
 - The raw output from MFA (a .TextGrid file for each utterance), some words are unknown (see the examples below). [Google drive link](https://drive.google.com/file/d/1OgfXbTYhgp8NW5fRTt_TXwViraOyVEyY/view?usp=sharing) (594mb archive, 3.5gb contents) **[you shouldn't need this]**

Once downloaded, merge the LibriSpeech directory with the original LibriSpeech dataset (only the directory structure will be merged, no files should be overwritten in the process).
 
**Warning:** for both archives there will be a set of unaligned utterances (see unaligned.txt), for these files there will simply be no alignment present, so take that into account in your parsers. There are 46 utterances unaligned in the raw TextGrid alignments (from failures of the model) and 127 in the simple format alignments (46 carried out from the first and 81 from being unable to match the text to the ground truth text). I wouldn't bother trying to annotate those in another way, as they still account for less than ~0.05% of the whole dataset.

## Format (TXT alignments)
For each book you will find a <book_id>.alignment.txt file, e.g.:  
```
LibriSpeech/dev-clean/84/121123:
 - 84-121123.alignment.txt
 - 84-121123.trans.txt
 - 84-121123-0000.flac
 - 84-121123-0001.flac
 - ...
```
Each line starts with the utterance id, followed by the ground truth words and finally the end time for each word. E.g.:
```
84-121123-0000 ",GO,,DO,YOU,HEAR," "0.490,0.890,1.270,1.380,1.490,1.890,2.09" 
84-121123-0001 ",BUT,IN,LESS,THAN,FIVE,MINUTES,THE,STAIRCASE,GROANED,BENEATH,AN,EXTRAORDINARY,WEIGHT," "0.270,0.420,0.530,0.730,0.870,1.100,1.460,1.580,2.080,2.490,2.780,2.860,3.470,3.830,3.99" 
...
```
If an utterance was not aligned (see unaligned.txt), there will be simply no line for it.

The list of words and of end times are surrounded by double quotes, and the items are seperated by commas. **Silences are represented as empty words**, e.g. in the first sentence there is a silence from 0s to 0.49s and the word 'GO' is pronounced from 0.49s to 0.89s. **Each sentence is guaranteed to start and end with a silence, even if its duration is 0**, this is for parsing convenience.

## Format (TextGrid alignments)
For each utterance you will find a .TextGrid file, e.g.:  
```
LibriSpeech/dev-clean/84/121123:
 - 84-121123.trans.txt
 - 84-121123-0000.flac
 - 84-121123-0000.TextGrid
 - 84-121123-0001.flac
 - 84-121123-0001.TextGrid
 - ...
```
If an utterance was not aligned (see unaligned.txt), the corresponding .TextGrid file will be missing.

You can read about the TextGrid format [here](https://montreal-forced-aligner.readthedocs.io/en/latest/data_format.html).
