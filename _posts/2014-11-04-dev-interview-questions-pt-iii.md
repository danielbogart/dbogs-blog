---
layout: post
title: "Dev Interview Questions Pt. III"
description: ""
category: 
tags: [JavaScript, Interviews, OOP]
---
{% include JB/setup %}

WOO MORE INTERVIEW QUESTIONS. I found this set of questions from a recent front-end dev interview relevant and interesting. Check it:

**General questions**

Tell me about your preferred development environment and tools used in workflow.

* I use Sublime Text 3 with a few plugins such as Emmet for efficiency. I work on a Macbook Air running Mavericks and planning to upgrade to Yosemite shortly. I like Balsamiq for mockups, Github for code repo, homebrew for installations, PSQL app for backend, and terminal for navigation.

If you could master one technology in the next 12-months, what would it be?

* AngularJS. That Angular is so hot right now.

How do you optimize the loading of client-side assets in the browser?

* You can merge multiple Javascripts into one, compress JavaScript and CSS with tools like CleanCSS and jcompress, and customize header expiry and caching. I’ve also seen load speed improvements with Turbolinks.

What's your favorite feature of internet explorer?

* Trick question? The last time I was forced to use IE extensively was probably in my high school’s library. That said, it sounds like IE 9 has some major improvements such as individual process tabs, improved security, and add-on speed impact analytics.

What did you learn this week? Show me some code.

I learned more about Service Objects and Concerns in Ruby on Rails - two ways of ensuring modular, easily testable code and avoiding ‘Fat’ and convoluted controllers. I also learned about recursive functions in Ruby. For example, you could write a method to return a certain position in the Fibonacci sequence like so:

{% highlight Ruby linenos %}
def fibonacci( n )
   return  n  if ( 0..1 ).include? n
   ( fibonacci( n - 1 ) + fibonacci( n - 2 ) )
end
puts fibonacci( 5 )
{% endhighlight %}

Tell me about your style of 'engineering discipline'
Style guides followed, documentation practices.

* I find that my styling generally follows the guidelines set forth by Google for HTML/CSS/JS (http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml/, http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
UTF-8 encoding, HTML5, frequent checks for valid HTML, ID for single references, class otherwise etc.

Tabs vs. spaces?

* I prefer tabs, mainly because it is a separate key only used for indentation. It’s impossible to ‘half’ indent something with tab, and it’s generally easy to spot where indentation is off. Whatever is used on a project I always ensure consistency throughout.

camelCaseVar = 0; vs. snake_case_var = 0;?

* My understanding is that the convention for JS is camel case, but again, consistency is key.

'some string' or "some string"?

* No preference, although again I try to maintain consistency throughout the project. If a string needs to return double quotes, I’ll wrap with single quotes (‘Returns “What’s up?”').

Do you use grunt, bower or other scaffolding/front-end package management/development tools?

* I don’t, but I would be interested to learn them.

**Basic front-end engineering questions**

What does the DRY principle mean to you in practice?

* Don’t repeat yourself - in other words, avoid repetitious code by writing functions/methods, and using blocks, loops, etc.

Bonus if you can show me an example in code you have written/a gist.

* https://gist.github.com/danielbogart/8d9a1828d3cb710a5c94

In js, what is the difference between == and ===?

* === is a strict comparison operator, that takes the type of variable being compared into account. For example, 0 === False returns false, but 0 == False returns true. When using the == operator, JS handles type conversion and returns the value based on the content.

In js, provide an example of a ternary expression.

* "The fee is " + (isMember ? "$2.00" : "$10.00")

What are the benefits of building an application using a RESTful architecture?

* Doesn’t require the client to know anything about the structure of the API - it’s completely disconnected and modular
* Server provides whatever information requested or needed to interact with the page
* POST, GET, DELETE and PUT requests are all that is needed to send to a URL to commit an action
* With the myriad programming languages available today, the modularity of REST ensures that a single API can be extended to web and mobile with several different languages on top.

Bonus: Disadvantages?

* Requires callbacks/HTTP requests which means page reloads, and difficulty presenting real-time data.

What is the difference between WebSockets, long-polling and ajax?

* WebSocket enables two-way communication between a client and remote host. Leaving the pipe open rather than requiring HTTP requests allows for real-time communication and notifications like the Facebook or Gmail notifications that you get without refreshing the page. Not great for complex calculations that may clog the pipe. 
* Long-polling ensures the server doesn’t immediately respond with the requested information but waits until there’s new information available. Once there is new info, server sends it to the client. The client then receives the info, and immediately sends another request, re-starting the process.
* AJAX (asynchronous javascript and XML) allows for background requests to be sent to the server and displayed to the client without a page reload.  Can create additional complexity and renders the back/forward buttons on the browser useless.

**Practical exam**

Provide answers to **at least one* the following in a github repo or gist:*

Make the following work in javascript (or python/ruby):
wordToLetterpairs('The Quick Fox');
output: ['Th', 'he', 'e ', ' Q', 'Qu', 'ui', 'ic', 'ck', 'k ', ' F', 'Fo', 'ox']

{% highlight JavaScript linenos %}
var wordToLetterPairs = function(sentence) {
	
	var pairs = [];
	var x = 0;
	var y = 2;

	while (x < (sentence.length-1)) {
		pairs.push(sentence.substring(x,y));
		y++;
		x++;
	};

	return pairs;
};

console.log(wordToLetterPairs('The Quick Fox'));
{% endhighlight %}