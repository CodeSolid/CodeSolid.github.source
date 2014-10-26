---
author: John Lockwood
layout: post
title: "Shutting Off Social Networks on Linux" 
excerpt:  Social networks are wasting your life?  Here's a quick fix.

categories:
- Miscellaneous
---

Are you tired of how social networks suck up your life and make you feel like you've somehow managed to avoid Vonnegut's dictum that all of life is like high school by turning your life into something that's really a lot more like middle school?

I know I am.

So in case you're wondering how to move on with your life, here's a simple way to accomplish that in Linux.

{% prism bash %}
cd /etc
sudo cp hosts hosts.backup
sudo <youreditor> hosts
{% endprism %}

Then add three lines to the end.

{% prism bash %}
# Customizations
127.0.0.1 	twitter.com
127.0.0.1   facebook.com
127.0.0.1   linkedin.com
{% endprism %}

Save the file, re-start your browser, and you're done.

Now go enjoy your life.