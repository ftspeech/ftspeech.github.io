---
layout: page
title: Documentation
sidebar_link: true
---

<br/>

**FT Speech** is a new speech corpus created from the recorded meetings of the Danish Parliament, also known as the _Folketing_ (FT). It contains over 1,800 hours of transcribed speech by a total of 434 speakers, which are partitioned into five subsets with no speaker overlap between train, development, and test data. The corpus partitions and their size in hours and number of utterances are shown in the table below. The speaker counts by gender are marked as **F** (female) and **M** (male). The subsets _dev-balanced_ and _dev-other_ contain the same set of speakers, but _dev-balanced_ contains approximately equal amounts of speech per speaker. The same is true for _test-balanced_ and _test-other_.


| Subset        |    Hours | Utterances | Speakers (F+M) |
|---------------|---------:|-----------:|---------------:|
| train         | 1,816.29 |    995,677 |  374 (146+228) |
| dev-balanced  |     5.03 |      2,601 |     20 (10+10) |
| dev-other     |    14.96 |      7,595 |                |
| test-balanced |    10.05 |      5,534 |     40 (20+20) |
| test-other    |    10.88 |      5,837 |                |
| **Total**         | **1,857.21** |  **1,017,244** |  **434 (176+258)** |


Since we cannot release audio data in a segmented form due to the restricted licence, we are releasing full-length audio recordings of the FT meetings in wav format together with the utterance transcripts time-coded with respect to the source audio in text format.  

The data set is divided into the audio and textual portions: 

1. The **audio part** contains 1003 wav files sampled at 16 kHz using a 16-bit linear PCM sample encoding (`PCM_S16LE`). Each audio file corresponds to a full-length recording of one parliamentary meeting. The meeting recordings are sorted chronologically and subdivided into 10 directories: `2010` – `2019`. 
   - The name of each subdirectory refers to the calendar year beginning one parliamentary year, which runs from the first Tuesday in October to the first Tuesday in October of the following year. Thus, for instance, the meetings that took place in parliamentary year 2010-2011 will be found in the subdirectory `audio/2010/`. 
  
   - The audio files are named after their meeting ids (`meeting_id.wav`), which are taken from the FT website and formatted as such `<year_subdir><collection_number>_M<meeting_number>`, where `<meeting_number>` refers to the ordinal number of the meeting in a given parliamentary year. This means, for example, that the audio file `audio/2016/20161_M041.wav` is a recording of the 41st meeting in parliamentary year 2016-17 whose unique id is `20161_M041`. The `collection_number` can be either `1` or `2`. The 2nd collection appears only in years with parliamentary elections and includes the meetings taking place after the election date.
   
2. The **textual part** consists of five tsv files with equivalent structure, each corresponding to one of the data set partitions presented above. Each tsv file contains the following five columns: `utterance_id`, `speaker_gender`, `start_time`, `end_time`, and `transcript`.

   - `utterance_id` includes information on `speaker_id` and `meeting_id`. For example, for an utterance titled `S001_20151_M012_P00034-2`, the first element `S001` is the *speaker id* and the second two elements `20151_M012` are the *meeting id*. This means that the utterance is found in the audio file `audio/2015/20151_M012.wav`.

   - `speaker gender` is a binary category with values `F`(emale) and `M`(ale) indicating the gender of the speaker obtained from their public biography available on the FT website.
  
   - `start_time` and `end_time` refer to the beginning and end time of an utterance with respect to the source audio file, given in seconds.

   - `transcript` contains orthographic transcriptions of the utterances as extracted from the official reports of the parliamentary meetings. All utterance text is normalized by expanding common abbreviations, numbers, dates, and symbols, as well as removing all punctuation, capitalization, and unspoken parenthetical remarks and references. A number of utterances begin and/or end with the silence token `<UNK>` indicating an utterance fragment which occurs when the audio segment is not perfectly aligned with the utterance boundaries.


**Nota bene**: Before using the data, it is recommended that you verify the integrity of your download. You may do this by generating an MD5 hash value for each of the downloaded data files and comparing them to our hash values, which can be found in the file `md5sums.txt`. You can do this by executing the commands below, where the `grep` command finds all lines in `my_md5sums.txt` that do not match any of the lines in our `md5sums.txt`. You should not get any audio or tsv text files in the output.  

```
cd FTSpeech
find . -type f -exec md5sum '{}' + > my_md5sums.txt
grep -vf md5sums.txt my_md5sums.txt
```

The MD5 hash value of the file `md5sums.txt` is `e5697b9a5b4b46531e39a2d67c975b2f`.  

<br/>


## Reference

For more information on how **FT Speech** was created and evaluated, please refer to the paper [*FT&nbsp;Speech: Danish Parliament Speech Corpus*](https://arxiv.org/abs/2005.12368). Please cite it when using FT Speech as:

```{% raw %}
@inproceedings{ftspeech,
  author    = {Kirkedal, Andreas and Stepanović, Marija and Plank, Barbara},
  title     = {{FT Speech: Danish Parliament Speech Corpus}},
  booktitle = {Proc. Interspeech 2020},
  year      = {2020}
}
{% endraw %}```

