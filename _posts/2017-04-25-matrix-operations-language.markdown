---
layout: post
title:  "Morphinity - A Language for Matrix Operations"
date:   2017-04-25 
categories: jekyll update
---
[Abby Atchison](http://www1.chapman.edu/~atchi102/), [Austin Ayers](), and [Josh Graves](http://www1.chapman.edu/~grave121/) are contributors on this project.  

Defining a matrix in most programming languages is often ugly and counter intuative. Few languages offer built in support for matrix operations. Thus we propose a langauge spcefically for matrix operations. 



{% highlight java %}
{% raw %}
// declaring 3x3 matrix in Java  
int matrix[][] = {{50,60,55},{62,65,70},{72,66,77}};
{% endraw %}
{% endhighlight %}

{% highlight c++ %}
{% raw %}
// declaring 3x3 matrix in C++  
int matrix[3][3] = {{50,60,55},{62,65,70},{72,66,77}};
{% endraw %}
{% endhighlight %}  

{% highlight python %}
# declaring 3x3 matrix in Python
matrix = [[1,2,3],[4,5,6],[7,8,9]]
{% endhighlight %}  

{% highlight morphinity %}
{% raw %}
// declaring 3x3 matrix in Morphinity  
A=
1 2 3 
4 5 6
7 8 9
// declaring 3x1 matrix
B= 
2
1 
3

C = A x B
{% endraw %}
{% endhighlight %} 

{% comment %}
need for this lang
grammar 
parse tree
assignments, java
demonstration
{% endcomment %}
