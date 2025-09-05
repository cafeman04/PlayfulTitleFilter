# PlayfulTitleFilter
Goal: Extracts playful and unique paper titles from a large dataset of papers

Dataset of 91,919 papers: https://drive.google.com/file/d/1EplQ4rVVPl3VFuV1x_OEfFN4aQwCTcJI/view?usp=sharing

**First Approach**

Initially, I believed filtering out certain keywords would be difficult as there can be a large assortment of writing styles of paper titles and clever ways to write them. That is why I first went down the route of finding a model to create semantic clusters to try to find a cluster that has playful titles. I loaded all of the paper titles into the SentenceTransformer model to create embeddings. As the HDBSCAN clusterer was taking too long, I decided to reduce the embedding dimensions using PCA. Creating these semantic clusters at first seemed like a wise idea because I thought a cluster of silly/funny titles would appear in one of them, however this was not the case. I realized I may have to change gears and give the filtering a more clear direction towards the titles I specifically want instead of hoping playful titles get clustered. 

I also tried to look at the highest outliers in the embeddings hoping they would give me titles I was looking for, but this was also not the case. I realized the outliers simply mean they were very different from other titles and didn’t share any similarity, which does not imply they would turn out silly. The outliers may be unique,but it allowed the titles to contain lots of technical jargon, which is the opposite of what I wanted.

**Second Approach**

My second approach was using cosine similarity with seeds. I picked ideal titles from a random selection of the large set, looking for silly, unique, and interesting titles. At first, I kept the entire title for these selected seed titles, but many titles that were found “similar” to the seeds only contained technical words and nothing eye-catching. Then, I chose to eliminate the technical portions from the seeds and only keep the interesting and silly portions, which helped nudge the filtered titles toward my desired output. I also added some personally hand-written seeds that I would see as eye-catching in a paper title.  

I computed embeddings for these seeds and then calculated cosine similarity with all titles, filtering for a similarity threshold above 0.6. This gave a set of titles that better aligned with the “silly/funny” aspect I wanted, but there were still some gaps present as I saw some titles that didn’t contain any playful elements.  

**Reflection**

In conclusion, there can still be more improvements made with more time spent optimizing the filtering. With more time, I would look into creating a dataset of bad titles that contain only technical jargon and have the similarity checking aim to get closer to silly embeddings while distancing from technical-only titles. I also think an approach that doesn’t solely focus on semantics of seed titles but incorporates the interesting and silly writing style would provide much better results. Diving deeper into this approach would be quite interesting.

