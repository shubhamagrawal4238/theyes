# theYes
Code can be found and run at 
https://colab.research.google.com/drive/1hlRWGCjun7ffqXXRn7Fp1UUTohFWzOlb?usp=sharing

Readme includes problem statement and answers

Product Category Classification Challenge

Input
You are given
- a catalog of 1000 fashion products in product_data.json.
- Each product has a description and a product image url.
- All the product data were crawled from the internet.
- a list of product categories are given in product_categories.txt.

Goal
Classify the fashion products by category. Add a “category” field to each product in the
product_data.json file as output.
You can use the language of you choice. You can use any technology available on the internet.

Deliverables
Upload the followings to Github:
- Code with README file
- Classification results for all 1000 fashion products added to the input json file
- Answers to the following questions:

- Why are you designing the solution in this way?

Basically I’m designing it like a standard ml pipeline. Data cleaning -> feature extraction (image and text) using pretrained models -> classification. Using best in class models available online. It would help combine aspects of both text and image in the category classification and we would get effective classification from all available inputs.

Input is a description and an image url. 
We do preprocessing by cleaning the description from html tags and resizing the images for correct model input. This is important to improve result quality.
Then to classify into categories we need to extract features and category scores from text and images. To do the same we would need bert like model word embedding for text representation and image classification model (bit-m google model) for image representation. 
Since, it's an unsupervised classification and the data is limited to 1000 only. It makes sense to use cosine similarity. (we could have done a supervised mlp if there was enough data with labels) To get scores we use cosine similarity of categories (embedding from bert model) and text_embedding, cosine similarity of categories (embedding from bert model) and weighted images classes embedding. Then we just combine the two and get argmax of scores for category.



- What are the aspects that you considered when designing?

Basic considerations were to use all data available and best pretrained models. 

I considered extracting more data from the internet like using bing api for better representation of categories and description. Having a graph of links to and from the image/product to classify better. Finetuning the image representation model using a dataset like fashion mnsist with the categories in consideration. But due to lack of compute resources and data, i wasn’t able to follow through.

Other considerations were using best models which I could run on my compute for image classification/representation and text representation. I considered labeling the data and using a supervised classification but data size was too small and it might not be what the problem was made with in mind.

I could have tried other clustering techniques to do classification too.

- What are the cases your solution covers, how are they covered and why are they
Important?

Data cleaning and resizing to properly run model and get good consistent results
Getting representation from all data. It is important to get representation of image and text as both form a complete representation of the category.
Classification using similarity to get most optimal category and considering if a category_score is low then classifying as other as there is no good way to classify others.

- What are the cases your solution does not cover and what are the ways you can
extend your current solution for them?

Cleaning images to get better results. Try applying various filters for better results.
Extracting more data from description/categories using bing api.

Finetuning the pretrained models for fashion classification and representation specific to our use case. A good way could be to collect more data or find a similar fashion dataset online like Fashion MNIST.

Exploring different pretrained models for image representation and text representation like LXMERT. Or multimodal models specifically trained for this task. 
Getting graph data of links (no. of pages pointing to the link and away from it) mentioned above or page_rank and using it in classification.

Using a mixture of Clustering and supervised classification to get better results. A better way could be to use kmeans clustering or Gaussian mixture models. Then using supervised learning or a simple mlp to classify the cluster produced along with word and image embedding.
