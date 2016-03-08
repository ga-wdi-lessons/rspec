#RSpec Cheat Sheet

##Commonly Used Terms

* `describe`: is a block that allows your code to be more readable and organized visually, allows you to discuss specific objects or methods

* `context`: is a block that functionally behaves the same way as `describe`, but should be used when describing different situations or "contexts"

* `it`:a block that allows you to test methods on the subject that return a simple value.

* `before(:each)`:is a block of code that runs before each test inside of it

* `before(:all)`:runs only once, before all the tests inside of it have started

* `subject`: allows you to control the initialization of the 'subject under test' and calls new on class your testing. This works the same way as `before(:each)` or `before(:all)` but could be considered more "semantic". With RSpec, it will usually be an instance of the object/class you are testing.

*  `let`: used to define a memoized helper method. The value will be cached across multiple calls in the same example but not across examples. `Let` is `lazy-evaluated`, meaning it is not evaluated until the first time the method it defines is invoked.

* `expectations`: begins with `expect(IUT).to`, or "Item Under Test"

* `matchers`:rspec contains built in matchers that can be used with expect(..).to or expect(..).not_to to define positive and negative expectations respectively on an object.
