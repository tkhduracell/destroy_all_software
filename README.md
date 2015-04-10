# Destroy all software notes
Notes on the Destroy All Software series

## Season 5

### Python vs. Ruby
#### Philosophy
 * Python: everything is an attribute.
 * Ruby: everything is a method call. 

#### Vision
 * Python is optimising for data access
 * Ruby is focusing on messages between objects, rather than data
  
**Question** 
Is Ruby more "object oriented" due to this fact?

### Rails: Where is correctness enforced?
**Answer**
In the database, or at least it should be. Use database layer validation and indices to enforce correctness.

A lot of complexity in models/controllers is often a sign of a poorly designed database schemes. The solution is what we have been doing for 30 year, upfront design of the database. Of course without preaching up-front application design and development.   
### Separating arrangement and work
Actors and composition
```ruby
def congratulate
  TopComments.start >> CongratulationsMailer.start 
end
```

vs. sequential calls
```ruby
def congratulate
  comments = TopComments.sort_by(...).take 10
  CongratulationsMailer.send_congratulate commments 
end
```

### Half-functional ruby
```ruby
# Nasty IOstuff
def main
  Dir["*.md"].each do |path|
    content = File.read path 
    out = SafeSuff.new(content).stuff
    File.write "#{path}.out"
  end
end

# Pure functional, no side-effects
class SafeStuff
  attr_reader :content

  def stuff
    content.upcase
  end
end
```

