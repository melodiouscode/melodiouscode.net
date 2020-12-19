---
layout: post
title: Do you fizz buzz, buzz fizz, or just scratch your head?
date: '2018-09-17 17:53:13'
image: /images/posts/rawpixel-567016-unsplash-min.jpg
tags:
- development
---

Over the years I have interviewed a lot of developer candidates and given advice to a fair few potential developers who are looking for their first interviews. Again and again, the FizzBuzz test has cropped up, and I have seen both some fantastic and some not so fantastic answers to the problem. For those who are not aware of what the FizzBuzz test is, here is the standard question:

Write a function which prints all the numbers from 1 to 100. But when printing a number which is a multiple of three print the word "Fizz" instead of the number, when the number is a multiple of five print the word "Buzz". If the number is a multiple of both three and five write the word "FizzBuzz" instead of the number.

FizzBuzz is a simple program, or at least it should be. I think that some people who are new to the industry find it hard because it does not fit into the standard coding styles taught in school/university, it isn't just a simple for loop nor can you just implement an if then else. This is why it can be such a good tool to break the candidates apart from those who can code and those who can problem solve; that being said it only really works for the earlier stages of someone's development career (although if a senior developer couldn't solve this problem then they may need to seek alternative employment).

# "So how do I FizzBuzz?"

## Break it down

It really is simple when you think about it, just break it down in to its constituent requirements.

### Print all the numbers from 1 to 100

Simple, just loop all the numbers and write them to the console.

<!--kg-card-begin: markdown-->

    using System;
    public class Program {
    	public static void Main() {
    		for(int x = 1; x <= 100; x++) {
    			Console.WriteLine(x);	
    		}
    	}
    }

<!--kg-card-end: markdown-->
### What about three?

Loop all the numbers as we did above, and test them to see if they are divisible by three.

<!--kg-card-begin: markdown-->

    using System;			
    public class Program {
    	public static void Main() {
    		for (int x = 1; x <= 100; x++) {
    			if (x % 3 == 0) {
    				Console.WriteLine("Fizz");
    			} else {
    				Console.WriteLine(x);
    			}
    		}
    		
    	}
    }

<!--kg-card-end: markdown-->
### Add in five to the mix

Again we just loop all the numbers but throw in the second test.

<!--kg-card-begin: markdown-->

    using System;
    					
    public class Program {
         public static void Main() {
             for (int x = 1; x <= 100; x++) {
                 if (x % 3 == 0) {
                     Console.WriteLine("Fizz");
                 } else if (x % 5 == 0) {
                     Console.WriteLine("Buzz");
                 } else {
                     Console.WriteLine(x);
                 }
             }
         }
    }

<!--kg-card-end: markdown-->
### And finally both three and five

Not hard when you look at it written, a simple if-else-if-else-if-else! But is there another way? Of course, especially if you want to set yourself apart from the crowd.

<!--kg-card-begin: markdown-->

    using System;
    
    public class Program {
    	public static void Main() {
    		for (int x = 1; x <= 100; x++) {
    			if (x % 3 == 0 && x % 5 == 0) {
    				Console.WriteLine("FizzBuzz");
    			} else if (x % 3 == 0) {
    				Console.WriteLine("Fizz");
    			} else if (x % 5 == 0) {
    				Console.WriteLine("Buzz");
    			} else {
    				Console.WriteLine(x);
    			}
    		}
    	}
    }

<!--kg-card-end: markdown-->
### Linq-ing it up a little

When it comes down to it FizzBuzz isn't a very hard challenge, but it can throw off some candidates especially if they have to write it by hand rather than in an IDE!

<!--kg-card-begin: markdown-->

    using System;
    using System.Linq;
    					
    public class Program
    {
    	public static void Main() {
    		Enumerable.Range(1,100).Select(
                            n => 
                            (n % 15 == 0) ? "FizzBuzz" : 
                            (n % 3 == 0) ? "Fizz" : 
                            (n % 5 == 0) ? "Buzz" : 
                            n.ToString())
                            .ToList()
                            .ForEach(Console.WriteLine);
    	}
    }

<!--kg-card-end: markdown-->