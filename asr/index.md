---
title: "ASR for sociolinguists"
date: "2024-04-24"
author:
  name: "Joe Pearce"
  url: "https://praat-enthusiast.github.io/asr/index.md"
format:
  html: default
license: "CC-BY-SA 4.0"
citation: true
---

# Terminology
Come back to this part of the tutorial if you see terminology that doesn't make sense to you. 
Please note, I am not an expert in any of this, but a mere sociolinguist/phonetician who has learnt about ASR in order to use it. These explanations come from my own understanding, so feel free to correct me if you disagree with my explanations.


| Term     | Explanation |
| :------- | :------- |
|**ASR**| Automatic Speech Recognition. Refers to using automatic methods to transcribe speech with minimal human input. Confusingly, ASR can sometimes also stand for automatic *speaker* recognition, but I won't be using it to mean that here.|
|**STT**| Speech-to-Text - Another way of saying ASR. |
|**GPU** | Graphics Processing Unit - Part of a computer or graphics card that allows you to separate a task like ASR into parallel tasks which can be run at the same time, speeding up the process. Better known for allowing you play video games. |
|**Model**| The statistics and probability that enables ASR to function. |  
|**VRAM**| Virtual Random Access Memory: A resource often required to run large ASR models, which can be increased by using a GPU. |
|**AI**| Artificial Intelligence - An application with the ability to learn information in order to complete a task. |
|**Training data**| For ASR, paired speech and transcripts that are fed to the model, allowing it to learn the relationship between text and audio. Training data is often subtitle data scraped from the internet. |
|**Prompt**| An instruction you give to an AI model, that can help shape the output it gives you.|
|**VAD**| Voice Activity Detection - Separation of human speech from silence, background noise, music, and so on. Often the first step in ASR. |
|**High-performance computer cluster**| A set of computers with a lot of processing power that your institution may have access to, allowing you to run ASR on GPU without transferring the data elsewhere.|
|**API**| Application Programming Interface - Part of a program stored on someone else's computer that allows data and services to be sent between your computer and theirs. APIs are used in ASR as the backend of more user-friendly ASR applications, which don't require you to download the ASR model, but instead let you send your data to a cloud-based implementation of it, request for it to be transcribed, and receive a transcribed file in return.|
|**GUI**| Graphical User Interface - An application where you click buttons to make things happen, rather than writing code. |
|**Diarization**| In a multi-speaker audio sample, the answer to who is speaking when.|
|**Command line**| A text-based interface for interacting with the files on your computer. You might for example, use it to tell your ASR to run on a particular folder. Introduction to it [here](https://tutorial.djangogirls.org/en/intro_to_command_line/). |

# What tools are out there?

There's a lot of options to choose from when it comes to ASR, and which one is best for you for will depend on a couple of factors:

*How much time you're willing to invest in learning how to run it 
*What kind of data you have (i.e. number of speakers, channels)
*Whether you have access to a high-performance computer cluster or GPU through your university
*If you, your participants and your institution's ethics board and data protection team are willing to transfer your data to someone else's servers during processing
*How much you care about how 'clean' your transcript is
*Whether you need accurate time-stamps and speaker diarization

For the purposes of this guide, I'm going to into more detail on OpenAI's Whisper, because this is what I know the most about, and because it's open source and free to install. It has numerous offshoots, some of which make it easier to process your data for use in sociolinguistic research. I'll briefly talk about some other options below.


## OpenAI Whisper and its children
You've probably heard of [OpenAI](https://openai.com/) as the company behind ChatGPT, DALL-E, and Sora. [Whisper](https://github.com/openai/whisper) is their set of speech recognition models, that allow transcription of audio data in a number of languages. A fun feature of Whisper is that it allows you to specify the language, guess what language it's hearing, or translate what it's hearing into English. You can learn more from the paper they put out about it [here](https://cdn.openai.com/papers/whisper.pdf).

Whisper has a number of models available, for various languages, and of varying sizes. As a rule of thumb, if you want more 'accurate' speech recognition, you have to use 'bigger models', which require more processing power. Smaller models, on the other hand, run quicker, and require less processing power, but come at a tradeoff for accuracy. Larger models use more parameters to describe the data, a concept that I admit I can't really get my head around. 

As the name suggests, OpenAI's models are open: Available for anyone to download and run on their own computer, and use the code to develop other apps. Because of this, you can find a lot of ASR systems which use Whisper as their starting point. Some of these have been collated [here](https://github.com/sindresorhus/awesome-whisper), and some which you might be interested in are:
*[faster-whisper](https://github.com/SYSTRAN/faster-whisper). Like Whisper, but faster.
*[whisper-timestamped](https://github.com/linto-ai/whisper-timestamped). Like Whisper, but with better timestamps.
*[WhisperX](https://github.com/m-bain/whisperX), which improves processing speed, alignment between audio and transcript, and implements speaker diarization (using [faster-whisper](https://github.com/SYSTRAN/faster-whisper), [wav2vec](https://arxiv.org/abs/2006.11477), and [pyannote](https://github.com/pyannote/pyannote-audio). My preferred option for most ASR in sociolinguistics and phonetics.

There are two main ways to run Whisper (or any of its children):
*Locally, by downloading the model onto your own computer and running it via the command line.
  +You can either do this on a CPU (=your computer's normal processor), which will be slower, or a GPU, which will speed things up.
  +Buying your own GPU is expensive, but you might have access to one already via your institution's high-perfomance computer cluster, or because you are a gamer. 
*Using an API, where you send the data to someone else's servers that are running Whisper, and get them to do it for you.

**Why would I run it locally?**
*Cost. Many APIs will charge you when you go over a certain about of data (usually, about five hours of audio), and so by running it locally you're hypothetically saving money. In practice, the cost of running it locally isn't actually free, as you or your institution might need to pay for GPU access, or power to run the GPU, but you're less likely to have to spend your personal funds or grant funds to run it locally.  
*Data privacy and security. By downloading Whisper's models onto your own computer, you spend less time worrying about where it's going and who is doing what with it. 
*Customizability. You have the choice between the original Whisper or any of its children mentioned above, and full control over the settings you use. 
*Time. You don't need to wait for files to upload and download, and with a little effort you can set it to run on a whole folder rather than a single file.

**Why would I use an API?**
*Resources/cost. If you don't have access to a GPU, but you still want to use the larger Whisper models, you can usually use an API for free up until a certain point. 
*User-friendliness. If you aren't interested in learning how to install Whisper and its dependencies, which can be intimidating if you haven't done anything like this before, and might take a while. 
*Not having admin privileges on your device. Some institutions will make it very hard to install anything on managed machines. You usually can install something like Whisper, if you're a staff member or research student, and your university has a good IT team, but you might take some convincing. If you're an undergraduate student or taught postgrad student using a university machine, you'll probably need a staff member to make the request for you.  



##Other options
Some additional tools I've seen mentioned, but which I haven't tested extensively myself:
*[vosk](https://github.com/alphacep/vosk-api) speech recognition toolkit, which you can download and run locally offline
  +[vosk](https://github.com/alphacep/vosk-api) is the backend for [audapolis](https://github.com/bugbakery/audapolis), a GUI which allows you to use download and run vosk ASR models, and then correct the output.
  +vosk has smaller models than many options, so it's often used for developing apps which need something lightweight to run locally - this means it's a good option if you don't have access to a GPU, but also have data privacy concerns about using a cloud-based option. 
*[OpenBrainAI](https://openbrainai.com/downloads/). I don't know anything about this one, but it was recommended to me recently.
*[Speechmatics](https://www.speechmatics.com/). Supposedly very good, but paid-for, API service. 
*[Microsoft Azure Speech-to-Text](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-to-text). A paid-for API service available from Microsoft. 
  +This service is popular in sociolinguistics, and I hear it's very good - But note that this in also an API service and does **not** run locally. [More information is available here](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/batch-transcription-audio-data?tabs=portal): your data needs to be temporarily stored on either in Azure Blob storage or on a publicly accessible URL in order to be transcribed. 
  *Microsoft Azure's service is the backend for [CLOx](https://clox.ling.washington.edu/#/), another popular option for linguists.
*[Deepgram](https://deepgram.com/). Again, a paid service which requires transferring your data to their servers. Privacy notice available [here](https://deepgram.com/privacy/).
  *Deepgram is the backend for DARLA's [bedword](http://darla.dartmouth.edu/bedword) service, which is a great option if you want to integrate it with automated vowel extraction. 

Paid options mentioned above are worth looking into if you're working with small amounts of data, as many offer a small amount of transcription for free (often up to about 5 hours a month). Some people may even have access to Microsoft Azure via their institutional login. And many of the paid options are more intuitive to learn and use than free options. It's also possible some of those options may perform better than free options, though I haven't looked into it. Diarization is one area where I suspect paid models might be useful, 

## When NOT to use ASR

ASR is not a solution to all of the world's transcription problems. There are a few cases where I would advise against using ASR, specifically:

*You're working with data that includes speakers with non-standard accents, and a test run indicates that the ASR struggles with the accent in question
  +As an example, this is the case on our project My Voice, My Glasgow (with Sadie Ryan and Emma Moore), where we are working with young people in Glasgow, many of whom have Glaswegian accents, use Scots, and have a different home language that influences their accent when speaking Scots/English. I was actually impressed with how well ASR coped with some of this, but it was still nowhere near good enough to be time-saving rather than time-wasting, compared to transcribing manually.
*You have a specific set of transcription guidelines that you'd like to follow, and implementing these after ASR is conducted won't save time compared to transcribing from scratch.
*You're doing in-depth qualitative research where transcription is seen as part of the process of familiarizing yourself with the data (e.g. Interpretative Phenomenological analysis).
*You don't have access to the resources you need (e.g. a GPU) and have concerns about using a cloud-based service. 


## WhisperX tutorial 
*Coming soon...*
