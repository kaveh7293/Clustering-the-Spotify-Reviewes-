# Clustering-the-Spotify-Reviewes-
<h3> Problem Specification </h3>
<p> In this case study, I do a clustering to categorize the comments that are left by spotify uses. I want to check if there is any unexpected pattern wihtin the data. To do so, the following steps are followed:
<ol>
  <li>Preprocessing of the data were implemented wherein:
    <ul><li>All the uppercase letters were converted into  lowercase letters</li>
      <li>The short forms are converted into the formal forms (e.g., i'm to i am)</li> 
      <li>Special characters such as @ and # are removed from the text</li> 
      <li>Stop words are removed</li>
      <li>Lemmatisation is done to use the root of the words (e.g., convert provided to provide). Note that lemmatisation is more powerful than stemming where the resulting outcome are usually meaningless (e.g., convert provided to provid).</li>
    </ul>
   <li> A tockenizer is used to convert the texts into the numbers and assign a unique number to each distinct word. Padding is done in the next step in order to convert the sequences with different lengths into the same size by putting additional zeros at the start of the sequence with shorter lengths than the maximum sequnce length.</li>
  <li> An embedding matrix is constructed based on the tocknized values of the words and using already trained embedding matrix downloaded from <a href='https://nlp.stanford.edu/projects/glove/'> here. </a> To do so, the row number in the embedding matrix corresponds to the index of the word based on their tockenized values.</li>
  <li> The embedded matrix is used in the embeddding layer and set trainable option to false so that no embedding is implemented.</li>
  <li> Each review has 30 elements (because we set the maximum length of the sequences to 30) and the output length corresponding to each word is 100 (i.e., dimentionality of the embedde matrix) resulting in a matrix of 100 by 100 for each review.</li>
  <li> In the next step, the average values of all the rows for the coded values of each sentence is obtained and saved as the corresponding vector for each review.</li>
  <li> Now, we have a row of number containing 100 columns for each of the reviews. </li>
  <li> We do a Principal Component Analysis (PCA) to reduce the number of dimensions.</li>
  <li> We do a hierarchical clustering to categorize the data.</li>
</p>
<h3>Model Architecture</h3>
<p>The following figure shows the architecture that I have used for clustering.<br>

  
  
 </p>
