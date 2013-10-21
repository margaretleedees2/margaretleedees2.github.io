---
layout: post
title: "inheritance-and-mixins"
date: 2013-10-20 18:24
comments: true
categories: 
---

Had a discussion about Inheritance in class the other day and this is my exploration of it.

From what I can tell, classes help us from being redunant by making certain methods available to all instances of that class.  

Inheritance seems to build on this notion of "sharing code" by allowing a Class to make available its capabilities to a sub-class which can include further specificity and methods.  

It helped me to think in terms of taxonomy.

The plant kingdom have characteristics that are true to all kinds of plants such as they are cellualur, convert energy from sunlight to food etc.

There are two primary subclasses of plants: seed-bearing and spore-bearing. Both subclasses possess plant kingdom characteristics (cellular, absorb sunlight) but also possess additional specifics such as ability to circulate fluids through their bodies or absorb via moisture surrounding them.  

In Ruby:

class Plant
end

class Rose <Plant
end

class Algae < Plant
end


The Rose class and Algae class are "Child" classes that inherit (denoted by <) all characteristics of the "Parent" class Plant.  

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


A Rose and Moss are a type of plant but also have their own specialized things they can do.

This brings us to Modules and Mixins.

Modules are another way that functionality can be "shared" between classes.  The difference here is that modules are not Classes and therefore do not have instances.  Module functions are able to be included or "mixed in" within a Class, however.

In our example from above:

module 



We saw this in the Playlister code we reviewed Friday.
