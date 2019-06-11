# Stutter Manager : Software requirements specification

## Change history

| Date | Author | Descrition |
| -------- | -------- | -------- |
| May 30, 2019     | [Romain GUILLOT](mailto:rguillot42@gmail.com) | First version     |

## Table of contents
[toc]

## Introduction
### Purpose
The purpose of this document is to describe the software requirements of the mobile application *Stutter Manager*. It will describe what the purpose of the applications, features, constraints.  

The application is developped at UTP as an internship project, this document is intented for everyone who continue the development of the application.

### Scope

Stutter Manager is an mobile application develop for Android and ideally on iOS to help people who stutter to reduce their stuttering with exercise and guides about stuttering. A therapist will able to access to the exercise results and progression of its students.

### Definitions, acronyms, and abbreviations


| Term | Definition |
| -------- | -------- |
| Stutter   |      |
| Therapist     |      |
| Patient |
| External database     |      |
| |




### References
- [IEEE Recommended Practice for Software Requirements Specifications](http://www.cse.msu.edu/~chengb/RE-491/Papers/IEEE-SRS-practice.pdf)

### Overview


## General description

The application is destined to two actors :
- **Stutter user :** a person who want to do exercises to improve its flow of speech ;
- **Therapist :** a person able to give feedback to a stutter user (rate exercises, advices, give suggest exercises).

### Product perspective
*Stutter Manager* is a mobile application on Play Store and eventually on iOS. Users can create an account. An account have two purposes :
- Synchronise data on the cloud
- Use features that required to be logged (especially for the communication beween a therapist and their students)

If user is connected, data can be save on an external database, if the user is not connected, data will be save on the user device. To access data on the database, user have to be logged. Two authentification method will be available :
- standard authentification with an email and a password ;
- social authentification with an Google account.

###### Hardware
Basics hardware requirements can be required for some features :
- **Internet accesss**
- **Microphone** (e.g. : delayed auditory feedback)
- **Front-facing camera :** (e.g. : mirroring)

### Product functions
Here an use-case diagram to recap all features :
![](https://i.imgur.com/Vev8gic.png)


### Constraints
User data are stored on an external database, these data can only be visible by the user himself or by a therapist if the user **autorize** a therapist to access to his data. Data privacy policy has to be clear, user has to know which data is available to other, which data is **strictly** personnal.

No sensible informations will be stored by the application itself (*credit card informations, password of other services, etc.*).

The application is intended to be available on app marketplace (Play Store and App Store), the application can be available on different country. The application have to follow regulation and laws in the country chose to distribute the application (*data policy, etc.*).


## Specific requirements

The section explain and describe first the data synchronisation and then system use-cases (*see use-case diagram above*). 

### Data Synchronisation
Data synchronisation is only available with an account and with an internet access. Data are not automatically synchronise from/in the external database. The are two type of data store in the external database :
- **Personnal data** : exercices progression logs and personnal information (email / id / password / ...)
- **Shared data** : typically exercises data (texts / short sentences / words / ...)

Therefore, the user have to handle indendently the synchronisation of this two database, the one to upload personnal data on the external database, the other to update / download exercises data. 

### Use-case : Sign-Up


|                  | Description |
| --------         | -------- |
| **Function**     | Create an account for a user |
| **Requirements** | Internet connection |
| **Description**  | A non-logged user can create a new account to save data in the cloud and access to some features available with an account (see use-cases with *Stutter account* or *Therapist account* requirement).<br><br>Two methods of authentification is available : <br> - **Standard method** : a form with an email, password, passwords verification fields.<br> - **Social authentification** : User can create an account with a Google account, form with the email and password is handle by the Google authentification service, the application kept only informations available by API provide by Google authentification service<br><br>After this first form, the user is logged and have to indicate its status to continue : *Stutter user* or *Therapist user*<br><br>The account informations are save on an external database. |




### Use-case : Log-In

|                  | Description |
| --------         | -------- |
| **Function**     | Logged the user in the app |
| **Requirements** | Internet connection - Stutter account OR Therapist account |
| **Description**  | If the user have already an account (stutter or therapist) he can log to the app with two different methods, depending of its inital sign-up method :<br>- **Standard form** : email and password fields <br>- **Social buttons** : Google authentification button, and it's google that handle the form (Google e-mail / password)<br><br> After connection process if form is correct and if the user have an account, the user will be logged to the app will be redirected to the homepage |

### Use-case : View and modify account informations
|                  | Description |
| --------         | -------- |
| **Function**     | View profile information and modify them |
| **Requirements** | Internet connection - Stutter account OR Therapist account |
| **Description**  | A logged user can access to its account to handle its personnal informations : <br> - Change sign-up informations as email or passwords<br> - View its unique and personnal identification key <br> - Delete **definitely** its account (personnal informations + data) <br> - Reset its account data (progression, results, allowed therapist, patients, etc) <br> - **For therapist only :** Add comment status (see *Use-case : Give patient exercises feedbacks*)|

### Use-case : Handle stutter patients
|                  | Description |
| --------         | -------- |
| **Function**     | Add patient (sutter user) to follow to track its progression / give feedbacks / ... |
| **Requirements** | Internet connection - Therapist account |
| **Description**  | A therapist is able to add stutters to follow to : <br> - Track their progressions <br> - Give results, feeback of exercises done by the stutters <br> - Give exercise to stutters<br><br> To add a patient the therapist has to have the stutter user key (a unique key associated to the account). This key is available in the app, in the account informations. The stutter informations is not directly available for the therapist, the stutter have to accept the therapist request, to summarize there are 4 states after the request : <br> - **Request pending** : the request has be sent but the stutters user do not yet approved ; <br> - **Request approved** : stutters accept the request, the therapist **can** access to the stutters informations ; <br> - **Request refused** : the sutters reject the request, the therapist **cannot** access to the stutters informations ;<br> - **Request revoque** : the stutter user revoque the access, this state is possible only if the stutter user **aproved** the request before.<br><br> The therapist can see at any time the list of his patients and delete them of his list of patients.    |

### Use-case : Handle allowed therapists
|                  | Description |
| --------         | -------- |
| **Function**     | Add a therapist allowed to access to the progression associated with the account |
| **Requirements** | Internet connection - Stutter account |
| **Output**       | Add a therapist to the list of allowed therapist account |
| **Description**  | Once a therapist made a request to add a stutters account to his patients, the stutter user receive this request and he can **accept** or **refuse** the request. If the stutter user accepts, the therapist will have an access to the stutter user progressions / results, and the therapist will be able to give some feedbacks about exercises and suggest exercises to do.<br><br> At any time, the stutter user can see the allowed theraists list and remove an allowed therapist of its account (=revoque the access of its informations to a therapist). |

### Use-case : View exercices results / progression / feedbacks
|                  | Description |
| --------         | -------- |
| **Function**     | Visualize stutter user exercises progression charts and feedback give by a therapist about these progression charts  |
| **Requirements** | *None* (internet connection and account unblock features) |
| **Description**  | Stutter user can visualize charts about his progression over day, week, month and year.<br> They can see the history of their exercises and access to the exercise logs (recording, responses, data, etc.). Each exercises defined its format of the chart and of the logs, see *Use-case : Do exercices* to have more informations about these informations.<br><br>A therapist can also visualize these informations for their patients.|

### Use-case : Communicate with patient
Therapist can interacts with his patients with 3 ways :
- **Comments** : general comments, just some texts (it can be advice for example)
- **Exercise suggestion** : therapist can suggest exercise to the patient (with custom settings and resources)
- **Exercise feeback** : comments, feedbacks about exercises done by patients

###### Comments


###### Exercise suggestion

###### Exercise feedback
|                  | Description |
| --------         | -------- |
| **Function**     | Provide feedbacks / advices / comments about exercises  |
| **Requirements** | Internet connection - Therapist account |
| **Description**  |  For each patient, the therapist can visualize the log and add a feedback to help the stutters user. A feedback is composed of 3 fields : <br> - **Status**: pre-filled comment (eg: "*:thumbsup: Perfect !*" ) ; <br> - **Comment**: text field to enter some advices, comments, whatever ; <br> - **Date (automatic field)** : current date when the feedback is submitted. <br><br> At least one of *status* or *comment* have to be filled.<br> A therapist can save its own status on its profile.<br> At any time, the therapist can delete or modify his comments.|


### Use-case : Do exercises

An exercise is independant : it has structure and data that does not depend of other exercises. Data can contain exercises content and user informations (e.g. results of previous exercises). Exercises can  also share data with other exercises, so an exercise can managed its data as it want :
- **private storage** : only accessible (read and write) by the exercise itself
- **share storage** : public storage accessible by all exercises (to write, read, delete data)

A complte exercise structure is composed of two parts :
- **Exercise structure** : which data is usefull to use, where to store data (private storage / share storage), how to dislay the exercise, how to answer, etc.
- **Progression structure** : which data has to be used to display progression, type of chart, etc.

Each exercise have to be complete with this following informations :
- How to do the exercise
- What is the purpose, how it can help the stuttering ?

![](https://i.imgur.com/huRsUas.png)

#### Resources for exercises



| Type | Description | 
| -------- | -------- | 
| Medium/long text     | Long texts of several sentences, user can chose the text he want to do the exercices and he can also add texts to its favorite texts. To chose a text, the user can order them by the number of words and select only among his favorite texts. |
| Short sentences | Collection a sentences, few words. Short sentences are picked automatically  |
| words | Only one word, words are picked automatically

See *appendix A* to know more about the storage policy.

Exercise can :
- **Chose a resource** for the exercice
- **Let user chose** among chosen resources (all, only among 2 type, ...). In this case, user have to chose the resource he want at the beginning of the exercises.

###### Ways to percept resources
- **Permanent text** : the resource is displayed without any restrictions
- **Covered text** : the resource is dislayed during few amount of time (eg: 2sec $\times$ number of words), and then the resources is covered. The user can still press the covered area to display them.
- **Vocal text *(only for words and short sentences)*** : The resource is read by a computer generated voice, the user can replay the voice.

Exercise can :
- **Chose itself** how user have to percept resources
- **Let user decide** how he want to percept resources

###### Tap to add to stutter words list feature
The user can select words from resources that he cannot say correctly (each exercices can :
- **require** this feature, 
- **disable** this feature 
- **let the user descide** if he wants this feature at the begining of the exercise

Following a description how the feature have to be implementing depending of resources :
- **medium/long exercise** : at the end of the exercise the user can select words if the feature is enable
- **short sentences** : between each sentences displayed the user can select words if the feature is enable
- **words** : to display an other word the user have to say if he correctyl ponounce the words or not (if the feature is enable)

###### Exercise progression
A progression is composed of :
- **Video or audio recording** : video or audio record of the exercise (if available) with a progress bar to go wherever the user wants 
- ***(Annotated)* resource** : resource used for the exercise, if user chose to check his pronunciation, words can be marked.
- **Exercise settings** : settings used for the exercise

A chart for each exericise is available. There is a maximum of 3 charts (one for each resources) : the chart data is the ratio of *correct words / total words*.

#### Exercices


Following are the specification for each exercises 

###### Exercise 1 : Metronome
|                  | Description |
| --------         | -------- |
| **Function**     | Exercise to recording his voice with a metronome |
| **Requirements** | Microphone |
| **Description**  | The user have to read a **medium/long text** or a succession of **short sentences** with a tempo defined by a metronome.<br><br>**Metronome**<br>the stutter user can change the value of the metronome interval (beats per minute). Once the exercises is launched, each metronome pulse is perceptible thanks to : <br>- *A sound* : A sound is emitted for each pulse (it can be disable) ; <br>- *A visual information* : A visual information is displayed for each pulse |
| **tap to add to stutter words list** | Let user decide at the begining.|
| **Ways to percept resources** | Let user decide at the begining |
| **Storage used** | - **Medium/long texts** <br>- **Short sentences** <br> - **Favorite texts** <br>- **Sutter words** <br> - **Exercise logs** : private exercise storage |

###### Exercise 2 : Delayed auditory feedback
|                  | Description |
| --------         | -------- |
| **Function**     | Delayed auditory feedback exercise |
| **Requirements** | Microphone |
| **Description**  | *(Wikipédia) Delayed Auditory Feedback (DAF) is a type of altered auditory feedback that consists of extending the time between speech and auditory perception*<br><br>The stutter user have to read a **medium/long text** or a succession of **short sentences**, and he listen its voice with a delay (<1s).<br><br>**Voice perception delay**<br>User can chose the delay time and adjust the intensity of the sound (he can speak to test the settings) |
| **tap to add to stutter words list** | Let user decide at the begining |
| **Ways to percept resources** | Let user decide at the begining |
| **Storage used** |  - **Medium/long texts** <br>- **Short sentences** <br> - **Favorite texts** <br>- **Sutter words**  <br> - **Exercise logs** : private exercise storage  |

###### Exercise 3 : Reading
|                  | Description |
| --------         | -------- |
| **Function**     | Reading texts or words and track diffult words |
| **Requirements** | *None* |
| **Description**  | Users has to read succession of **words**, succession of **short sentences** or a **medium/long text**. There are 3 ways to percept this resources.<br>The user can chose to record the exercise or not. The user can stop the exercise when he wants.|
| **tap to add to stutter words list** | Required |
| **Ways to percept resources** | Let user decide at the begining |
| **Storage used** |  - **Medium/long texts** <br>- **Short sentences** <br> - **words collection** <br> - **Favorite texts** <br>- **Sutter words**  <br> - **Exercise logs** : private exercise storage  |

###### Exercise 4 : Mirroring
|                  | Description |
| --------         | -------- |
| **Function**     | Speech with video recording to analyse his physical behaviour during the speech |
| **Requirements** | Front facial camera - Microphone |
| **Description**  | Users has to read **succession of words**, **succession of short sentences** or a **medium/long text** and his face is recorded to analyse his muscles, his behaviour during the stuttering, ... When he launch the exercise the front facial video recording is also started. He can chose to dislay or not the video feedback. |
| **tap to add to stutter words list** | Let user decide at the begining |
| **Ways to percept resources** | Let user decide at the begining |
| **Storage used** |  - **Medium/long texts** <br>- **Short sentences** <br> - **Favorite texts** <br>- **Sutter words**  <br> - **Exercise logs** : private exercise storage |

###### Exercise 5 : Stutter rate
|                  | Description |
| --------         | -------- |
| **Function**     |  |
| **Requirements** |  |
| **Description**  |  |
| **tap to add to stutter words list** | *No resource used* |
| **Ways to percept resources** | *No resource used* |
| **Storage** |  |




### Use-case : Suggest exercises to a patient
|                  | Description |
| --------         | -------- |
| **Function**     |  |
| **Requirements** | Internet connection - Therapist account |
| **Description**  |  |


### Use-case : Access therapist suggested exercises 
|                  | Description |
| --------         | -------- |
| **Function**     |  |
| **Requirements** | Internet connection - Stutter account |
| **Output**       |  |
| **Description**  |  |

## Conclusion

This document defined the purpose of *Stutter Manager* application and how it should be. Every application modification or improvments has to be add  in this document to keep a cohesion between the technical part (the application itself) and the specification parts (this document). The modification logs (short summary of perfomed modifications) are available at the beginning of the document.

## Apendix

### A : Shared storage database

| id | description | user data |
| -------- | ------ |----- | 
| 1 | Collection of texts | no |
| 2 | Words collection | no |
| 3 | Sentences collection | no |
| 4 | Favorite texts | yes |
| 5 | Sutters words | yes |