---
layout: post
title: "inheritance-and-mixins"
date: 2013-10-20 18:24
comments: true
categories: 
---

Have been learning more about Ruby and wanted to understand better how interitance (and mixins) works.

The way I understand it, Classes help us make certain methods available to all instances of that class.  That ability to "share" methods prevents us from having to repeat those same methods over and over thus making our code more succinct.

Inheritance allows us to have a Class with all its capabilities but then create specialized classes of that Class that automatically have all those capabilities and then some.  The original class is called the "Parent" class and the specialized class or classes are its "Child" classes.

So,

	class Parent
	end

	class Child < Parent
	end

The < indicates child inherits 





 	def 
		puts "#{self} loves Kathleen Battle "
	end

	def establish_habit
		puts "#{self.name} laughs inappropriately during sad times"
	end



When we need to convert an object to a string, we call to_s method on the object

But we've also written classes that don't explicity implement to_s.

These Classes respond successfully when we call to_s on them.

This has to do with inheritance, subclassing, and how Ruby determines which method to run when you send a message to an object


Original = Superclass/Parent
Next class = Subclass/Child

Child inherits all of the capabilities of its parent class. 

All parent's instance methods are available in instances of the child

######EXAMPLE HERE######

While the child class defines no methods, when we create an instance of it, the child inherits all the methods of its parents.  Ruby goes all the way through its ancestors until it runs out of classes

This explains why to_s is available to every object.  Rub is 






