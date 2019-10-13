<h2> Problem Statement </h2>
<h3> Generating Distractors for questions </h3>

MCQs are a widely question format that is used for general assessment on domain knowledge of candidates. Most of the MCQs are created as paragraphs-based questions.

A paragraph or code snippet forms the base of such questions. The questions are created based on three or four options from which one option is the correct answer. The other remaining options are called the distractors which means that these options are nearest to the correct answer but are not correct.

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
2. Text can be generated just by considering the left context of right-most word. This can be achieved by training a GPT2 model. But if we don't have long sequences of texts it is difficult to train a model that generates grammatically correct sentences.
3. If we have a collection of potential distractors or "candidate distractors" we can choose the most similar distractors to the Question-Answer pair. The idea is to produce semantically meaningful sentence embeddings for Question-Answer pairs and the Distractors.

Here, I have choosen the 3rd approach since we need grammatically correct distractors. But if the passages were provided it is possible to generate distractors that are close to the context of the passage without compromising too much on their gramatical correctness. This can be achieved by leveraging from pre-trainded wide bidirectional encoder-decoder neural network architectures such as BERT.

<h3> Different ways of producing sentence embeddings: </h3>

1. **Avg-W2V:** Words can be converted to vectors by producing their W2V embeddings. For sentences we can take average of the all the word embeddings to produce the sentence embedding. Since this is based of indivdual word embeddings this does not consider the context, POS of the words, Voice of the sentences.
2. **Avg-W2V (Glove):** Leverages a pretrained Glove model to produce sentence embeddings. This is said to also consider the context of the words.
3. **Sentence Transformers:** Sentence Embeddings using BERT. Tunes a model on Natural Language Inference (NLI) data. Given two sentences, the model should classify if these two sentence entail, contradict, or are neutral to each other. For this, the two sentences are passed to a transformer model to generate fixed-sized sentence embeddings. These sentence embeddings are then passed to a softmax classifier to derive the final label (entail, contradict, neutral). This generates sentence embeddings that are useful for tasks like clustering or semantic textual similarity.

<h4> Constructing sentence embeddings: </h4>

Choosing 'bert-base-nli-mean-tokens' and 'bert-base-nli-stsb-mean-tokens' pretrained sentence embeddings model for constructing sentence embedings/vectors.

Finally, calculating the cosine distance of all the distractors from every Question-Answer pair.
And found the closest 3 distractors from the corpus of distractors for each query sentence based on cosine similarity.
