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

[[Your answer goes here!]]

## Exercise 3

[[Your answer goes here!]]
