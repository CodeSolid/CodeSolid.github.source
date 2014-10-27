---
author: John Lockwood
layout: post
title: "Bash script to switch between scala versions" 
excerpt:  I've found it helpful to be able to switch to different Scala versions, both for testing out my code and for the sake of experimenting with certain libraries that haven't yet been brough current.  Here's a simple bash script that shows how I set this up.
categories:
- Miscellaneous
---

Switching between Scala versions in bash (in my case running on Ubuntu linux) was a pretty easy project even for me as a novice bash programmer,
given the programmer's friend:  Google.

One wrinkle is that environment variables set in a bash script do not affect the global environment, but an easy fix for that was to "source" the script from within two utility aliases I set up, one for each version I wanted to pass to the script:

{% prism bash %}
alias ver10='source ~/bin/scalaver.sh 2.10'
alias ver11='source ~/bin/scalaver.sh 2.11'
{% endprism %}

As you can see, I saved the script to my &lt;user home&gt;/bin directory

Here is the bash script that the alias calls:

{% prism bash %}

#!/bin/bash

function printUsage() {
	echo "Usage scalaver.sh [2.10|2.11]"
	exit 1
}

if [ -z $1  ]; then
	printUsage;
elif [ "$1" = "2.10" ]; then
	export SCALA_HOME=~/apps/scala-2.10.4
	export PATH=$SCALA_HOME/bin:$PATH	
	echo "Scala version is 2.10.4"
	scala -version
elif [ "$1" = "2.11" ]; then
	export SCALA_HOME=~/apps/scala-2.11.2
	export PATH=$SCALA_HOME/bin:$PATH	
	echo "Scala version is 2.11.2"
	scala -version
else
	printUsage;		
fi


{% endprism %}