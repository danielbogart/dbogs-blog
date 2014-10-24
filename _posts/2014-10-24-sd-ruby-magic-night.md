---
layout: post
title: "SD Ruby Magic Night"
description: ""
category: 
tags: [SD Ruby, Meetups, RoR]
---
{% include JB/setup %}

Last night I attended the [SD Ruby](http://www.meetup.com/sdruby/) "Magic Night" (no, not the Cris Angel type of magic). These events are essentially hack nights revolving around one challenge. The 20 or so people who showed up at the MonkDev offices in Old Town San Diego were broken up into groups of 4 based on skill level, plied with pizza and beer, and set to work to solve the challenge in two hours. Super fun, and way educational for us Ruby newbies. 

Last night's challenge was to create a photo cropping tool. We could use a command line interface, pure Ruby, or RoR. Gems were fair game. My team consisted of one veteran Rubyist, a GO/JS guy, myself, and a dude completely new to Ruby. We projected my laptop screen onto a TV in the office lounge area, and got to it. Thinking out the plan, we decided to make things as simple as possible by using the topically named [MiniMagick image gem](https://github.com/minimagick/minimagick) that acts as a nice wrapper for ImageMagick. 

Our next order of business was creating a new rails app, adding the handy [Bootstrap Generator](https://github.com/decioferreira/bootstrap-generators) gem, and generating a scaffold for our image_file model. This was a huge time saver - it created the model, controller with CRUD operations, and approriate views immediately. Also, everything is wrapped in Bootstrap styling. From there, we could start using some of our gem's magick to play with the uploaded image. 

MiniMagick is super easy to use, and once we figured out how to grab the temporary image file:

	image = MiniMagick::Image.open(image_file_params[:png_file].tempfile.path)  

we could then easily manipulate the image with methods like .resize or .crop. Using .crop, we realized we'd need to add offset fields to choose where to start the crop. After adding those fields, we had a little bit of time left, and had our JS expert add some nice jQuery to allow us to actually click and drag across the image exactly where we wanted to crop:

	<script>

		$(document).ready(function(){

			var left, right, top, bottom;
			var $img = $('img');

			// Offset
			var offset = $img.offset();

			$img.on('mousedown', function(event){

				event.preventDefault();

				left = event.pageX;
				top = event.pageY;
				
				$(this).on('mouseup', function(event){
					right = event.pageX;
					bottom = event.pageY;
				
					// Set end result
					var newTop = Math.ceil(top - offset.top);
					var newLeft = Math.ceil(left - offset.left);
					var width = Math.ceil(right - left);
					var height = Math.ceil(bottom - top);


					$('#image_file_width_offset').val(newLeft);
					$('#image_file_height_offset').val(newTop);
					$('#image_file_width').val(width);
					$('#image_file_height').val(height);
				});
			});


		});

	</script>

An interesting hangup we ran into was initially when trying to click and drag on the image would cause the user to actually drag the entire image off the page. We finally figured out that using event.preventDefault(); would prevent this action, and allow us to drag as needed. Our result worked, and looked half decent doing it. I had an awesome time, met some great people, and learned plenty along the way.