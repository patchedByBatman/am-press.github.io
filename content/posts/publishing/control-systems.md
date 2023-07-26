---
title: "Control Systems Book"
summary: Announcement of upcoming book
date: 2022-08-19
series: ["Publishing"]
weight: 1
tags: ["Book", "Control"]
author: "Pantelis Sopasakis"
---



Applied Mathematix Press proudly presents the textbook “Control Systems: An introduction” by Dr Pantelis Sopasakis.

<img alt="Control Systems Front Cover" src="/book-jacket.jpg" style="width: 35%; margin-left: auto;margin-right: auto;">


<a href="https://www.amazon.co.uk/dp/173913866X" title="Buy from Amazon"><img alt="Buy from Amazon" src="/amazon-buy-now-button.png" style="width: 20%; margin-left: auto;margin-right: auto;"></a>

<p style="text-align:center"><span style="color:#cc0000;font-size: 30px;font-weight:bold"><b>Summer discount: <s>£42.00</s> £29.99</b></span></p>
<p style="text-align:center;font-weight:bold">Until the 10th of September</p>
<p id="demo" style="text-align:center;font-weight:bold;font-size: 25px;"></p>



<script>
// Set the date we're counting down to
var countDownDate = new Date("Sep 10, 2023 23:59:59").getTime();

// Update the count down every 1 second
var x = setInterval(function() {

  // Get today's date and time
  var now = new Date().getTime();
    
  // Find the distance between now and the count down date
  var distance = countDownDate - now;
    
  // Time calculations for days, hours, minutes and seconds
  var days = Math.floor(distance / (1000 * 60 * 60 * 24));
  var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
  var seconds = Math.floor((distance % (1000 * 60)) / 1000);
    
  // Output the result in an element with id="demo"
  document.getElementById("demo").innerHTML = "The offer expires in " 
  + days + "d " 
  + hours + "h "
  + minutes + "m "
  + seconds + "s";
    
  // If the count down is over, write some text 
  if (distance < 0) {
    clearInterval(x);
    document.getElementById("demo").innerHTML = "EXPIRED";
  }
}, 1000);
</script>

This book’s objective is to equip the students of engineering schools with the necessary theoretical tools and practical skills (including programming) to analyse dynamical systems and design appropriate controllers.

The book starts with an introductory chapter on modelling of physical systems, gives a brief presentation of linearisation, and moves on to the frequency domain with the introduction of the Laplace transform and its inverse. This brings us to the concept of a transfer function, which is a notion of central importance in classical control theory. We give the definition of BIBO stability and state the Routh-Hurwitz criterion. We then move to the frequency domain: we discuss the properties of the steady state frequency response of the system and state the Bode stability criterion and conclude with the powerful Nyquist criterion.

The theory is presented in a rigorous, yet accessible way, while numerous examples with illustrations help the reader to solidify their understanding and avoid common pitfalls and caveats.

## Clearly stated results

All results are clearly stated and, with few exceptions, are accompanied by step-by-step proofs.

<img alt="Exercise from book" src="/final-value-theorem.png" style="width: 90%; margin-left: auto;margin-right: auto;"><br/>


## Numerous worked-out examples

Each piece of theory is followed by plenty of worked-out examples with figures and detailed derivations and discussion of the results

Each piece of theory is followed by plenty of worked-out examples with figures and detailed derivations and discussion of the results<br/>

<img alt="Exercise from book" src="https://am-press.github.io/ControlSystemsBook/images/examples.png" style="width: 90%; margin-left: auto;margin-right: auto;"><br/>

## Hundreds of exercises with hints and answers

The book counts over 280 exercises, the majority of which are accompanied by short answers and/or hints. In fact, the answers are written at the end of the exercise, but upside down.<br/>

<img alt="Exercise from book" src="https://am-press.github.io/ControlSystemsBook/images/exercises.png" style="width: 80%; margin-left: auto;margin-right: auto;"><br/>

## Over 250 high-quality figures
High-quality illustrations help the reader understand the concepts easier and deeper.<br/>

<img alt="Image from book" src="https://am-press.github.io/ControlSystemsBook/images/book-images.png" style="width: 90%; margin-left: auto;margin-right: auto;">

## Code snippets in Python and MATLAB

Code in snippets in both Python and MATLAB so that you can experiment with controller design yourself and get valuable hands-on experience.


<img alt="Image from book" src="https://am-press.github.io/ControlSystemsBook/images/python-matlab-2.png" style="width: 90%; margin-left: auto;margin-right: auto;">



## Ace your control exams

Ideal for students who want to understand the topic thoroughly and in depth, avoid common pitfalls, and ace their control exams!

## Bibliographic references with comments

Bibliographic references with comments.


## Buy from Amazon

The paperback version of the book in available on Amazon 
([.com](https://www.amazon.com/dp/173913866X), [UK](https://www.amazon.co.uk/dp/173913866X), [Canada](https://www.amazon.ca/dp/173913866X), [Germany](https://www.amazon.de/dp/173913866X), [Italy](https://www.amazon.it/dp/173913866X), [France](https://www.amazon.fr/dp/173913866X), [Spain](https://www.amazon.es/dp/173913866X), [The Netherlands](https://www.amazon.nl/dp/173913866X), [Poland](https://www.amazon.pl/dp/173913866X), [Sweden](https://www.amazon.se/dp/173913866X), and [Australia](https://www.amazon.com.au/dp/173913866X)).

<a href="https://www.amazon.co.uk/dp/173913866X" title="Buy from Amazon"><img alt="Buy from Amazon" src="/amazon-buy-now-button.png" style="width: 35%; margin-left: auto;margin-right: auto;"></a>


## About the author

Pantelis Sopasakis was born in Athens, Greece, in 1985. He received a diploma (MEng) in chemical engineering in 2007 and an MSc with honours in applied mathematics in 2009 from the National Technical University of Athens. In 2012, he defended his PhD thesis entitled "Modelling and control of biological and physiological systems" at the School of Chemical Engineering, NTU Athens. He held postdoctoral positions at IMT Lucca, KU Leuven and University of Cyprus. Since 2019 he joined the School of Electronics, Electrical Engineering and Computer Science (EEECS) and the i-AMS research centre at Queen's University Belfast. His research interests revolve around model predictive control for uncertain systems and numerical optimisation methods and algorithms for large-scale problems. In 2020, Dr Sopasakis was a runner-up for the QUB Teaching Excellence Award.

