---
layout: post
title:      "RSpec: Using BDD In Our Code"
date:       2018-05-24 21:43:42 +0000
permalink:  rspec_using_bdd_in_our_code
---



RSpec is a great way to test your code in Ruby, and implement BDD (behavior-driven development). BDD was built on top of Test Driven Development (TDD) in order to allow us to develop tests that are based on the specifications of system behavior. Our tests cases are still written in the most concise way, but now we can be even clearer about how the code should behave.

Let’s look at an example of BDD:
```
describe Order do
  describe "#submit" do

    before do
      @meal = Meal.new(:name => "Steak", :price => 16)
      @customer = Customer.new
      @order = Order.new(@customer, @meal)

      @order.submit
    end

    describe "customer" do
      it "puts the ordered meal in customer's order history" do
        expect(@customer.orders).to include(@order)
        expect(@customer.ordered_meals).to include(@meal)
      end
    end

    describe "order" do
      it "is marked as complete" do
        expect(@order).to be_complete
      end

      it "is not yet delivered" do
        expect(@order).not_to be_delivered
      end
    end
  end
end
```


Now that we’ve seen a bit of BDD, we can explore more of RSpec to help us build a method to add up some strings. 

First we set up RSpec by adding `gem “rspec”` to our Gemfile, and run `bundle install` in our terminal.

Next we will run ` mkdir spec` in our terminal to make a directory folder where we will store our “specs".

```
# spec/add_strings_spec.rb 

describe AddString do  
end 
```

We want to describe the behavior, so we always put a `describe` block in our specs. 

Let’s run our tests:

`bundle exec rspec`


We haven’t written any code yet, so our test will fail. You should see `uninitialized constant AddString (NameError)`. 

Create a new directory where we will store our classes:

`mkdir lib `

Inside this folder create a file that will contain our AddString class.

```
# lib/add_string.rb 
class AddString 
end 
```

We must add this file to our spec, so it can locate it. 

```
# spec/add_string_spec.rb 

require “add_string” 

describe AddString do 
end 
```

Try running the tests again. They pass, but we have no examples. Let’s get coding. 

Lets first start with a simple task. If our input is an empty string, we want to return 0. 

```
# spec/add_string_spec.rb
describe AddString do

  describe ".add" do
    context "given an empty string" do
      it "returns zero" do
        expect(Addstring.add("")).to eql(0)
      end
    end
  end
end
```


Let’s break this code down:

* We use another `describe` block for our add method. We prefix class methods with a “.” and an instance method with a “#”. 
* We use a `context` block to describe a context where this test should pass. 
* We use an `it` block to describe a specific example or “test case”. 
* We use `expect(...).to` or `expect(...).not_to` to define expected outcomes. `Eql` is then our matcher to fully define an expectation of our piece of code. 


If we run our spec, we’ll get a new failure, `NoMethodError`. So we must create that method. 

```
#lib/add_string.rb 

class AddString 
 
 def self.add(input)
   0
 end 

end
```

Our code will pass. Now we are ready to add more tests for actual input. 

```
# spec/add_string_spec.rb
describe AddString do

  describe ".add" do
    context "given '4'" do
      it "returns 4" do
        expect(AddString.add("4")).to eql(4)
      end
    end

    context "given '10'" do
      it "returns 10" do
        expect(Addstring.add("10")).to eql(10)
      end
    end
  end
end
```


To make these new tests pass, we must add code to our `.add` method. 

```
# lib/add_string.rb

class AddString

  def self.add(input)
    if input.empty?
      0
    else
      input.to_i
    end
  end
	
end
```


We want our `.add` method to actually add, so let’s write some tests for example strings. 

```
# spec/add_string_spec.rb

describe AddString do

  describe ".add" do
    context "two numbers" do
      context "given '2,4'" do
        it "returns 6" do
          expect(AddString.add("2,4")).to eql(6)
        end
      end

      context "given '17,100'" do
        it "returns 117" do
          expect(AddString.add("17,100")).to eql(117)
        end
      end
    end
 end

end
```


And now we are ready to add our final bit of code to get these tests to pass. 

```
class AddString

  def self.add(input)
    if input.empty?
       0
    else
       numbers = input.split(",").map { |num| num.to_i }
       numbers.inject(0) { |sum, number| sum + number }
    end
  end
end
```


Our tests should pass now, and we have successfully used RSpec to drive our code. 


