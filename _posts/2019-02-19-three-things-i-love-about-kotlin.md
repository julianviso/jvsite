---
title: "Three Things I Love About Kotlin"
author: Julian Viso
layout: post
tags: [blog]
---

Let's get one thing straight right away. Kotlin is a really nice language to write code in!

It's mid-summer of 2018. At work I had just been swapped to a new team (actually a team I was a part of back in 2016). Up until now in my short career I had focused mostly on front-end development. For some time however, I had wanted to start working more on backend development to improve as a software engineer. Coincidentally (not really, I had already heard of it before moving to this team) the team I am to this day a part of was planning to update their entire backend API from a dated Grails app to something modern and there was going to be lots of opportunities to get my feet wet with backend development!

Groovy at this point is becoming a dying a langauge, and our team was looking for what language to re-write our entire backend in that supports Spring 3.0. Java? Groovy? Kotlin?!? As a team we decided that Groovy was not worth using, and let's be real, Java is too wordy. Enter Kotlin...

Around Fall of 2018 I finally started to get my feet wet with Kotlin. After a couple of months of coding in Kotlin I am by no means an expert in the language, but I have quickly grown to love it! Kotlin was created by JetBrains, and runs on the JVM. This means that Kotlin can be easily integrated with Java code out there and will compile just fine! Let's discuss some basics about Kotlin that differentiate it as well as some features that I personally love. 

### Strong Null Checks
The first thing you'll notice about Kotlin is that there are strong null checks. A variable cannot be null by default unless specified with the ? operator. Kotlin forces you to watch out for null pointer exceptions. Say goodbye to all those try/catch blocks!

```
var example: MyClass = MyClass() 
example = null // Will fail to compile

var workingExample: MyClass? = MyClass()
var workingExample = null //will compile

```

Variables can be set using var or val, with var being modifiable while val isn't. Ok, this really isn't something that I love or hate but I just wanted to point out real quick.

```
    val a: String = "julian" // val is immutable
    var b: Int = 8 // var is modifiable
```

### When
Ok, back to actual things I love about Kotlin, there's when. We've all used switch statements before. Kotlin has their own version of Switch which is way more readable and I now try to incorporate it perhaps too much these days. There are tons of ways you can use when but here are two examples showing it.

```
val user: Boolean = when {
    user == null -> false
    user is "julian" -> true
    else -> user = "lost"
}

when (x) {
    in 1..10 -> print("x in range")
    in validRange -> print("x is valid")
    else -> print("x invalid")
}
```


### Data Classes
In Kotlin, we can avoid writing a lot of boilerplate code. A data class encapsulates all the functionality of your typical objects which do nothing but store data. Better shown, let's first look at a Java movie class below.

```
public class Movie {
    private String name;
    private String director;

    public Movie(String name, String director) {
        this.name = name;
        this.director = director;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getDirector() {
        return director;
    }

    public void setDirector(String director) {
        this.director = director;
    }

    // Purposely leaving these empty, yes deal with it
    @Override
    public String toString(){}

    @Override
    public Boolean equals(Object o){}

    @Override
    public Int hashCode() {}
}
```

Just writing that was enough to make me lazy halfway through creating a simple class that stores 2 fields of data for a movie. Luckily, in Kotlin we can do this all in a single line!

```
data class Movie(val name: String, val director: String)    
```

That's literally it! With this Kotlin will generate the rest for us. We also get a copy() for free alongside toString(), equals(), and hashCode().
