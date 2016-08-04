# RSpec

## Learning Objectives
- Explain the purpose and benefits of Unit testing
- Describe TDD and it's importance
- Explain what is RSpec
- Compare and contrast `expectations` and `matchers`
- Compare and contrast common RSpec terms including `"describe"`, `"it"`, `"context"`, `before(:each)`, `before(:all)`, `"subject"`,  `"let"`
- Write and pass unit tests using RSpec

## Framing: Introduction to Test-Driven Development

### Why do we implement tests in our applications? (5 min)

As our applications increase in complexity, we need a safety net.  We need something to ensure that we "Do no harm".  We need a battery of automated tests.  These are specifications about YOUR code that you can run to ensure your code is doing what it should.  

Think back to the way you code.  You create a part of a web page, then you browse to that page to test it.  To ensure that it is doing as you expect.  Then you add another feature.  And test both features.  Then you add a third feature and test... just the third feature.  Imagine if you had a battery of automated specs, which run against your code, so you can see if your new changes fit your new requirements and EVERY requirement that came before this.

### Unit testing (5 min)

**Unit tests** check the smallest level. The functionality of a specific method.

**Acceptance tests** verify our apps at the level of user interaction.  Testing for things when users visit web pages, click on links, validate the DOM, etc.  

  * The "units" in unit tests are individual methods. Unit tests are intended to test small, little blocks of code, and make sure a specific input results in a specific output.

  * As a rule of thumb, a good unit test should not be more than 5 lines long.

  * Functional tests have a much wider focus. You'd use functional testing to make sure a sign-in form works, or that a user who doesn't have admin privileges can see this page, while a user who does have admin privileges can see that page.

Unit testing always should come before functional testing. Functional testing is much less crucial. Unit testing is so important, that...

**Employers give you major bonus points for it!**

You'll see the term **test coverage** pop up pretty often. People are always aiming for "100% test coverage". If your app has 100% test coverage, that means every single method in your app has a unit test verifying that it works.

>For instance, while it's easy and free to write Salesforce apps, Salesforce will only add your app to its "app store" if you've obtained 100% test coverage, and Salesforce's developer team can run your tests and have them all pass.

**What are the reasons testing is so important? Why would employers love it so much?**

<!-- Real World Example: DC Tech Startups -->
<!--5 people from my cohort hired by Accella in charge of creating rspec tests  -->
<!--Planning on talking about two startups interviewed with and how wished they would have integrated more testing earlier on when developing their applications, it's now a big focus for them, cut corners early on and now need to refactor code base -->

We've asked you to write user stories. Writing unit tests is a very similar process.

When we think of "testing" we tend to think of something you do *after* you've created something. With unit tests, you're encouraged to write the tests *first* before you even start writing actual code.

### Turn and talk (5 min)

Turn to a partner and discuss reasons of why would you write tests beforehand?

>Answers

>When you write tests first, you're creating a tidy little checklist for yourself of things to complete. The **goal of unit tests** is that **when all of the tests pass, your app is complete**.

>You're used to thinking the other way around: when the app is complete, all the tests should pass. Writing the tests first forces you to think about what an app really *needs* to do to be complete. It forces you to scope things down to your MVP. It forces you to think of your app as a bunch of little pieces, rather than one big behoemeth.

>In short: writing out unit tests, even if you just leave them pending, will make this class much easier, and make you look super-marketable.

>This process of writing the tests **first** is called **Test-Driven Development**, or TDD.

### TDD Overview: (5 min)

![TDD Example](http://joshldavis.com/img/tdd-vs-bdd/tdd-flowchart.png)

**Benefits**

* Fewer bugs in our code

* Provides a clear goal in the development, that is, to make all tests to pass.

* Allows for automation and continuous integration, ensuring that our application won’t break

* A little more time upfront means a lot of time saved down the line! (Think about refactoring)

**DrawBacks**

* Requires time and effort.

* Could be more costly to an organization when there are changes in requirements.

## What is RSpec? (5 min)

**RSpec** is a testing framework for the Ruby programming language.

RSpec makes it easier to write tests.  It's a Domain Specific Language for writing live specifications about your code.  It was released on May 18, 2007, so it's been around for a while.  It is the defacto testing framework.

> DSL: "Domain Specific Language" that is created specifically to solve problems in a particular domain and is not intended to be able to solve problems outside it

---
### We-Do: RSpec Example (5 min)

Code is available here: [rspec_person_example](https://github.com/ga-dc/rspec_person_example)

When I run `rspec` in the `rspec_person_example` directory, what do we see?

```
Finished in 0.00565 seconds (files took 0.14281 seconds to load)
5 examples, 0 failures
```
Let's review `spec/person_spec.rb`.  This is the specification for a Person.  It indicates how we can expect a Person to function.
```
rspec_person_example/
├── models
│   └── person.rb
└── spec
    ├── person_spec.rb
    └── spec_helper.rb

2 directories, 3 files
```

We have a Person model and a Person spec (a specification or test). This is the typical RSpec convention.  Specs live under the spec directory and echo the models in our system with the `_spec` suffix.

Let's look further into ```person_spec.rb```

``` ruby
# This first line is a reference to our library code.  We need to access to the classes we have written in Ruby to write our tests!

require_relative '../models/person'  # a reference to our code

describe Person do
  describe "Constructor" do
    before(:each) do
      @matt = Person.new("Matt")
    end

    it "should create a new instance of class Person" do
      expect(@matt).to be_an_instance_of(Person)
    end

    it "should have a name" do
      expect(@matt.name).to_not be_nil
    end

    it "should default #language to 'English'" do
      expect(@matt.language).to eq("English")
    end
  end

  describe "#greeting" do
    context "for default language (English)" do
      subject(:bob) { Person.new("Bob") }

      it "should offer a greeting in English" do
        expect(bob.greeting).to eql("Hello, my name is Bob.")
      end
    end

    context "when language is 'Italian'" do
      subject(:tony) { Person.new("Tony", "Italian") }

      it "should offer a greeting in Italian" do
        # legacy syntax - the old DSL
        tony.greeting.should eql("Ciao, mi chiamo Tony.")
        # equivalent to:
        # expect(tony.greeting).to eql("Ciao, mi chiamo Tony.")
      end
    end
  end
end
```
**Q. What does `expect(@matt).to be_an_instance_of(Person)` mean in regular English?**

---

### You-Do - Modify Person.rb to fail tests (5 min)

**Instructions:**

1. Fork and Clone the Rspec Person Example Repo: https://github.com/ga-dc/rspec_person_example

2. In the root of `rspec_person_example directory` run `$ rspec --init` in our terminal.

3. Now run `$ rspec` in our terminal.

4. See the tests pass, now take a few minutes to adjust the code:

  * Comment-out various parts of the code, delete methods, add methods back in, etc.. and run the specs a few times.

  * Play with it! See how your actions in the code AND in the specs affect the output. See the specs fail, then make them pass again.

## We-Do - Create a Unit Test using RSpec

We are going to be creating something similar to the above example. Instead we will be writing a spec for creating a new ruby class of `Dog`

### RSpec Set-up (5 min)

In your `wdi/sandbox` directory:

Let's build out our directory for this exercise:
```
$ cd sandbox/
$ mkdir rspec-example
$ cd rspec-example
$ touch Gemfile
```

#### Install RSpec

We're going to do some stuff now that you haven't seen before. I want to walk through it first, and then explain what everything is afterward.

The first thing we'll do is install a gem called RSpec. To do this, just add `gem 'rspec'` to the `Gemfile`:

```rb
source "https://rubygems.org"

gem "rspec"
```

Then, in your Terminal:

```sh
$ bundle install
$ rspec
```
>After running `rspec`, you should get a message saying "No examples found." When it says "examples", it means "tests". It's saying, "You haven't written any tests for me to run!"

#### Set up the directory

Now, let's create a `spec` directory and add a file called `dog_spec.rb`. Additionally, we will be creating a `models` directory and a file where we will define our class `Dog`

```sh
$ mkdir spec
$ touch spec/dog_spec.rb
$ mkdir models
$ touch models/dog.rb
$ rspec --init
```
>`rspec --init`

>When you look at repos with RSpec inside them, you're likely to see two files we don't have right now: `.rspec` and `spec_helper.rb`. These files are generated by running RSpec's built-in file generator.

>Both of these files are configuration files. Neither of them are necessary unless you want to configure RSpec a certain way, for example adding color

>Within `.rspec` file add `--color` OR in `spec/spec_helper.rb` add `config.color = true`

### Writing our first tests (10 min)

Now, in our `models/dog.rb` file let's add the following code:

```rb
class Dog
  attr_accessor :name
  attr_reader :hunger_level

  def initialize(initial_name, initial_hunger_level)
    @name = initial_name
    @hunger_level = initial_hunger_level
  end

  def set_hunger_level (new_hunger_level)
    if new_hunger_level < 0
      @hunger_level = 0
    else
      @hunger_level = new_hunger_level
    end
  end

end
```
Now, let's start writing our tests! Let's add the following into our `spec/dog_spec.rb`:

```rb
require "rspec"
require_relative "../models/dog"  
```
To make sure everything's set up properly, run `rspec` again. You should still get "No examples found." If you get anything else, something was set up incorrectly.

We're writing tests that describe the Dog class. So, after all your `require` lines, write:

```rb
describe Dog do

end
```

...and remember, every `do` needs an `end`. Add it.

We're going to write a simple test just to make sure a new Dog has the class of Dog... which, of course, it will, but that's OK!

```rb
require "rspec"
require_relative "../models/dog"

describe Dog do
  it "has the class Dog"
end
```
Save the file, and run `rspec` again.

Now you should get a message in your Terminal like:

```plain
$ rspec
*

Pending: (Failures listed here are expected and do not affect your suite's status)

  1) Dog has the class Dog
     # Not yet implemented
     # ./spec/dog_spec.rb:5


Finished in 0.00033 seconds (files took 0.07384 seconds to load)
1 example, 0 failures, 1 pending
```

Wow! That's different! This is a list of all the tests we've written. Right now, that's a grand total of one.

There are a couple things to point out here.

- "Not yet implemented"
  - That means that this test doesn't actually test anything yet. Clearly it doesn't -- we just wrote some English, we didn't write any actual code.
- The file and line number
  - This shows the line on which that particular test is found.
- `1 example... 1 pending`
  - "Pending" is another way of saying "not yet implemented", and "example" is another way of saying "test".

Let's add another pending test:

```rb
describe Dog do
  it "has the class Dog"
  it "has a String for a Name"
end
```
**Q. Run `rspec` again. Anything crazy going on?**

---
You might have noticed when we ran `rspec` before that there was a little asterisk `*` at the top of the message, and now there are two `**`. This indicates two pending tests.

### It...do

Now add `do` at the end of the first `it` line. Remember, each `do` needs an `end`!

```rb
describe Dog do
  it "has the class Dog" do

  end
  it "has a String for an Name" do

  end
end
```

**Q. Run `rspec` again. What's different?**

---

```
..

Finished in 0.0005 seconds (files took 0.07273 seconds to load)
2 examples, 0 failures

```

Adding `do...end` makes RSpec think this test is an actual test -- not pending anymore. There's no malfunctioning code inside this test, so RSpec is saying it passes. Asterisk `*` indicates a pending test, and dot `.` indicates a passing test.

## Break (10 min)

## We-Do: Passing Our First Test (10 min)

Let's make these tests actually test something. Inside the first test, make (but don't save) a new Dog and save it to a variable.

```rb
it "has the class Dog" do
  dog = Dog.new("Rover", 10)
end
```

Now, let's tell the test that we expect that new dog to be a dog:

```rb
it "has the class Dog" do
  dog = Dog.new("Rover", 10)
  expect(dog).to be_a(Dog)
end
```

Run `rspec`. The test should still pass.

>Read that new line to yourself. We literally wrote "expect dog to be a dog". This is totally proper English but it's code! The methods that come built-in with RSpec were created in such a way that tests look as English-y as possible.

This is our first first spec or "expectation"

RSpec assertions have two components: `expectation` and `matcher`.

1. We expect `dog` to be something.

2. We identify that "something" with a Matcher:

> Expectation: `expect(dog).to `

> Matcher: `be_a(Dog)`

>We use `expect(IUT)` to "wrap" the ***Item Under Test***, so that it supports the `to` method which accepts a matcher. Here we are wrapping an object or block in expect, call to or to_not (aliased as not_to) and pass it a matcher object

[RSpec documentation Built in Matchers](https://www.relishapp.com/rspec/rspec-expectations/docs/built-in-matchers)

Now let's make the test **fail**. Let's say we "expect dog to be a Integer":

```rb
it "has the class Dog" do
  dog = Dog.new("Rover", 10)
  expect(dog).to be_a(Integer)
end
```

Run `rspec` and... You got an F! See how it says `F.` with a dot after it? That indicates you have one failing test, and one passing test.

Whenever a test fails, RSpec will put an error message after that test which should give you an idea of why it failed. This message is a little complicated, so let's create a simpler one.

Change the line to:

```rb
expect(dog.class.to_s).to eq("Integer")
```

Now we're saying, "the name of the dog's class should equal 'Integer'".

Run `rspec`. This new message is easier to read:

```
expected: "Integer"
  got: "Dog"
```

Before moving on, let's change the first test so it passes again!

## You-Do: Make the second test pass (10 min)

**Instructions:**

1. Spend 5 minutes writing code to make our second test pass!

2. Then we will review the solution together

[Link to see solution code](https://github.com/ga-wdi-lessons/rspec/blob/master/solution.md)

## You-Do: Create a new Spec (5 min)

**Instructions:**

1. Write a Spec that confirms the following: "has a hunger level thats an Integer"

## We-Do: Additional Tests Using Context (5 min)

Now, let's write a test for our method `set_hunger_level` that will be changing our dog's hunger level. Add in the following:

```rb
describe "#set_hunger_level" do
  context "when new hunger level" do
    context "is less than 0" do
      it "set the hunger level to 0"
    end
    context "is greater than 0" do
      it "set our hunger level to the new hunger level"
    end
  end
end
```
Let's go through it a bit at a time:

You can **nest** as many `describe` blocks as you want. What's the purpose? Just to lump together some tests. **It doesn't affect the code at all.** It's purely to keep things organized visually.

Also, **`context` does literally the exact same thing as `describe`**. They're identical. RSpec makes no difference between them. So why have both? To make your tests more readable from an English standpoint. You can see here I'm using `describe` for when I'm talking about specific objects or methods, and `context` when I'm talking about, well, different contexts. If I replace `describe` with `context`, and vice-versa, the tests will run the exact same way.

The hash `#` in front of `set_hunger_level` also doesn't do anything -- it's just what programmers usually use to indicate that something is a method, in the same way they use `$` to indicate a command you should enter in the terminal.

`describe` and `context` are not tests; they just help organize them. Only `it` is a test.

`it` also is **childless**. `it` cannot have any `describe`, `context`, or `it` blocks inside it.

 <!-- RSpec is all about making tests easy to read from an English standpoint. -->

## You-Do: Making the `#set_hunger_level` tests pass (10 min)

**Instructions:**

Given what we have done in class so far, spend the next 10 minutes getting our `'#set_hunger_level'` tests to pass!

## DRYing it up (10 min)

**Which lines on here repeat?**
```rb
describe Dog do
  it "has the class Dog" do
    dog = Dog.new("Rover", 10)
    expect(dog).to be_a(Dog)
  end
  it "has a String for an Name" do
    dog = Dog.new("Rover", 10)
    expect(dog.name).to be_a(String)
  end
  it "has an initial hunger level thats an Integer" do
    dog = Dog.new("Rover", 10)
    expect(dog.hunger_level).to be_a(Integer)
  end
  describe "#set_hunger_level" do
    context "when new hunger level" do
      context "is less than 0" do
        it "sets the hunger level to 0" do
          @dog = Dog.new("Rover", 10)
          @dog.set_hunger_level(-1)
          expect(@dog.hunger_level).to eq(0)
        end
      end
      context "is greater than 0" do
        it "sets our hunger level to the new hunger level" do
          @dog = Dog.new("Rover", 10)
          @dog.set_hunger_level(2)
          expect(@dog.hunger_level).to eq(2)
        end
      end
    end
  end
end
```

Usually, you're going to have a whole bunch of tests that all do very similar things. Writing `dog = Dog.new("Rover", 10)` a bunch of times would get tiresome.

Swap out your code with this:

```rb
require "rspec"
require_relative '../models/dog'

describe Dog do
  before(:each) do
    @dog = Dog.new("Rover", 10)
  end

  describe "attributes of a dog" do
    it "has the class Dog" do
      expect(@dog).to be_a(Dog)
    end
    it "has a String for an Name" do
      expect(@dog.name).to be_a(String)
    end
    it "has an Integer for a hunger level" do
      expect(@dog.hunger_level).to be_a(Integer)
    end
  end

  describe "#set_hunger_level" do
    context "when new hunger level" do
      context "is less than 0" do
        it "sets the hunger level to 0" do
          @dog.set_hunger_level(-1)
          expect(@dog.hunger_level).to eq(0)
        end
      end
      context "is greater than 0" do
        it "sets our hunger level to the new hunger level" do
          @dog.set_hunger_level(5)
          expect(@dog.hunger_level).to eq(5)
        end
      end
    end

  end
end


```
What changed? We moved the `Dog.new("Rover", 10)`, into a `before:each` block.  Since the local variable is not available across methods, we converted `dog` to an instance variable (with `@`).

Run `rspec`. It should still work.

### Change the `:each` to `:all`. Run `rspec`. What's different?

**before:each** is a block of code that runs *before each* test inside it. Try adding a `puts "*" * 50` inside `before:each`, then running `rspec`. You should see two lines of asterisks pop up.

**before:all** is the same concept, except it only runs **once**, *before all* the tests inside it have started.

### `before` vs `subject`

Now replace the code with this:

```rb

describe Dog do

  subject(:dog) do
    dog = Dog.new("Rover", 10)
  end

  describe "attributes of a dog" do
    it "has the class Dog" do
      expect(dog).to be_a(Dog)
    end
    it "has a String for an Name" do
      expect(dog.name).to be_a(String)
    end
    it "has an Integer for a hunger level" do
      expect(dog.hunger_level).to be_a(Integer)
    end
  end

  describe "#set_hunger_level" do
    context "when new hunger level" do
      context "is less than 0" do
        it "sets the hunger level to 0" do
          dog.set_hunger_level(-1)
          expect(dog.hunger_level).to eq(0)
        end
      end
      context "is greater than 0" do
        it "sets our hunger level to the new hunger level" do
          dog.set_hunger_level(5)
          expect(dog.hunger_level).to eq(5)
        end
      end
    end

  end
end

```
What changed?  We've identified that "dog" is the "subject under test", converting the instance variable (@dog) into the "subject" helper.  This method takes a name (:dog) and block of code that returns the subject (a new Dog with a name of Rover and hunger level of 10).  It provides a method, named "dog", that we now use throughout our spec.  

This is a way of ensuring the subject is available in every test, just like `before:each` and `before:all`. What's the difference? `subject` is semantic.**Functionally, however, 'before' and 'subject' are the same.**

Interestingly, we could also replace each use of "dog" with "subject".

### `let`

RSpec also provides a "let" helper, which works the same way.  You can use it to identify other important components of the specification.

`let` is "lazy-evaluated", only evaluated when directly called upon and value is cached the first time

You can have `subject`, `let`, and `before:each` right next to each other.

## Break (10 min)

## Garnet Example (5 min)

We use RSpec to test Garnet, the attendance/homework tracking app. Before any changes get pushed up to our live server, they have to pass all the tests -- an automated system rejects the changes if they don't pass.

[Here's what that looks like. Seem familiar?](https://travis-ci.org/ga-dc/garnet/builds/89503768#L241) Clearly there are a lot of tests that are just pending and don't do anything yet! These dramatically help us plan. But the main benefit is that tests tell you if you or anyone else breaks a class or function while working on the codebase at a later point. Everyone has to always run the test cases as they make the changes.

## Reminderly Example (10 minutes)

Let's take a look at tests in an app you're already familiar with.

You can clone the
[Reminderly repo](https://github.com/ga-wdi-exercises/reminderly/tree/master) and check out the testing branch.

Fair warning, this is a contrived example because the CRUD apps we've made so far in this class have been on the simple side. But I did want to demonstrate that testing is something you, yes you, can implement right now to demonstrate to employers that you understand the principles behind it.

The [rspec-rails](https://github.com/rspec/rspec-rails) gem has pretty strong documentation on setting up tests in your Rails application. This is a similar process to what we've already seen.

As stated before, testing is something you want to keep in mind right when you start building your application and the goal is to get you to start writing tests before you write your functional code. That said, since you are in essence learning a new DSL and you're likely more comfortable writing functional code, it might be helpful the first few times you play around with testing to write tests after your code to get a better feel for the rspec syntax.  
In this app, you'll notice I've written tests for the todo model and controller. With Rails apps, you'd generally want to focus on writing tests for model methods. We haven't covered model methods in this class, but we create them to manipulate our data. In this example, I concatenated the author_first_name and author_last_name fields to get a full name, which I can now use as a property.

I wrote tests for my controller simply to demonstrate that it can be done, but I wouldn't recommend you do the same when your doing your own tests. The point of testing is to make sure your own code is working but a lot of testing done in the controller seem to be more of a test of Rails, ie expecting a template to be rendered.

Another cool gem used to test web applications that can be used in tangent with rspec is called
[Capybara](https://github.com/jnicklas/capybara). We're not going to go too much into it today, but Capybara allows you write tests to simulate how users interact with and experience your application in the browser such as how they sign in. In the Reminderly example, I wrote tests to see that the root page has the words "All Todos" at the top and to see that the value of the body key is being displayed.


## You-Do: Let's Go Shopping (20 min)

**Instructions:**

 * Fork and Clone the following repo:
[rspec-shopping-exercise](https://github.com/ga-wdi-exercises/rspec-shopping-exercise/tree/master)

  > Don't forget to run bundle install!

 * Take a look at the `product.rb model`. Write unit tests in `product_spec.rb` to to test the methods it contains

 * You might need to refer to the RSpec documentation linked below for additional matchers to use when writing your tests

  [RSpec documentation Built in Matchers](https://www.relishapp.com/rspec/rspec-expectations/docs/built-in-matchers).  Make sure you are on the version that corresponds to your installed library (v3.3).

  ## Bonus!

  Try a TDD approach to solving this exercise - https://github.com/ga-wdi-exercises/luhn_algorithm

## The Flow (5 min)

Most testing frameworks, including RSpec, follow this flow:

  - Setup
  - Run
  - Teardown

Think `Red/Green/Refactor`

* Each spec should run in isolation.  

## Closing (5 min)

### Quiz Questions:

- What is the purpose Unit testing?
- How does Unit testing compare to Functional testing?
- Explain what role RSpec plays in testing.
- Describe TDD Cycle/Mantra
- Explain what is RSpec's basic syntax. Specially how does `describe` and `context` differ?

>Answers

>1. Design/architecture/maintainability/fewer bugs.
2. Unit tests are intended to test small, little blocks of code, and make sure a specific input results in a specific output. They are useful for us as developers. Functional tests verify our apps at the level of user interaction.  They visit web pages, click on links, validate the DOM.  
3. RSpec is a testing framework for the Ruby, makes writing tests much more simple for us as developers! We can use Rspec to write unit tests.
4. Red, Green, Refactor.  We write a test that fails, indicating that the feature is not supported.  Then, we adjust code until it passes (turns Green).  Lastly, we refactor our app using the knowledge we gained from supporting the spec.
5. "Describe" and "Context" FUNCTIONALLY do the same thing (context is an alias of describe) The difference is the intent they express.
"```describe```" indicates what I'm testing, typically a class or the name of a method while " ```context```" indicates a specific set of circumstances that effect the test (think WHEN!).

### Additional Resources
- [Learn Ruby via RSpec]( https://github.com/ga-dc/learn_ruby_via_rspec)
- [Code School RSpec](https://www.codeschool.com/courses/testing-with-rspec)
- [RSpec for Newbies](http://code.tutsplus.com/tutorials/ruby-for-newbies-testing-with-rspec--net-21297)
- [Mocks & Stubs](https://www.relishapp.com/rspec/rspec-mocks/docs)
- [How to use a Test Double](http://www.martinfowler.com/bliki/TestDouble.html)
- [RSpec Cheatsheets](https://www.anchor.com.au/wp-content/uploads/rspec_cheatsheet_attributed.pdf)
