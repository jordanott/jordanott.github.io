---
layout: post
title:  "Morphinity - A Language for Matrix Operations"
date:   2017-04-25
categories: jekyll update
---
[Abby Atchison](http://www1.chapman.edu/~atchi102/), [Austin Ayers](), and [Josh Graves](http://www1.chapman.edu/~grave121/) are contributors on this project. All the code is available [here](https://github.com/jordanott/Morphinity).

Defining a matrix in most programming languages is often ugly and counterintuitive. Few languages offer built in support for matrix operations. Thus we propose a langauge spcefically for matrices.  

{% highlight java %}
{% raw %}
// declaring 3x3 matrix in Java  
int matrix[][] = {{50,60,55},{62,65,70},{72,66,77}};

// declaring 3x3 matrix in C++  
int matrix[3][3] = {{50,60,55},{62,65,70},{72,66,77}};

// declaring 3x3 matrix in Python
matrix = [[1,2,3],[4,5,6],[7,8,9]]
{% endraw %}
{% endhighlight %}  

Writing your own compiler can be very tedious and time consuming. To make this process easier we used [Antlr](http://www.antlr.org/). Antlr is a *powerful parser generator for reading, processing, executing, or translating structured text or binary files.*

The first step in creating your own programming language is to create a grammar for that language. Most programming languages are defined using [Backus-Naur Form](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form) (BNF).

{% highlight java %}
{% raw %}
grammar morphinity;
program : statement+ ;
statement : assign | operation | print;

assign : ID equals (newline matrix | ID newline);
matrix : (row newline)+ ;
row : (NUMBER space)+ NUMBER;
operation : ID equals (ID expr ID | NUMBER expr ID | ID expr NUMBER) newline;
print: 'print ' ID newline;

equals: '=';
expr : '+' | '-' | '.' | '*';
newline : '\n';
space : ' ';
ID : [a-z]+;
NUMBER: [0-9]+;
{% endraw %}
{% endhighlight %}  

Here is an example of Morphinity syntax, with the corresponding parse tree.   
{% highlight morphinity %}
{% raw %}
a=
1 2 3
4 5 6
b=
2 3 4
5 6 7
c=a+b
{% endraw %}
{% endhighlight %}
![Something]({{ site.url }}/assets/antlr4_parse_tree.png)  

Now we add the functionality to our language by creating a listener that navigates the parse tree. See [listener file](https://github.com/jordanott/Morphinity/blob/master/MyListener.java). 
