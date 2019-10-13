<h2> Problem Statement </h2>
<h3> Generating Distractors for questions </h3>

MCQs are a widely question format that is used for general assessment on domain knowledge of candidates. Most of the MCQs are created as paragraphs-based questions.

A paragraph or code snippet forms the base of such questions. The questions are created based on three or four options from which one option is the correct answer. The othe remaining options are called the distractors which means that these options ar eneares to the correct answer but are not correct.

We are provided with training dataset of questions, answers, and distractors to build and train an **NLP** model. The **test** dataset contains questions and answers. We are required to use your NLP model to create up to **three** distractors for each question-answer combination provided in the Test data.

<h3> Data Description: </h3>

- Train.csv 31499 * 3 (excluding headers)
- Test.csv 13500 * 2 (excluding headers)

|Column|Description|
|------|-----------|
|Question|Question of MCQs|
|Answer|Correct answer of the corresponding question|
|Distractor|Options that closely related to the correct answer but are not the correct answer|

<h3> Submission format: </h3>

- Your task is to create upto **three** distractors for each question-answer combination provided in the **Result.csv** file.
- Each distractor must be placed between quotes (' ' or " ") and must be separeated by a comma(,).
- This format can be observed in the traning dataset.

<h3> Sample Data: </h2>

|question|answer_text|Distractors|
|--------|-----------|-----------|
|What is the color of Donald Duck's bowtie?|Red|'Blue','Yellow',"green'
|What is a Web browser?|A software program that allows you to access sites on the World Wide Web| 'A kind of spider','A computer that stores WWW files','A person who likes to look at websites'

<h2> Approach: </h2>

Developing distractors has one of the most challenging and time-consuming tasks for a question-setter.

<h4> Different ways for Generating distractor: </h4>

1. Can be generated from and after learning the context/concept from the passage(if provided) by training a Generative model. This can be achieved by generating texts from the passage that are close to answers but not exactly the same. But the grammar and POS of the generated text might be all messed up which is undesirable. 
2. If we have a collection of potential distractors or "candidate distractors" we can choose the most similar distractors to the Question-Answer pair. The idea is to produce semantically meaningful sentence embeddings for Question-Answer pairs and the Distractors.

Here, I have choosen the 2nd approach since we need grammatically correct distractors.
