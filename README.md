# Introduction
In order to develop effective crowdsourcing aggregation methods for multiple choice question answering(MCQA) and evaluate them empirically, we developed and deployed a crowdsourced system for playing the “Who wants to be a millionaire?” quiz show. This repository includes our dataset in csv and sql formats. Note that, as question and answer texts are originally in Turkish you should use UTF8 format at all times to avoid encoding problems.

# Citation
Please cite this publication http://onlinelibrary.wiley.com/doi/10.1002/cpe.4168/full

Sample citation formats:
- Harvard
Aydin BI, Yilmaz YS, Demirbas M. A crowdsourced “Who wants to be a millionaire?” player. Concurrency Computat.: Pract. Exper. 2017;e4168. https://doi.org/10.1002/cpe.4168

- BibTex entry
@article {CPE:CPE4168,
  author = {Aydin, Bahadir Ismail and Yilmaz, Yavuz Selim and Demirbas, Murat},
  title = {A crowdsourced “Who wants to be a millionaire?” player},
  journal = {Concurrency and Computation: Practice and Experience},
  issn = {1532-0634},
  url = {http://dx.doi.org/10.1002/cpe.4168},
  doi = {10.1002/cpe.4168},
  pages = {e4168--n/a},
  keywords = {crowdsourcing, multiple-choicem, question answering},
  note = {e4168 cpe.4168},
}

# Data
Over the period of 9 months, we collected over 3 GB of data using our CrowdMillionaire app. In our dataset, there are 1908 questions and 214,658 unique answers to those
questions from CrowdMillionaire participants. In addition,
we have more than 5 million offline answers for archived live
questions.
Our dataset includes detailed information on the game
play. For example, our exhaustive timestamps show (1) how
much time it took for a question to arrive to a participant,
(2) when the question is actually presented to the participant
on her device, and (3) when exactly the participant answered
the question. We
shared this dataset in order
to advance the understanding of the MCQA dynamics, after we cleaned and anonymized the data.

## Data Format
Our data set includes 9 tables. Only 1 table is related to both online and offline data. 

### User:
- user_id: ID for a user in our dataset. All other information from this is cleaned in order to fully anonymize our dataset.

Following 3 tables are holding information about questions shown on TV live and their corresponding answers.

### Program: 
- program_id: ID for a program in our dataset.	Program is abstraction for an episode of show as it aired on TV. 
- start_time: Server timestamp of program's start time.
- end_time: Server timestamp of program's ending time.	
- num_of_contests: Total number of different players appeared on TV during that episode.
- num_of_questions: Total number of different questions appeared on TV during that episode.

### Question: 
- question_id: ID for a question in our dataset. Used as a foreign key in other tables.
- no: Level of the question in gameshow- 1 to 12-. Often is an indicator of the question difficulty.	
- question: Text of the question in Turkish.
- time: Server timestamp of the question. 
- choiceA: Text of first choice in Turkish.
- choiceB: Text of second choice in Turkish.	
- choiceC: Text of third choice in Turkish.
- choiceD: Text of fourth choice in Turkish.
- correct_choice: Letter for the correct choice.	
- program_id: The foreign key from the Program table that identifies the program the question has appeared in.

### Answer:
- answer_id: ID for an answer in our dataset.
- user_id: The foreign key from the User table.
- question_id: The foreign key from the Question table.
- choice: The choice of the user who is identified by user_id for the question which is identified by question_id.
- confidence: The sureness level of the user while answering. Don't mix it with statistical confidence. Note that, the confidence labels "certain", "guessing" and "no idea" are mapped to 1, 2 and 3 respectively. 
- time: Server timestamp of the answer arrival. Recommended to ignore.
- receivedTime: Timestamp recorded on Android device at the time user sees the question. 
- answerTime: Timestamp recorded on Andorid device at the time user answers. 

Following 5 tables are holding information about offline questions that users can answer for practice using our Android app at anytime, their answers and contextual category information.

### Practice Question: 
Same format as Question table. Some live questions are also used as practice questions. But note that neither all live questions are used as practice questions nor all practice questions appeared in live show. For the ones coexist in both tables, 10000 + (question_id in Question table) corresponds to the question_id of same question in Practice Question table. 

### Practice Answer:
Same format as Answer table.

### Question Category:
- question_category_id: ID for a question category in our dataset.
- category: Title of a question category in Turkish.
- category_en: Title of a question category in English.

### Question Subcategory:
- question_subcategory_id: ID for a question subcategory in our dataset.
- subcategory: Title of a question subcategory in Turkish.
- subcategory_en: Title of a question subcategory in English.
- question_category_id: The foreign key from the Question Category table that identifies the contextual category that encapsulates this subcategory.

### Question Subcategory Pair:
- question_subcategory_pair_id:  ID for a (question,subcategory) pair in our dataset.
- question_id: The foreign key from the Question table.
- question_subcategory_id: The foreign key from the Question Subcategory table.

## SQL files
There are 4 different SQL files. 
- millonaire.sql: Includes all the tables described above.
- millonaire_live.sql: Includes User, Program, Question and Answer tables.
- millonaire_offline.sql: Includes User, Question, Answer, Question Category, Question Subcategory and Question Subcategory Pair tables.
- millionaire_extended.sql: Includes all the tables in millonaire.sql and also some preprocessing data such as performance of users. As these preprocessing inforation depends on the period of programs, it is highly recommended for you to recalculate it.

A sample import statement should work as
- In a DOS based system: 
mysql.exe --protocol=tcp --host=127.0.0.1 --user=user --port=3306 --default-character-set=utf8 --comments < "C:\\SQLDump\\millionaire.sql"
- In Linux based system: 
mysql --protocol=tcp --host=127.0.0.1 --user=user --port=3306 --default-character-set=utf8 --comments < "/tmp/SQLDump/millionaire.sql"

