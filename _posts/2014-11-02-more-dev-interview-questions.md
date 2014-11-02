---
layout: post
title: "More Ruby on Rails Dev Interview Questions"
description: ""
category: 
tags: [RoR, Interviews, OOP]
---
{% include JB/setup %}

On Friday I had a three hour technical interview with a local startup. I knew that as a novice developer, I'd probably be in over my head. It was a tough but interesting and equally fun experience. Here's what I was asked about.

Define:

**SQL Injection**: (SQLi) is any situation in which a user can manipulate a database query in an unintended manner. Consequences of SQL injection vulnerabilites range from data leaks, to authentication bypass, to root access on a database server. In short, it is a very big deal.

Here is an example of using exists? to determine if a given user exists (per [this blog post](http://blog.presidentbeef.com/blog/2013/02/08/avoid-sql-injection-in-rails/)):

{% highlight Ruby %}
User.exists? params[:user_id]
{% endhighlight %}

This looks harmless, since params[:user_id] is a string, and strings will be sanitized. In fact, the documentation clearly points out not to pass in conditions as strings, because they will be escaped.

However, there is no gaurantee params[:user_id] is a string. An attacker could send a request with ?user_id[]=some_attack_string, which Rails will turn into an array ["some_attack_string"]. Now the argument is an array, the first element of which is not escaped.

To avoid this problem, the user input should be converted to the expected type:

{% highlight Ruby %}
User.exists? params[:user_id].to_i
{% endhighlight %}

Or use a hash:
{% highlight Ruby %}
User.exists? :id => params[:user_id]
{% endhighlight %}

**Include vs. <**:
Include is used in the model to call methods from a module that is defined somewhere else (like a service object). This looks as follows:

{% highlight Ruby %}
class Customer < ActiveRecord::Base
  include Foo
end
{% endhighlight %}

(Inheritance)[http://rubylearning.com/satishtalim/ruby_inheritance.html] (denoted with <) is a relation between two classes. We know that all cats are mammals, and all mammals are animals. The benefit of inheritance is that classes lower down the hierarchy get the features of those higher up, but can also add specific features of their own. If all mammals breathe, then all cats breathe. In Ruby, a class can only inherit from a single other class. Some other languages support multiple inheritance, a feature that allows classes to inherit features from multiple classes, but Ruby doesn't support this.

Might look like this:

{% highlight Ruby linenos %}
class Mammal  
  def breathe  
    puts "inhale and exhale"  
  end  
end  
  
class Cat < Mammal  
  def speak  
    puts "Meow"  
  end  
end  
  
rani = Cat.new  
rani.breathe  
rani.speak  
{% endhighlight %}

**Recursion**: A recursive function/method calls itself within its definition. For a recursive algorithm to terminate you need a base case (e.g. a condition where the function does not call itself recursively) and you also need to make sure that you get closer to that base case in each recursive call. 

After being asked to define these terms, I then had to use a whiteboard to write solutions to a few programming questions.

**Define a method that will take two arguments and return the result of the first divided by the second, without using the division operator**: My solution was much simpler and used a while loop to subtract the second arg from the first, and track how many times it could do so before reaching zero. This wouldn't work in all cases. Here's a solution from StackOverflow:

{% highlight Ruby linenos %}
unsigned divide(unsigned dividend, unsigned divisor) { 

    unsigned denom=divisor;
    unsigned current = 1;
    unsigned answer=0;

    if ( denom > dividend) 
        return 0;

    if ( denom == dividend)
        return 1;

    while (denom <= dividend) {
        denom <<= 1;
        current <<= 1;
    }

    denom >>= 1;
    current >>= 1;

    while (current!=0) {
        if ( dividend >= denom) {
            dividend -= denom;
            answer |= current;
        }
        current >>= 1;
        denom >>= 1;
    }    
    return answer;
}
{% endhighlight %}

**Define a method that will take one argument and then return the Fibonacci Sequence at that position. So if you pass in the number 4, it will return the 3 (1,1,2,3...)**:

{% highlight Ruby linenos %}
def fibonacci( n )
  return  n  if ( 0..1 ).include? n
  ( fibonacci( n - 1 ) + fibonacci( n - 2 ) )
end
puts fibonacci( 5 )
{% endhighlight %}

**Build a basic rails blog within an hour**: Plenty of good tutorials online if you'd know how to do this already. [This one is quick and easy](https://www.reinteractive.net/posts/32-ruby-on-rails-3-2-blog-in-15-minutes-step-by-step) and paired with the [bootstrap generator gem](https://github.com/decioferreira/bootstrap-generators) will look decent as well.