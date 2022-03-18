# Airbnb Predict Booking

![airbnb](https://user-images.githubusercontent.com/75986085/158188129-ab8930d2-7999-412b-b24f-bf1c25a01b84.png)

<h2>0. Bussiness Problem</h2>
<p><i>Airbnb, Inc. is an American company that operates an online marketplace for lodging, primarily homestays for vacation rentals, and tourism activities. Based in San Francisco, California, the platform is accessible via website and mobile app. Airbnb does not own any of the listed properties; instead, it profits by receiving commission from each booking.</i> ~Wiki</p>

<p>New users on Airbnb can book a place to stay in 34,000+ cities across 190+ countries. By accurately predicting where a new user will book their first travel experience, Airbnb can share more personalized content with their community, decrease the average time to first booking, and better forecast demand.</p>

> *Predict the user destination based on user info and sessions actions.*

<h3>0.1. What is a Marketplace ?</h3>
<p>The marketplace is a bussiness model based on demand and offer, the new client install the app or acess the airbnb site for search your next booking, this new client demand a booking, the city or country is the offer for the new client to travel, the money basically comes from a tax based on demand and offer transaction or a monthly price.</p>
<p>Examples of other two Marketplaces:</p>
<ul>
  <ol>Uber. (Passagers -> Taxi)</ol>
  <ol>Ifood. (Clients -> Restaurants)</ol>
</ul>
<p>One of the basic difference between marketplace and e-commerce, in marketplace, have some different sellers (have some other offerts) in example of Ifood, have some restaurants registred on app, in e-commerce is usually only products sold from the same company or manufacturer.</p>
<p>On the first step is publish the products on the plataform of marketplace, in example of ifood, several different sellers register their products on the marketplace platform like fastfood, new unique dishes, and other foods. There are companies specialized in registering products in several marketplaces, such as Brazilian Osit Plataform</p>

<h3>0.3. Metrics and First Assumptions</h3>
<ul>
  <dl>
    <dt>Offer (People offering Accomodations)</dt>
      <dd>☁ Number of New Users</dd>
      <dd>☁ Channels where these new users come (Online & Offline)</dd>
      <dd>☁ LTV (Life Time Value)</dd>
      <dd>☁ CAC (Client Aquisition Cost)</dd>
      <dd>☁ Frequency of Bookings.</dd>
      <dd>☁ Bounce Rate (On App or Website)</dd>
      <dd>☁ Other Site/App Metrics.</dd>
    <dt>Demmand (People Finding Accomodations)</dt>
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

<p>The Dataset Base <a href='https://www.kaggle.com/c/airbnb-recruiting-new-user-bookings'>House Prices at Kaggle</a>.</p>

<h2>1. Solution Strategy & Assumptions </h2>
<h3>First CRISP Cycle</h3>
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
      <dd>In Working.</dd>
  </dl>
</ul>

<h2>2. Exploratory Data Analysis</h2>

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

<h3>Top 3 Eda Insight's</h3>

<p>Users do not use Google to loggin in Airbnb.</p>

![s_method](https://user-images.githubusercontent.com/75986085/158493253-95c4569c-341c-43bd-949b-849fb20f7dfb.png)

<p>Users with mean take 40 days to reserve, but with median it takes around 5 days. (Outliers Problem)</p>

![mean](https://user-images.githubusercontent.com/75986085/158493271-582cb61a-54e2-4059-92a0-3db01f690556.png)

<p>The percentage of new bookings remains constant up to a certain period in relation to the percentage of previous bookings.</p>

![year_bookings](https://user-images.githubusercontent.com/75986085/158493281-6e19889a-e677-4648-83a2-f46d2c58d340.png)

<h2>3. Data Preparation</h2>
<p>Used Frequency Encoding for SMOTETomek, MinMaxScaler & RobustScaler.</p>
<p>I have selected Frequency Encoding because he have good results on my other projects and i selected again.</p>

<h3>SMOTETomek</h3>
<p>Smote is a technique for Oversampling based on k(5) nearest neighbours on dataset matrix space, and he generate new dataset row based on linear combination (convex combination). Tomeklinks is a Undersampling technique to reduce dataset size based on overlap data (M.L salt and pepper error) location</p>
<p>And have SMOTETomeklinks class on Python for use on unbalanced dataset</p>

<!--
<h2>4. Machine Learning Models</h2>


<h2>5. Bussiness Results</h2>


<h2>7. Model Deployment</h2>
-->

<h2>X. References</h2>
<ul>
  <li><a href='https://www.oreilly.com/library/view/practical-statistics-for/9781491952955/'>Practical Statistics Book</li>
  <li><a href='https://www.strategyzer.com/books/business-model-generation'>Model Bussiness Book</li>
  <li><a href='https://www.ideianoar.com.br/marketplace/'>Marketplace by "Ideia no ar"</li>
  <li><a href='https://imbalanced-learn.org/dev/references/generated/imblearn.combine.SMOTETomek.html'>Smote + Tomek Link</li>
</ul>
