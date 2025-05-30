# Section 1: ai-related-dataset

The `ai-related-dataset` folder contains two datasets:

1. **ai-aspect_extraction-pre-processed.parquet**  
    A more compact version of the dataset where the aspect-sentiment pairs are not split.  
    **Columns:** `rev_id`, `app_name`, `review`, `features`, `ai_related`, `summaries_text`, `CATEGORIES`, `app_pkg`

2. **ai-summary-sentiment-merged-se3.parquet**  
    An unfolded version of the previous dataset with split aspect-sentiment pairs.  
    **Columns:** `keys`, `values`, `rev_id`, `app_name`, `review`, `features`, `ai_related`, `summaries_text`, `CATEGORIES`

3. **new-prompt.txt**  
    A file containing all the prompts used for evaluating different LLMs for AI-related classifications.


# Section 2: aspect-extraction folder

The `aspect-extraction` folder contains:

1. **prompt-extraction.txt**  
    This file includes both the system level and user level prompts used to instruct LLama 70b to extract AI-aspects-sentiment pairs.


# Section 3: Table 5 (Distribution Data)

This section generates Table 5 from the paper. It includes the following files:

1. **neg-asp.parquet**  
    Data used to compute the distribution of negative aspects.

2. **pos-asp.parquet**  
    Data used to compute the distribution of positive aspects.

3. **neg-rev.parquet**  
    Data used to compute the distribution of negative reviews (a review can appear in multiple topics).

4. **pos-rev.parquet**  
    Data used to compute the distribution of positive reviews (a review can appear in multiple topics).

5. **table5.py**  
    Computes the table 5 in the paper using the dataset in 1,2,3,4.


# Section 4: Figure 4

This section generates Figure 4 from the paper.

1. **co_occur_matrix.parquet**  
    Contains the positive and negative co-occurrences used to build a Sankey diagram that answers: "What are the negative topics being discussed in the same review when a positive topic is mentioned?"  
    
2. **sankey.py**  
    Utilizes the data from the parquet file to construct the Sankey diagram presented as Figure 4 in the paper.

3. **acm_invisible_sankey_top5_vector-6.pdf**  
    The PDF output displaying the final Sankey diagram as included in the paper.


# Section 5: Figure5-6 (Positive and Negative Heatmaps)

1. **heatmap-pos.parquet**  
    Dataframe containing the distribution of positive topics across app categories.

2. **heatmap-neg.parquet**  
    Dataframe containing the distribution of negative topics across app categories.

3. **heatmap.py**  
    Plots the heatmaps using the data from heatmap-pos.parquet and heatmap-neg.parquet to generate Figures 5 and 6.



# Section 6: kmeans

1. preprocess.py does pre-processing of the ai summary-sentiment pairs (ai-summary-sentiment-merged-se3.parquet) and computes the embeddings for the aspects. For each sentiment, corresponding aspects are saved and the embeddings for positive and negative aspects are generated separately.

2. final_neg_2.py and final_pos_2.py perform kmeans clustering for negative and positive sentiment-aspects respectively. They run the clustering for k values ranging from 2 to 20 and evaluate each cluster.

3. **pos-kmeans-out.parquet**  
    Contains the clustering output for positive aspects.  
    **Columns:** `sentence`, `cluster_label`, `cluster_name`

4. **neg-kmeans-out.parquet**  
    Contains the clustering output for negative aspects.  
    **Columns:** `sentence`, `cluster_label`, `cluster_name`
