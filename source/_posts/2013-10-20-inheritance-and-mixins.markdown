---
layout: post
title: "inheritance-and-modules"
date: 2013-10-20 18:24
comments: true
categories: 
---

At the end of last week, we discussed inheritance and modules.  I needed to review it as not all of it had sunk-in at runtime-lecture.  So here goes:

If one of the many purposes of Ruby Classes is to help free us from redunancy by making certain methods available to all instances of that class.  Along that line it seems inheritance builds on the notion of "sharing" in that it allows a Class to make its capabilities available to sub-classes and include further specificity and/or additional methods where necessary.  

As I researched inheritance up, people liked using taxonomies to help illustrate [this](http://www.rubist.net/~slagell/ruby/inheritance.html). I'll do the same but instead use plants instead of animals/mammals/etc.  The plant kingdom has certain characteristics that hold true for all things defined as plants including such attributes as-- they are cellular, they can convert energy from sunlight to food, they can propogate etc.

There are two primary subclasses of plants: seed-bearing and spore-bearing. Both subclasses possess the primary plant kingdom characteristics (cellular, absorb sunlight) but they also possess additional specifics such as being able to have flowers, being able to either absorb water or circulate fluids throughout itself or being of a certain sex or asexual.  

So in Ruby:

	class Plant
	end

	class Rose <Plant
	end

	class Algae < Plant
	end


The Rose class and Algae class are "Child" classes that inherit (denoted by `<`) all characteristics of the "Parent" class Plant. This makes it easy to ascribe further specificity:

	class Plant
		def live
			puts "multicellular, can reproduce, absorbs light, circulate or absorb water"
		end
	end

	class Rose <Plant
		def make_flower
			puts "leaf, stem, roots" 
		end
	end


	class Moss < Plant
		def produce_spore
			puts "simple, can live on another plant"
		end
	end


A Rose and Moss are a type of plant but also have their own specialized things they can do.  Its important to note that in Ruby, at least, a Class can only inherit features from **one** other class.

This brings us to Modules and Mixins.  Modules are, according to [Ruby docs](http://www.ruby-doc.org/core-1.9.3/Module.html), a collection of methods and constants.  Hmmm. Need more help here. As it turns out, Ruby itself possesses a number of modules in its standard library.  A quick example in IRB:

	irb> Math.sqrt(2)
   	=>1.41421
	irb> Math::PI
   	=>3.14159	

The `::` operator denotes which module Ruby should use for the value of a constant. If we want to refer to the methods or constants of a module directly without using `::`, we can `include` that module:

	irb> include Math 	
	=>Object
	irb> sqrt(2)
	=>1.41421
	irb> PI
	=>3.14159

As mentioned in the Pickaxe, "Modules define a namespace, a sandbox in which your methods and constants can play without having to worry about being stepped on by other methods and constants." This is one important use of modules. 

The other key important use of modules is that, like inheritance, modules allow functionality to be "shared" between classes thereby streamlining the number of times you have to write the same methods. As one person describes,

"mixins are a group of methods not yet attached to any class.  They exist in a module and are not useful until included in a class.  Once included they are now normal methods of a class." ([source](http://ruby.about.com/od/beginningruby/a/mixin.htm))

So illustrating on the above Class inheritance structure:

	module Plant
		def live
			puts "multicellular, can reproduce, absorbs light, circulate or absorb water"
		end
	end

	class Rose <Plant
		include Plant

		def make_flower
			puts "leaf, stem, roots" 
		end
	end


	class Moss < Plant
		include Plant

		def produce_spore
			puts "simple, can live on another plant"
		end
	end


Methods within a module can either be instance methods or module level methods.  In the example above, the module is included within a class, thus the module's methods are "mixed in" as instance methods and apply to all instances of the Rose and Moss classes. As 

Why may modules be a better choice over classes with inheritance?

As [this person](http://ducktypo.blogspot.com/2010/08/why-inheritance-sucks.html)  states: Modules are generally more flexible than superclasses.  Modules can be managed at runtime, because `include` is just  regular method call, while superclasses are set in stone as you write your class definitions.  Modules are much easier to use and test in isolation than tightly coupled hierachy of classes.   You can include as many modules as you like, while you can only have one superclass per class. 

Modules can also be applied at the Class level by "extending" within the Class.  This would allows the methods within the module to be accessed by other classes.  This piece of Avi code from Friday's Playlister was what had led me to look into inheritance, modules and mixins a little further to begin with:

<dt>memorable.rb</dt>
	module Memorable
	  module InstanceMethods
	    def initialize
	      self.class.all << self
	    end
	  end

	  module ClassMethods
	    def self.extended(base)
	      base.reset_all
	    end

		  def reset_all
	      @all = [] #still do not quite understand why we don't use @@all here
	    end
		  
		  def count
	      self.all.size
	    end

	    def all
	      @all
	    end
	  end
	end

We see in the partial Artist.rb file below, all the methods in module Findable and ClassMethods specifically in Memorable will be Artist Class methods.  I also noted the use of `super`, whereby Ruby searches upward in the ancestry to find the method `initialize` so that it doesn't need to be written here again.

<dt>artist.rb</dt>
	class Artist
	  attr_accessor :name
	  attr_reader :songs

	  extend Memorable::ClassMethods
	  include Memorable::InstanceMethods #modules

	  extend Findable
	  
	  def initialize
	    super
	    @songs = []
	  end
	[code omitted]

So the primary difference in usage as I try to apply this in my own code.  `include` applies to Class Instance Methods and `extend` when the module is to be extended to other classes instead of being included.  Access to the module method is done through the class instead of the instance.  

This serves as a start in learning about something unique and powerful to Ruby.  From the readings it seems that  other languages handle inheritance very differently (multiple inheritances etc.,).  Furthermore, really cool things happen when we start looking at how, for instance, mixins from Ruby's standard library (eg, Enumerable, Comparable, or Math) can work with code in the class using it. Looking forward to putting some of this into greater practice going forward.


Resources and other interesting posts on inheritance and modules: 
1. http://www.ruby-doc.org/core-1.9.3/Module.html
2. http://www.rubyist.net/~slagell/ruby/modules.html
3. http://ducktypo.blogspot.com/2010/08/why-inheritance-sucks.html
4. http://ruby.about.com/od/beginningruby/a/mixin.htm


