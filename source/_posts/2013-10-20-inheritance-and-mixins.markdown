---
layout: post
title: "inheritance-and-mixins"
date: 2013-10-20 18:24
comments: true
categories: 
---

At the end of last week, we discussed inheritance and modules.  I needed to go over it again as not all of it sunk in during lecture-runtime.  So here goes:

If classes save us from being redunant by making certain methods available to all instances of that class, then inheritance seems to build on that notion of "sharing" in that it allow a Class to make its capabilities available to a sub-class(es) which can then include further specificity and additional methods.  

When I looked it up, many used taxonomies to [explain] (http://www.rubist.net/~slagell/ruby/inheritance.html).

So instead of mammals and fish, lets use plants.  The plant kingdom has characteristics that are true for all things defined as plants including properties like they are cellular, convert energy from sunlight to food, can propogate etc.

There are two primary subclasses of plants: seed-bearing and spore-bearing. Both subclasses possess plant kingdom characteristics (cellular, absorb sunlight) but also possess additional specifics such as being able to have flowers, being able to either absorb water or circulate fluids throughout itself or be of a certain sex or be asexual.  

So in Ruby:

	class Plant
	end

	class Rose <Plant
	end

	class Algae < Plant
	end


The Rose class and Algae class are "Child" classes that inherit (denoted by <) all characteristics of the "Parent" class Plant. But they have further specificity:

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


A Rose and Moss are a type of plant but also have their own specialized things they can do.  Its important to note that a Class can only inherit features from one other class.

This brings us to Modules and Mixins.  Modules are, according to Ruby docs [ruby-doc.org/core-2.0.0/Module.html], a collection of methods and constants.  They are another way that functionality can be "shared" between classes. I liked the following description[ruby.about.com/od/beginningruby/a/mixin.htm]

It says that mixins are a group of methods not yet attached to any class.  They exist in a module and are not useful until included in a class.  Once included they are now normal methods of a class.

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


Methods within a module can either be ins tance methods or module methods.  In the example above, the module is included (via "include") in within a class, thus the module's methods are "mixed in" as instance methods and apply to all instances of the Rose and Moss classes. 

Why is this better?

This person explains it nicely [dycktypo.blogspot.com/2010/08/why-inheritance-sucks.html]  
	
	Modules are generally more flexible than superclasses.  Modules can be managed at runtime, because include is just  regular method call, while superclasses are set in stone as you write your class definitions.  Modules are much easier to use and test in isolation than tightly coupled hierachy of classes.   You can include as many modules as you like, while you can only have one superclass per class. 

Modules can also be applied at the Class level by adding "extend Plant" within the Moss and Rose Classes.  This would allows the module 


