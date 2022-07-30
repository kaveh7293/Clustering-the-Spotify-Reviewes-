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
<p>The following figure shows the process of converting each sequence to the vector of numbers. As shown, we convert each word in the sequence to a vector of numbers using the matrix of word embedding (I used an embedding layer from keras to do so). The numerical values of the embedding matrix was obtained from <a href='https://nlp.stanford.edu/projects/glove/'> here <a>. Since there are 61594 reviewes the corresponding matrix of the numerical data have a shape of 61594 by 100. <br>

  <img src='https://github.com/kaveh7293/Clustering-the-Spotify-Reviewes-/blob/main/Screenshot%202022-07-29%20184955.jpg'></p>
 <h3> Dimension Reduction </h3>
  <p> I used principal component analysis to obtain the optimal number of principal components using which a majority of the variations in the data can be explained. Based on the following figure, using 5 PCAs 85 % of the variations in the data can be explained.</p>
  <img src='https://github.com/kaveh7293/Clustering-the-Spotify-Reviewes-/blob/main/explained_variance.png' width='600' height='400'><br>
  Note that based on the figure, 80 % of the variations in the data can be explained by the first two pricipal components. So the plot of the projected data onto the second proncipal component vs. the first principal component could be informative especially when they are plotted along the principal components in a biplot:<br>
  <img src='https://github.com/kaveh7293/Clustering-the-Spotify-Reviewes-/blob/main/download.png'><br>
  As shown, the data along the positive side of the first pricipal component vector seem to be different from the rest of the data (i.e., they seems to be outliers). we can investigate these data by first finding the reviews corresponding to these values. Because the outliers are along the positive side of the PC1. I plotted the distribution of the sentences lengths for all of the reviewes and the distribution of the outlier reviews. As shown in the following, the outliers are those that have very large sizes.<br><br>
  <img src='https://github.com/kaveh7293/Clustering-the-Spotify-Reviewes-/blob/main/download%20(2).png'><br><br>
 The following plot shows the distribution of the reviewes length which has the smallest values along the PC1:<br><br>
 <img src='https://github.com/kaveh7293/Clustering-the-Spotify-Reviewes-/blob/main/download%20(3).png'><br>
  
As shown, the lengths of the reviews are very small for the reviewes whose projected data onto the PC1 is very small. In the next section, I do a cluster analysis and I guess that the length of the reviews is an important parameter which distinguish different reviews data.
 </p>
 <h3> Cluster Analysis</h3>
 
