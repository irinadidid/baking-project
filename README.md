# baking-project
I started baking in the beginning of the pandemic in 2020. I was wondering what makes a cookie so crunchy, a bread that fluffy and a cake so spongy. So I decided to work on a project that will shed the light on a magic behind backing. 

Baking project is an exploratory data analysis followed by a charecter-level LSTM RNN trained on ~ 26k recipes from Kaggle dataset.

### Data 
is avaliable here https://www.kaggle.com/shuyangli94/food-com-recipes-and-user-interactions

We have cleaned and prepared the data by selecting only baking recipes that consist of no less then 2 steps and ingredients. Then, we assigned each recipe a 'recipe type'.

## Preliminary data analysis 
showed the key differences between cakes, breads and cookies in terms of effort, time and ingredients needed. 

<img width="1258" alt="ingredients distribution" src="https://user-images.githubusercontent.com/81694642/149795727-8a2f13f9-5bd3-4b3b-be58-59e3fc3ee218.png">

*Pic. 1. Distribution of the number of inredients.*

<img width="1273" alt="estimated cooking time" src="https://user-images.githubusercontent.com/81694642/149796358-a77a8bb5-a05f-4188-a9e0-2cc39c815399.png">

*Pic. 2. Estimeted cooking time in minutes.*

Here we notice that in both cases on average cake recipes seem to be more difficult to repeat as they require more ingredients and more effort i.e steps to folllow.
For cookies we see less variability in number of ingredients and number of steps as well as time to cook.
At the same time bread recipes are very diverse: from easy-to-follow 3 steps breads to very time consuming 145 steps recipe requiring 43 ingredients. On average it takes longer to cook a bread rather then cake or cookies.

## Text analysis 

gave us an idea of what cookies, cakes and bread are made of. We have scraped the most common ingredients for each recipe type.

*Cookies:*

<img width="300" alt="cookie ingredients" src="https://user-images.githubusercontent.com/81694642/149798237-f6d79076-de08-4033-99dc-81dac51f544e.png">

*Cakes:*

<img width="300" alt="cake ingredients" src="https://user-images.githubusercontent.com/81694642/149798612-b8125801-e7eb-4aff-af1b-911cb421ec43.png">

*Breads:*

<img width="300" alt="bread ingredients" src="https://user-images.githubusercontent.com/81694642/149803695-918bf698-8dff-40b0-9be2-399a9cb25232.png">

### Things to improve

- The number of observations could be extended by scraping more recipes from web 
- Some sweet breads should be marked as 'cakes' for better classification (i.e banana bread) 

## LSTM model training 

On a high level, Recurrent Neural Network (RNN) is a class of deep neural networks, most commonly applied to sequence-based data like speech, voice, text or music. They are used for machine translation, speech recognition, voice synthesis etc. The key feature of RNNs is that they are stateful, and they have an internal memory in which some context for the sequence may be stored. For better understanding consult https://colah.github.io/posts/2015-08-Understanding-LSTMs/

Our RNN was was trained on Python using TensorFlow 2 with Keras API.

Model components: 

<img width="487" alt="plot model" src="https://user-images.githubusercontent.com/81694642/149805007-cb40dc7c-af2a-45bf-9ec1-ea130fcee019.png">

For each character the model looks up the embedding, runs the LSTM one time-step with the embedding as input, and applies the dense layer to generate logits predicting the log-likelihood of the next character.

### Example generated recipe 

> 📌 TITLE
>
> chocolate cake
>
> 👀 DESCRIPTION
>
> this is the dough on the topping with bread machine.
>
>🍒 INGREDIENTS
>
> • white sugar <br>
>• eggs <br>
>• milk <br>
>• vanilla extract <br>
>• all-purpose flour <br>
>• baking powder <br>
>• salt<br>
>• baking soda<br>
>• baking soda<br>
>• salt<br>
>• butter<br>
>• sugar<br>
>• vanilla extract<br>
>• baking powder<br>
>• baking soda<br>
>• salt<br>
>• sugar<br>
>• vanilla<br>
>• cream<br>
>• salt<br>
> 
>📝 INSTRUCTIONS
>
>▪︎ preheat oven to 350f<br>
>▪︎ butter a 9x5x3' pan<br>
>▪︎ blend self raising eggs , one at a time , beating well with the flour and salt<br>
>▪︎ stir in the chocolate chips and salt<br>
>▪︎ add the milk and vanilla<br>
>▪︎ stir in the butter , and mix well<br>
>▪︎ add the chocolate chips and remaining sugar<br>
>▪︎ add the eggs , one at a time , beating well after each addition<br>
>▪︎ pour into prepared pan<br>
>▪︎ bake at 350 for 12-12 minutes or until golden brown<br>
>▪︎ cool in pan for 10 minutes<br>
>▪︎ top with remaining cream cheese , then refrigerate for at least 2 hours or until the cake is set and the cake is set , about 25 minutes until the cake pan<br>
>▪︎ refrigerate for at least 1 hour<br>
>▪︎ remove f<br>

## Demo

Demo is avaliable in the last cell of the ```baking-project.ipynb```

I have been using an opensource project https://gradio.app

![demo](https://user-images.githubusercontent.com/81694642/149809091-08b409bf-0703-4311-8e68-ae32046525fa.gif)

### Things to improve 

- Recipe title, description, ingredients and instructions are disconneced most of the time 
- We have lots of repetitions especially on the ingredients section
- For better perfomance we could, again, use more data
