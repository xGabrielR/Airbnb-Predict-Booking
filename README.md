# Airbnb Predict Booking

![airbnb](https://user-images.githubusercontent.com/75986085/158188129-ab8930d2-7999-412b-b24f-bf1c25a01b84.png)

<h2>Summary</h2>
<hr>

- [0. Bussiness Problem](#0-bussiness-problem)
  - [0.1. What is a Marketplace](#01-what-is-a-marketplace)
  - [0.2. Metrics and First Assumptions](#02-metrics-and-first-assumptions)

- [1. Solution Strategy & Assumptions Resume](#1-solution-strategy-and-assumptions-resume)
  - [1.1. First CRISP Cycle](#11-first-crisp-cycle)
  - [1.2. Second CRISP Cycle](#12-second-crisp-cycle)
  - [1.3. Third CRISP Cycle](#13-third-crisp-cycle)

- [2. Exploratory Data Analysis](#2-exploratory-data-analysis)
  - [2.1. EDA On First Cycle](#21-eda-on-first-cycle)
  - [2.2. Top 3 Eda Insights](#22-top-3-eda-insights)

- [3. Data Preparation](#3-data-preparation)
  - [3.1. SMOTETomek](#31-smotetomek)
  - [3.2. SMOTEEN](#32-smoteen)

- [4. Feature Space Study](#4-feature-space-study)
  - [4.1. PCA Embedding](#41-pca-embedding)
  - [4.2. UMAP Embedding](#42-umap-embedding)
  - [4.3. t-SNE Embedding](#43-t-sne-embedding)
  - [4.4. Tree-Based Embedding](#44-tree-based-embedding)

- [5. Machine Learning Models](#5-machine-learning-models)
  - [5.1. XGBoost Classifier First Cycle](#51-xgboost-classifier-first-cycle)
  - [5.2. Random Forest Classifier Second Cycle](#52-random-forest-classifier-second-cycle)

- [6. Bussiness Results](#6-bussiness-results)
  - [6.1. First Cycle](#61-first-cycle)
  - [6.2. Second Cycle](#62-second-cycle)

- [7. Model Deployment](#7-model-deployment)
- [8. References](#8-references)

---

<h2>0. Bussiness Problem</h2>
<hr>
<p><i>Airbnb, Inc. is an American company that operates an online marketplace for lodging, primarily homestays for vacation rentals, and tourism activities. Based in San Francisco, California, the platform is accessible via website and mobile app. Airbnb does not own any of the listed properties; instead, it profits by receiving commission from each booking.</i> ~Wiki</p>

<p>New users on Airbnb can book a place to stay in 34,000+ cities across 190+ countries. By accurately predicting where a new user will book their first travel experience, Airbnb can share more personalized content with their community, decrease the average time to first booking, and better forecast demand.</p>

> *Predict the user destination based on user info and sessions actions.*

<h3>0.1. What is a Marketplace</h3>
<p>The marketplace is a bussiness model based on demand and offer, the new client install the app or acess the airbnb site for search your next booking, this new client demand a booking, the city or country is the offer for the new client to travel, the money basically comes from a tax based on demand and offer transaction or a monthly price.</p>
<p>Examples of other two Marketplaces:</p>
<ul>
  <ol>Uber. (Passagers -> Taxi)</ol>
  <ol>Ifood. (Clients -> Restaurants)</ol>
</ul>
<p>One of the basic difference between marketplace and e-commerce, in marketplace, have some different sellers (have some other offerts) in example of Ifood, have some restaurants registred on app, in e-commerce is usually only products sold from the same company or manufacturer.</p>
<p>On the first step is publish the products on the plataform of marketplace, in example of ifood, several different sellers register their products on the marketplace platform like fastfood, new unique dishes, and other foods. There are companies specialized in registering products in several marketplaces, such as Brazilian Osit Plataform</p>

<h3>0.2. Metrics and First Assumptions</h3>
<ul>
  <dl>
    <dt>Offer (People offering Accomodations)</dt>
      <dd>☁ Number of New Users</dd>
      <dd>☁ Channels where these new users come (Online & Offline)</dd>
      <dd>☁ Bounce Rate (On App or Website)</dd>
      <dd>☁ Other Site/App Metrics.</dd>
    <dt>Demmand (People Finding Accomodations)</dt>
      <dd>☁ LTV (Life Time Value)</dd>
      <dd>☁ CAC (Client Aquisition Cost)</dd>
      <dd>☁ Frequency of Bookings.</dd>
      <dd>☁ Number of Country to Booking.</dd>
      <dd>☁ Mean price of theses countries.</dd>
      <dd>☁Properties Size / Diversity.</dd>
      <dd>☁ Country Marketing.</dd>
      <dd>☁ Property Quality.</dd>
  </dl>
</ul>

1. Have good photos of theses properties to user make a booking ?
2. How is the quality of theses properties to user make a booking ?
3. Old users can come back to make a new Booking ?
4. How is the user experience on App / Site to make your booking ?
5. How is the budget of marketing on theses countryes ?
6. How is the cost of new users based on old users ?
7. The fee of transaction is acessible to all new users based on counties ? ...

<p>The Dataset Base <a href='https://www.kaggle.com/c/airbnb-recruiting-new-user-bookings'>Airbnb Dataset</a>.</p>

<h2>1. Solution Strategy and Assumptions Resume</h2>
<hr>

![google_sheets_deploy](https://user-images.githubusercontent.com/75986085/161452041-90ee21ea-3a1a-42f7-b16a-4436490df41e.gif)

<h3>1.1. First CRISP Cycle</h3>
<ul>
  <dl>
    <dt>Data Clearing & Descriptive Statistical.</dt>
      <dd>First real step is download the dataset, import in jupyter and start in seven steps to change data types, data dimension, fillout na... At first statistic dataframe, i used simple statistic descriptions to check how my data is organized, and check <strong>strong Unbalance Dataset.</strong></dd>
    <dt>Feature Engineering.</dt>
      <dd>In this step, with coggle.it to make a mind map and use the mind map to create some hypothesis list, after this list, i created some new features based on mdatetime.</dd>
    <dt>Data Filtering.</dt>
      <dd>Simple filtering clear inconsistencies.</dd>
    <dt>Data Balance.</dt>
      <dd>Used SMOTETomek for Over and Undersampling.</dd>
    <dt>Exploratory Data Analysis.</dt>
      <dd>Analysis of two datasets simultaneously & hypothesis validation.</dd>
    <dt>Data Preparation.</dt>
      <dd>Frequency Encoding & Robust and MinMaxScaler.</dd>
    <dt>ML Models.</dt>
      <dd>XGBoost with apx 58% accuracy.</dd>
  </dl>
</ul>

<h3>1.2. Second CRISP Cycle</h3>
<hr>
<ul>
  <dl>
    <dt>Data Balance.</dt>
      <dd>Used SMOTEEN and SMOTETOMEK in new feature space based os data filtering.</dd>
    <dt>Data Preparation.</dt>
      <dd>Frequency Encoding & Robust and MinMaxScaler.</dd>
    <dt>ML Models.</dt>
      <dd>XGBoost with apx 66% accuracy.</dd>
      <dd>Base RF with apx 92% accuracy.</dd>
      <dd>Tuned RF with apx 90% accuracy (Simple Tuning)''.</dd>
  </dl>
</ul>

<h3>1.3. Third CRISP Cycle</h3>
<hr>
<ul>
  <dl>
    <dt>Feature Space Study.</dt>
      <dd>Used PCA Embedding for Dims reduction (2-4 Features)</dd>
      <dd>Used UMAP Embedding for Dims reduction (2 Features)</dd>
      <dd>Used t-SNE Embedding for Dims reduction. (3 Features)</dd>
      <dd>Used Tree-Based Embedding for Dims reduction.</dd>
      <ul>
          <li>Used PCA on Tree-Based Embedding.</li>
          <li>Used UMAP on Tree-Based Embedding.</li>
          <li>All Feature Spaces i used Smoteen and Smotetomeklinks Datasets.</li>
      </ul>
  </dl>
</ul>


<h2>2. Exploratory Data Analysis</h2>
<hr>

<h3>2.1. EDA On First Cycle</h3>

<p>In Univariable Analisys</p>
<ol>
    <li>The Dataset have some normal features.</li>
    <li>Secs Elapsed from Sessions dataset have high outliers.</li>
</ol>

<p>Bivariate Analysis</p>
<ol>
  <li>Users do not use Google to loggin in Airbnb.</li>
  <li>Users with mean take 40 days to reserve, but with median it takes around 5 days.</li>
  <li>The percentage of new bookings remains constant up to a certain period in relation to the percentage of previous bookings.</li>
</ol>

<p>List of Correlated Features</p>

<p>Train Dataset:</p>
<ul>
    <li>Categorical Features: affliate_provider, first_browser, first_device_type</li>
    <li>Numerical Features: Some Correlated Feature Engineering Dataset</li>
</ul>

<p>Session Dataset:</p>
<ul>
    <li>Categorical Features: action, action_detail</li>
    <li>Numerical Features: //</li>
</ul>

<h3>2.2. Top 3 Eda Insights</h3>
<hr>

<p>Users do not use Google to loggin in Airbnb.</p>

![s_method](https://user-images.githubusercontent.com/75986085/158493253-95c4569c-341c-43bd-949b-849fb20f7dfb.png)

<p>Users with mean take 40 days to reserve, but with median it takes around 5 days. (Outliers Problem)</p>

![mean](https://user-images.githubusercontent.com/75986085/158493271-582cb61a-54e2-4059-92a0-3db01f690556.png)

<p>The percentage of new bookings remains constant up to a certain period in relation to the percentage of previous bookings.</p>

![year_bookings](https://user-images.githubusercontent.com/75986085/158493281-6e19889a-e677-4648-83a2-f46d2c58d340.png)



<h2>3. Data Preparation</h2>
<hr>

<p>For Encoding, i selected Frequency Encoding, i like this encoder and Target Encoder.</p>
<p>I have selected Frequency Encoding because he have good results on my other projects and i selected again.</p>
<p>For Rescaling i used both, MinMax and RobustScaler and for Nature Transformation used SIN / COS transformation.</p>

![sm](https://user-images.githubusercontent.com/75986085/159078786-432ad933-30b2-4276-bd96-9488a0f6ead5.png)

<p>Diff between Smote, Smoteenn & Smotetomek, on references for more details.</p>

<h3>3.1. SMOTETomek</h3>

<p>Smote is a technique for Oversampling based on k(5) nearest neighbours on dataset matrix space, and he generate new dataset row based on linear combination (convex combination). Tomeklinks is a Undersampling technique to reduce dataset size based on overlap data (M.L salt and pepper error) location</p>
<p>And have SMOTETomeklinks class on Python for use on unbalanced dataset</p>

<h3>3.2. SMOTEEN</h3>

<p>Similar to smotetomek, but now the undersamplig is based on Edited Nearest Neighbours, with smoteen, the Random Forest Model have more performcae.</p>

![features](https://user-images.githubusercontent.com/75986085/159298757-3af49b28-6084-4d38-967c-61f41d138f4b.png)

<p>For Feature selection to dims reduction, only used Feature Importances of Random forest & Xgboost.</p>
<p>In Next Cycles i use BORUTA and Other Techniques.</p>

<h2>4. Feature Space Study</h2>
<hr>

<h3>4.1. PCA Embedding</h3>
<p>The PCA performs a dimensionality reduction based on Eigenvalues and eigenvectors.</p>
<p>In the PCA, first you need to set a n_components, its number of columns to performace the PCA. After that, the PCA will return the main combinations of the features with the greatest variation.</p>

![pca_results](https://user-images.githubusercontent.com/75986085/159299291-77329e23-2afc-40b7-94a4-2f574ca47bec.png)

<p>PCA without Tree and Reduced Dataset (10000 Examples)</p>

![pca_reduced](https://user-images.githubusercontent.com/75986085/159311433-be72c553-77d2-4d74-8add-c9d5eb8d4f60.gif)

<p>I have worked with full dataset twoo, but is hard to see any classification region</p>

![pca_full](https://user-images.githubusercontent.com/75986085/159311536-89c49d26-3d66-4f2d-b027-de5a9f9171d5.gif)

<h3>4.2. UMAP Embedding</h3>
<p>The UMAP performs a dimensionality reduction based on Manifold (topological space), similar to t-SNE.</p>

![umap_reduced](https://user-images.githubusercontent.com/75986085/159311605-d177ec81-9919-4263-b2a4-c7a043c1cea6.png)

<p>I worked with UMAP reduced dataset to see any classification region on dataset.</p>

<h3>4.3. t-SNE Embedding</h3>
<p>The t-SNE performs a dimensionality reduction based on Manifold (topological space), is a tool to visualize high-dimensional data.</p>

![tsne_reduced](https://user-images.githubusercontent.com/75986085/159311834-ae81cc42-de07-4109-b14a-341bda2d97bd.png)

<p>Same thing to t-SNE, i prefer using reduced on this step to see classification regions. But t-SNE dont haved a good performace on reduced and full dataset.</p>

![tsne_full](https://user-images.githubusercontent.com/75986085/159311932-79267dfd-4982-41e9-8323-ddc36c71528d.gif)

<h3>4.4. Tree-Based Embedding</h3>
<p>The Random Forest do not performs a dimensionality reduction, its possible to take the leaves of forests, because Tree make a embedding on leaves.</p>

<p>In Tree, i tested PCA and UMAP on both datasets, reduced and full.</p>

![umap_tree_reduced](https://user-images.githubusercontent.com/75986085/159312124-73b36cc1-43f6-46e2-ba07-15acbdf74bc9.png)

![pca_tree_reduced](https://user-images.githubusercontent.com/75986085/159312158-aaa9acc1-b5fd-438d-9324-aee3220b0b8d.png)

![pca_tree_reduced](https://user-images.githubusercontent.com/75986085/159312596-42034d6c-8182-480b-83a7-a07fa66bcb4c.gif)

<p>UMAP and PCA reducers, both in reduced dataset to see any new region, but with tree leaves both haved greate performace.</p>

![pca_tree_full](https://user-images.githubusercontent.com/75986085/159312623-7711da22-896d-4489-b6ea-c8098c9d484c.png)

![pca_tree_full](https://user-images.githubusercontent.com/75986085/159313068-6be15228-a185-4056-bbd4-e4ef09a44d67.gif)

<p>On full Dataset, PCA look's like a Monster / Dragon xD</p>



<h2>5. Machine Learning Models</h2>
<hr>

<h3>5.1. XGBoost Classifier First Cycle</h3>

<p>I selected Only two models, a XGBClass & Neural Network with 64 Layers, but NN dont haved a good performace and take a long time to train, because of that i have selected XGB to Hyperparameter Tuning.</p>
<p>With Random Search technique and cross validation, i have a tunned model with +0.2% of balanced accuracy for next predictions on first cycle.</p>

![model](https://user-images.githubusercontent.com/75986085/159079769-efb420c0-41f9-4caa-98ee-cd4b999b719b.png)

<p>The total model performace based on Mean and Standard Deviation for Cohen Kappa of ( 0.5396 +/- 0.0016 ) and for Balanced Acuracy of (	0.5571 +/- 0.0016 )</p>

![bootstrap](https://user-images.githubusercontent.com/75986085/159080057-c8a214f8-0966-4f63-8e35-4af61bfa7581.png)

<p>With 75.0% of confidence interval, the model performs is 54.7% and 55.3% based on 100 bootstrap (random sampling of dataset) to train and predict on validation dataset, this technique is similar to cross validation.</p>

<h3>5.2. Random Forest Classifier Second Cycle</h3>

<p>On first cycle, i have tested XGBoost, and on second too in new dataset based on SMOTEEN, but XGBoost do not have good performace again.</p>
<p>At second cycle Random Forest Model haved better performace to classify new bookings, with this model i reached at 90% balanced accuracy for new users without using sessions dataset. With XGBoost i reached at aprox 67% of Balanced Accuracy in new dataset.</p>

![3](https://user-images.githubusercontent.com/75986085/159268514-8aa1d2ec-f692-4dd8-a2c6-264341f94849.png)

<p>With Random Search technique and cross validation, i have a tunned model with +/-.1% of balanced accuracy for next predictions on second cycle.</p>
<p>Why this performace? I have selected more simple model on Tuning, for a good tuning, need to train more times with more and different model parameters, for RF on second cycle i only selected three parameters for random search.</p>

![bootstrap](https://user-images.githubusercontent.com/75986085/159269031-b5d1927c-0486-4cd0-a194-48b84d0fff20.png)

<p>I have performed a simple bootstrap with 1000 iterations to check the confidence interval of model performace in different scenarios.</p>

<h2>6. Bussiness Results</h2>
<hr>

<h3>6.1. First Cycle</h3>

![res](https://user-images.githubusercontent.com/75986085/159080572-d5e0ae1a-46bb-4f58-962a-dccf925c4b6d.png)

<p>On Train Dataset and Validation Dataset, the model haved some good and worst predictions.</p>

<ul>
    <li>Total of Users on Dataset: 508991 </li>
    <li>Total of Unique Rows on Dataset: 490961 </li>
</ul>

<h3>6.2. Second Cycle</h3>

![rf_r](https://user-images.githubusercontent.com/75986085/159265745-d7ef43d0-9cac-474a-9a54-4f5ff6a9276b.png)

<p>RF Model is more superior than XGBoost for this dataset.</p>
<p>RF Model do not wrong any NDF class booking destination.</p>

<h2>7. Model Deployment</h2>
<hr>

https://user-images.githubusercontent.com/75986085/161451983-2ed0fdd2-da30-463d-af22-846a29223bc4.mp4

<p>At Google Sheets with Google Sheets Scripts (.gs) and Heroku for Model.</p>

<h2>8. References</h2>
<hr>

<ul>
  <li><a href='https://www.oreilly.com/library/view/practical-statistics-for/9781491952955/'>Practical Statistics Book</a></li>
  <li><a href='https://www.strategyzer.com/books/business-model-generation'>Model Bussiness Book</a></li>
  <li><a href='https://www.ideianoar.com.br/marketplace/'>Marketplace by "Ideia no ar"</a></li>
  <li><a href='https://partner.booking.com/pt-br/ajuda/trabalhar-com-booking/ficando-online/como-bookingcom-funciona-para-propriet%C3%A1rios'>Booking by "partner.booking".</li>
  <li><a href='https://imbalanced-learn.org/dev/references/generated/imblearn.combine.SMOTETomek.html'>Smote + Tomek Link</a></li>
  <li><a href='https://imbalanced-learn.org/stable/references/generated/imblearn.combine.SMOTEENN.html'>Smote + Edited Nearest Neighbours</a></li>
  <li><a href='https://imbalanced-learn.org/dev/auto_examples/combine/plot_comparison_combine.html#sphx-glr-auto-examples-combine-plot-comparison-combine-py'>Smote, Smoteen & SmoteTomek</a></li>
  <li><a href='https://scikit-learn.org/stable/modules/generated/sklearn.manifold.TSNE.html'>t-SNE</a></li>
  <li><a href='https://umap-learn.readthedocs.io/en/latest/'>UMAP</a></li>
  <li><a href='https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html'>PCA</a></li>
  <li><a href='https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html'>Random Forest Classifier</a></li>
</ul>
