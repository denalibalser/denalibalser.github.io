---
layout: post
title:      "Ruby Variables & Methods"
date:       2019-06-17 02:13:21 +0000
permalink:  ruby_variables_and_methods
---


Ruby variables are crucial for maintaining the readability of our code, an important concept in programming as it is likely your code will be read and often worked on by others. Variables store information that is referenced and manipulated within a program. The naming of a variable is important, it should be descriptive of the information it is representing so that the code can be understood by both yourself and others. Variables, and thus the data that they represent are used throughout programs. 

The equals sign ( = ) is used to assign value to a variable, for example: 

the_variable = "This is the value!"

Above, 'the_variable' is set equal to a string of "This is the value!". Ruby variable names are always in snake case (this_is_snake_case). Now that this variable has been defined, you can reference it: 

the_variable 
=> "This is the value!"

Variables are equal to values in memory, meaning they can be re-assigned, this is important to know when defining variables as if you use the same variable name, the first will no longer point to the original data and instead be updated to the new data. If this is not the intention, remember to use unique variable names! 

Variables have scope, which defines where in a program they are able to be accessed and used. The scope of a variable is determined by where the variable is created. The scope of Ruby variables is defined by a block, which is the code that falls between the **def** and **end** keywords of a method (more on methods later), a variable defined within these keywords is  an inner scope variable, the outer scope for that method is anything outside the method. An *important*  concept to remember is that inner scope **can** access variables created in an outer scope, but not the other way around. SO, a variable defined within a method is not accessible after the **end** keyword, BUT a variable defined outside of the method is accessible within the method. 

In addition, there are several *types* of variables. Constants, global variables, class variables, instance variables, and local variables:

*Constants* are defined with all caps (THE_CONSTANT) and store data that does not need to change. Constants can't be defined in method definitions and are available in all of an application's scopes.

*Global variables* are defined by beginning the variable name with a dollar symbol ($) and are also available in all of an application's scopes. In Ruby, it is good practice to avoid using global variables as they can cause unexpected issues in programs.  

*Class variables* are defined by preceeding the variable name with two @ symbols  and are available to instances of a class and the class itself. These variables need to be defined at the class level, outside of any method definition and are able to be altered through class or instance method definitions. 

*Instance variables* are defined with one @ symbol before their name and are available in the current instance of a parent class. 

*Local variables* are subservient to all scope boundaries, and are defined with nothing preceeding and use snake_case  for  the name. 



Within Ruby we are provided a very useful tool; methods allow us to extract the logic out of an action so that our programs can have greater flexibility in application. Ruby methods are started with the *def* keyword and ended with an *end* keyword, the functionality residing in a *block*  or body between the two. 

For example:

def shout(string)
   string.upcase 
end 

shout('what is going on')
=> "WHAT IS GOING ON"

shout('kevin')
=> "KEVIN"

shout('look at the sunset')
=> "LOOK AT THE SUNSET"

etc. 

While this is a fairly contrived example, you can see how this application would save the programmer time and improve the flexibility of the code when you compare it to the non-method alternative: 

puts "WHAT IS GOING ON"
puts "KEVIN"
puts "LOOK AT THE SUNSET" 

In the above example, we have to puts out each phrase in caps, while with the shout method we are able to use a parameter (the (string) ) by passing an arugment in when we call the method and have it returned in all uppercase thanks to the .upcase method that is called on the parameter within the shout method block. In such, we are able to call the shout method with any number of arguments and have them returned in all uppercase, rather than having to explicitly*puts* them out in uppercase ourselves. 

For background, a **parameter** is used when you want to access data from outside of the method definition's scope (if a variable is defined within the method it is within scope, but if it is not it will return a NameError) by passing it into the method. As a programmer, you can name your parameter whatever you want, but it is good practice to give accurately descriptive and explicit names to parameters etc. In addition, an **argument** is a piece of information that takes the place of the parameter when you are calling the method and is modified by the code within the body of the method.  

So,  in the above example, *(string)* is the parameter and *('what is going on')* is one of the arguments that the *shout* method was called with. 






