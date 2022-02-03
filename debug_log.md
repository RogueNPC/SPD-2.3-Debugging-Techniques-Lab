# Debug Log

**Explain how you used the the techniques covered (Trace Forward, Trace Backward, Divide & Conquer) to uncover the bugs in each exercise. Be specific!**

In your explanations, you may want to answer:

- What is the expected vs. actual output?
- If there is a stack trace, what useful information does it contain?
- Which technique did you use, on which line numbers?
- What assumptions did you have about each line of code, and which ones were proven to be wrong?

_Example: I noticed that the program should show pizza orders once a new order is made, and that it wasn't showing any. So, I used the trace forward technique starting on line 13. I discovered the bug on line 27 was caused by a typo of 'pzza' instead of 'pizza'._

_Then I noticed another bug ..._

## Exercise 1

I noticed there was a TypeError: 'topping' is an invalid keyword argument for PizzaTopping after entering a new pizza order.  So, I used the Divide and Conquer technique to analyze where the pizza toppings were being added in the Pizza object.  I found the bug in line 79 where pizza toppings were being added .append(PizzaTopping(topping=topping_str)), the attribute in PizzaTopping is called topping_type not topping.

There was another bug on line 80 -- TypeError: 'in <string>' requires string as left operand, not ToppingType.  Using trace forward technique, I found on that same line, the for loop was going through a class when I could simply loop through toppings_list.

There was a bug in the next line appending a PizzaTopping object into the pizza toppings attribute because it assigned toppings=topping_str when the PizzaTopping model uses the term topping_type.  I changed line 81 to ...append(PizzaTopping(topping_type=topping_str))

I discovered a bug on line 74 where the Pizza order was being constructed without a toppings attribute, therefore when we append the toppings to the pizza object on line 78, there was nowhere to append to.  I created a toppings attribute in the constructor assigned as an empty list for us to append our toppings to.

Another bug appeared after submitting an order, there was an error in destination page.  Using Divide and Conquer, I found a bug on line 85 where the redirect was trying to go to a route when it should have redirected to the html file.

Seeing the print statement on line 77, there was a bug where pizza.size was return none.  I used the trace backwards technique to figure out why it was returning none. The pizza.size comes from pizza_size_str, which comes from the request form for 'size'.  Checking the order form, the size value is inputed as 'pizza_size' which is not the same as 'size'.

There were still no pizza orders that showed on the homepage, so I used Divide and Conquer to find out why there wasn't anything showing up.  I first checked through the route and template, but after figuring out there was nothing wrong with the querying and rendering, I later realized the pizza object wasn't being commited into the database on line 83.

There was another error regarding the order_name on line 67. I used the trace backwards technique to figure out why it was returning none. Like the problem with pizza.size, there was an inconsistancy with the naming of the form field.  One was called 'order_name' while the other was trying to get 'name'.

After inputing my order, I was still geting errors with the toppings in the form of 'str' is not a 'list' so after using Divide and Conquer on line 66 - line 81, I found out I needed to request.form.getlist('toppings') instead of request.form.get('toppings').

After all that I noticed nothing was showing up on the homepage, so doing Divide and Conquer again, I went to the home.html page and noticed there was an else statement in the bottom of the file without an if statement.  I added the if statement on line 8 {% if pizza_orders %}.

## Exercise 2

The first bug after clicking submit was File "/exercise-2/app.py", line 52, in results 'city': result_js ['name'], KeyError: 'name'.  Looking at line 52, I see that that it involves the weather API so I decided to take a peek into the result_json to see if it was getting the data... and I get {'cod': '400', 'message': 'Nothing to geocode'}.  After finding no problems with the API call, I traced backwards checking to see if there was something wrong with the city and units being requested from the user form... which there was, there were no city or units being obtained.  The problem was that the html form in home.html was entering the city under 'city' and units under 'units', but on line 40 of app.py, thery were called 'users_city' and 'requested_units'.  After changing those, I was getting the city and units entered by the user.

I also noticed on line 44, the API_KEY was being passed in as a global variable and not from the .env file.  I used os.getenv('API_KEY') instead to get that working.

I was still getting the {'cod': '400', 'message': 'Nothing to geocode'} bug so I ended up scouring the API documentation on the openweathermap webpage and I realized that the parameter for city name has to be 'q' and not 'city' on line 45 of app.py.  After replacing city with q, I was able to get the API call working.

Another bug appeared on line 56 with 'temp': result_json['main']['temperature'], KeyError: 'temperature'.  Checking the documentation again I see that temperature is stored under the varaible 'temp' so I changed line 56 to 'temp': result_json['main']['temp'].

After that bug fix, it returned the result page successfully.

## Exercise 3

[[Your answer goes here!]]
