
# Datathon and Machine Learning Competition on Antisemitism

The Datathon and Machine Learning Competition will take place in **July 2025**. General information can be found here:  
https://isca.indiana.edu/publication-research/social-media-project/datathon-2025/index.html

Full challenge description: [2025 Task Instructions](https://github.com/AnnotationPortal/DatathonandHackathon.github.io/tree/main/Datathon_Challenge.pdf)

## #1 CHALLENGE: Building a Dataset with Bright Data (July 13 to July 20, 2025)

More information will be provided at the workshop on July 20.

Goal: Create a small but meaningful labeled dataset for hate speech detection.

Tasks:
1. Use the [Bright Data](https://brightdata.com/products/web-scraper/functions) interface to scrape at least 100 relevant user-generated posts.
2. Define your scraping focus (hashtags, user groups, topics) and document your rationale and potential biases.
3. Annotate your data using:
   - A definition of antisemitism and hate speech
   - A standardized annotation form (ours or adapted) [see paper](https://arxiv.org/abs/1910.01214)
   - The [Annotation Portal](https://annotate.osome.iu.edu/) or another tool (e.g., Label Studio, INCEpTION)
4. Prepare a [dataset](https://brightdata.com) and a dataset report including label definitions, distributions, and annotation rationale.

Participants are invited to use our Annotation Portal at https://datathon.annotationportal.com. The functionality of the portal will be explained at the first workshop. You do not need to register in advance. Once you register, please make sure to remember your password.

**IMPORTANT:** Please make sure you register to the portal with the same email address you used to register for this challenge. Please use "Datathon" for "Annotation Type" when registering. You can upload & annotate your scraped in the class "Datathon_Upload". You can see how you have annotated the dataset by using the "Export" button in the portal.



## #2 CHALLENGE: Modeling and Evaluation (July 20 to July 27, 2025)

Goal: Use our pre-annotated gold standard dataset to build and evaluate a hate speech detection system.

Participants can select from the following curated datasets:
- [Antisemitism on Twitter: A Dataset for Machine Learning and Text Analytics](https://zenodo.org/records/14448399)
- [Antisemitism on X: Trends in Counter-Speech and Israel-Related Discourse Before and After October 7](https://zenodo.org/records/15025646)
- [A German Language Labeled Dataset of Tweets](https://zenodo.org/records/10053509)

Each dataset consists of user-generated content annotated for antisemitic hate speech and conspiracy narratives. Annotations were created using an expert-reviewed schema and include agreement between multiple annotators.
The labeled datasets contain messages from the social media platform X/Twitter with the keywords "Jews, Israel, Kikes, or Zionazi*" classified as biased/non-biased (based on 100% agreement between two annotators).

Tasks:
1. Download the (Goldstandard/GroundTruth) datasets listed above.
2. Use tools such as scikit-learn, spaCy, or Hugging Face Transformers to train a model.
3. Evaluate your model:
   - Report precision, recall, F1-score, and display a confusion matrix.
   - List the hyperparameters used for training.
   - Conduct error analysis and provide qualitative examples, especially false positives.

Your code should be submitted in a format that runs on both Unix and Windows systems with clear readme instructions.



## Deliverables

You provide the deliverables in the form of software packages with instructions on how to run them (read-me files). The software must run on any system (Unix or Windows).

The evaluation committee carries out an independent assessment of the teams' performance.

**Deliverables for Challenge #1 include:** 
   - Adapting and implementing an existing definition of antisemitism
   - Reporting how the data was scraped and which guidelines were used to classify and annotate the data in a standardized way

**Deliverables for Challenge #2 include:**
   - Evaluation Report + Metrics (the performance measure for the classifiers will be F1 scores)

**You can earn bonus points:**
   - Gain +10 additional points for Challenge #1 by providing additional evaluation metrics, such as Cohen's Kappa or Krippendorff's Alpha, for Inter-Annotator Agreement (IAA).
   - Gain +10 additional points for Challenge #2 by using the fine-tuned model on unseen data.

You can share the files with us in any way you want. The easiest for you is probably uploading it to any cloud storage and sharing the link with us.

All deliverables, including annotations and evaluations, must be summarized and completed by **August 5, 2025**.


## Prizes

- 1st Place Team: $1,000 gift certificate  
- 2nd Place Team: $600 gift certificate  
- 3rd Place Team: $400 gift certificate  

\* Prizes are provided and managed by the World Jewish Congress.

### Participation Certificate

Selected participants will receive a certificate recognizing their achievement and skills.


## Links and Related Content

- [Tutorial and Material on Social Media Text pre-processing and classification](https://github.com/AnnotationPortal/DatathonandHackathon.github.io/blob/main/NLP_ML_Social_Media_Processing.md)
- [General NLP-Tools, Guides, and Tutorials for all levels](https://github.com/AnnotationPortal/DatathonandHackathon.github.io/blob/c8cc15cf6231e0e994162514d60e4737c34f0cc9/NLP-Tools%20and%20Guides.md)


## Previous material

The material from the 2020 Hackathon and Datathon on Antisemitism in Social Media can be found here:  
[https://github.com/dcavar/AntisemitismDatathon2020](https://github.com/dcavar/AntisemitismDatathon2020)

Information on the 2024 Datathon and Machine Learning Competition can be found here:  
[https://isca.indiana.edu/publication-research/social-media-project/datathon-2024/index.html]

[PPT from January 15, 2023, on psychological and historical reasons for racism and antisemitism](https://github.com/AnnotationPortal/DatathonandHackathon.github.io/blob/main/Psychological%20and%20Historical%20Reasons%20for%20Racism%20and%20Antisemitism.pptx)

[PPT by Damir Cavar, January 29, 2023, Corpus Standards and Evaluation](https://github.com/AnnotationPortal/DatathonandHackathon.github.io/blob/main/Corpus_Format_Selection.pdf) and [Video](https://iu.mediaspace.kaltura.com/media/t/1_5sfcj3ix)
