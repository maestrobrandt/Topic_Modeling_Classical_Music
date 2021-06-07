# Topic Modeling Classical Music: Introducing The Song-Chord Matrix

![Project Image](https://media-exp3.licdn.com/dms/image/C4D12AQHV_ay7485IMg/article-cover_image-shrink_720_1280/0/1623088585599?e=1628726400&v=beta&t=g5JUs8QKIwRQInfQtuBEmryPv16aDPa5X7jh4aZi66I)

>Discover how to use deep learning to anaylze classical music, and how to compose new music

___


### Table of Contents
- [Description](#description)
- [Introduction](#introduction)
- [Story](#story)
- [Composing](#composing)
- [Future Consideration](#future-consideration)
- [Author Info](#author-info)

___

## Description

This project used NLP to topic model classical music based on musical chords. Classical composers were then clustered using the topics from the NLP, and then a neural network was used to generate original music based on trained music of the different classical composers. All of these metrics were used as a model for complexity of music.

#### Files
- The code for the project is in Topic_Modeling_Classical_Music.ipynb

#### Technologies
- Python
- Jupyter Notebooks
- Natural Language Processing Models
  - NMF
  - LDA
- Neural Network
  - Autoencoder
___

## Introduction

Music is a diverse medium. We all have preferences regarding the genres that we like, such as hip-hop, rock, pop, etc. Even within classical music, there are differences in styles, such as baroque, romantic, and high classical. In fact, musicologists dedicate entire careers to studying these stylistic differences. There are myriad articles, textbooks, and entire curriculums in universities that focus on how to classify and relate classical music. Coming from a musical background myself, but with a newfound interest in data science, I thought that there must be a way to utilize machine learning to analyze classical music. So my idea - and my research question - was: can I use unsupervised learning to help better understand topical differences in harmony between classical composers?

Before diving into the data science, it is first important to understand the musical side of the project. I was specifically interested in analyzing the harmony of the music. Harmony in music is made from chords. Imagine playing a guitar and strumming different chords; these chords give you different harmonies, and classical music is no different. Harmony plays a huge part in how a song sounds, and can directly impact how complex the song sounds. For instance, I have two examples here. Mozart and Chopin are composers of contrasting styles, and just using my music theory knowledge, I know that Chopin’s music sounds more harmonically complex.

___

## Story

To analyze harmonies of classical music, I got my data from a cross-composer data set. This was a set of MIDI files that came with 10 composers, with a 100 pieces each, resulting in 1000 songs total. Of course, I had to do a bunch of cleaning, and since I wanted to run quasi-NLP analysis on the dataset, I needed it arranged in my song-chord matrix format. Once I had the data in the correct format, I ran NMF (Non-negative Matrix Factorization) on it and observed the topical differences. I also considered n-grams and word2vec to include analysis on phrasing, or the actual progression of chords. For example, if the chord I was looking at was D Major, I considered up 2 two chords preceding and following that chord.

After running my analysis, I settled on 24 topics. This is because the analysis returned topics that were just the keys that the songs were in. There are 24 possible keys: these are based on the 12 different notes in the chromatic scale, both in major and minor tonalities. As a result, there were 24 keys and 24 topics. To give you a better idea, I have provided the first three “topics/keys”. Consistently, all the topics' most common chord was the I chord - this is the name of the key, such A Maj or Eb Maj - followed by the IV or V chord of the key.

![Topics Image](https://media-exp3.licdn.com/dms/image/C4D12AQHQoHRzWsw2zQ/article-inline_image-shrink_1500_2232/0/1623092866191?e=1628726400&v=beta&t=RzlSSrJc6DtJ_O7zLrg5_ThXYgh4RmtjnkhSrrznkTo)

Using t-SNE to visualize does a fairly decent job of discerning the separation between keys. However, when I hue the graph by composers to see the separation between composers, I get a jumbled mess. This was discouraging to me at first, but all this really means is that all of my composers composed pieces in pretty much every different key. In order to uncover meaningful distinctions, I now needed to measure differences in harmonic styles between the composers.

![Keys Image](https://media-exp3.licdn.com/dms/image/C4D12AQF0tADRBMCgGQ/article-inline_image-shrink_1500_2232/0/1623093480490?e=1628726400&v=beta&t=0h8ilf5qgVJO-RTex_QQNtUiegcwLcYHF2Dbp5Nbeb4)

![Composers Image](https://media-exp3.licdn.com/dms/image/C4D12AQGXU8lXbABOZA/article-inline_image-shrink_1500_2232/0/1623093500205?e=1628726400&v=beta&t=CqmRHY4sUXHxDfp7cJtgKDkgXzcg3sTOAC_ifLHIDFk)

I did this by using the model’s confidence that a piece is in a certain key as a measure for the complexity of the piece. If the model is very confident that the piece is in A Major, then the piece is likely to be fairly simple harmonically and does not veer away from the key. If the model is not very confident at all, then the piece is likely to be more experimental and does not stick only to chords from that key. After putting all of my composers and their musical pieces through my model, I came up with a visualization demonstrating the harmonic complexity per composer. Here are the rankings of the average confidence of key per song by composer: Beethoven and Mozart, two high classical composers, are at the top, and Shostakovich, the most modern composer in this set, is at the bottom. Hence, I have backed up my musical theory knowledge on harmonic differences between composers using NLP on chord progressions. This finding is extremely helpful alone, but I took it a step further.

![Rankings Image](https://media-exp3.licdn.com/dms/image/C4D12AQGHcHntN24baw/article-inline_image-shrink_1500_2232/0/1623094026996?e=1628726400&v=beta&t=RDu-mB-uQ5jzVWnaFQg2X-Qxwigi6EwGv4ipJE-eT_A)

___

## Composing

I generated new music by training a neural network to encode music by a certain composer and to compose a new piece based on the learned music. I took the MIDI files of a composer, converted the data to an array, had the neural network encode and model it, then had it generate the output: music. I have provided two generated examples: one from the most harmonically-simple composer, and one from the most complex. Feel free to listen to the differences yourself.

![Beethoven](https://youtu.be/J70VLPFTs_Y)

![Shostakovich](https://youtu.be/rtLVYekxN2Y)

## Future Consideration

My takeaways are threefold. First, music absolutely has a place in data science, and data science has a place in music, because we can use data science to analyze music in a profound way like I have just shown. Second, music is full of patterns, to the point where a computer can discern and not only show us those patterns, but also create new music based on the patterns. And lastly, for future work, music differentiation does not consist only of harmony. I hope to analyze melody, timbre, orchestration, and even lyrics, so we can use these findings to truly unlock the power of music.

___

## Author Information

- LinkedIn - [ZacharyMBrandt](https://www.linkedin.com/in/zacharymbrandt/)
- Website - [The Aspiring Music Psychologist](https://www.theaspiringmusicpsychologist.com)
- Podcast - [The Aspiring Music Psychologist](https://anchor.fm/zachary-brandt5)
