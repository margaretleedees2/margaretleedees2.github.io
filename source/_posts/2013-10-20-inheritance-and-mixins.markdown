---
layout: post
title: "inheritance-and-mixins"
date: 2013-10-20 18:24
comments: true
categories: 
---

At the end of last week, we discussed inheritance and modules.

If Classes help us from being redunant by making certain methods available to all instances of that class, then inheritance seems to build on that notion of "sharing" by allowing a Class to make available all its capabilities to a sub-class which can include further specificity and additional methods.  

When I looked it up, many referenced certain taxonomies when explaining it (eg., www.rubist.net/~slagell/ruby/inheritance.html)

For instance, the plant kingdom has characteristics that are true to all kinds of plants including things like they are cellular, convert energy from sunlight to food, can propogate etc.

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

This brings us to Modules and Mixins.  Modules are, according to Ruby docs [ruby-doc.org/core-2.0.0/Module.html], a collection of methods and constants.  They are another way that functionality can be "shared" between classes. Module functions are able to be included or "mixed in" within a Class. 


Modules can either be instance methods or module methods.  When we "include" modules in a class, instance methods appear as methods in a class.  When we "extend"


