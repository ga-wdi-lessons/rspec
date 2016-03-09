# Solution Code

##You-Do: Solution 1:

```rb
it "has a String for an Name" do
  dog = Dog.new("Rover", 10)
  expect(dog.name).to be_a(String)
end

```

##You-Do: Solution 2:
```rb
it "has a hunger level thats an Integer" do
  dog = Dog.new("Rover", 10)
  expect(dog.hunger_level).to be_a(Integer)
end
```

##You-Do: Solution 3:

```rb
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
```

## Final Solution Code:

### Before(:each)
```rb
require "rspec"
require_relative '../models/dog'

describe Dog do
  before(:each) do
    @dog = Dog.new("Rover", 10)
  end

  describe "attributes of a Dog" do
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

### Subject:

```rb
require "rspec"
require_relative '../models/dog'

describe Dog do
  subject(:dog) do
    dog = Dog.new("Rover", 10)
  end

  describe "attributes of a Dog" do
    it "has the class Dog" do
      expect(subject).to be_a(Dog)
    end
    it "has a String for an Name" do
      expect(subject.name).to be_a(String)
    end
    it "has an Integer for a hunger level" do
      expect(subject.hunger_level).to be_a(Integer)
    end
  end

  describe "#set_hunger_level" do
    context "when new hunger level" do
      context "is less than 0" do
        it "sets the hunger level to 0" do
          subject.set_hunger_level(-1)
          expect(subject.hunger_level).to eq(0)
        end
      end
      context "is greater than 0" do
        it "sets our hunger level to the new hunger level" do
          subject.set_hunger_level(5)
          expect(subject.hunger_level).to eq(5)
        end
      end
    end

  end
end
```

### Let:

```rb
require "rspec"
require_relative '../models/dog'

describe Dog do
  let(:dog) {Dog.new("Rover", 10)}

  describe "attributes of a Dog" do
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
