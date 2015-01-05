---
layout: post
title:  "Welcome to Jekyll!"
date:   2014-12-31 08:50:24
category: python
---
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight python %}
def print_hi(name)
from django.db import models

# Create your models here.

class Categories(models.Model):
    name = models.CharField(max_length=100)

    def __unicode__(self):
        return self.name

class Product(models.Model):
    transmission_choice = (
        ('automatic', 'automatic'),
        ('manual', 'manual'),
    )


    category = models.ForeignKey(Categories)
    name = models.CharField(max_length=100)
    price = models.FloatField()
    passenger = models.IntegerField()
    luggage = models.CharField(max_length=100)
    transmission = models.CharField(max_length=10, choices=transmission_choice)
    ac = models.BooleanField(default=True)
    average = models.FloatField()
    booked = models.BooleanField(default=False)

    def __unicode__(self):
        return self.name

class Extras(models.Model):
    name = models.CharField(max_length=100)
    price = models.FloatField()

    def __unicode__(self):
        return '%s for rs %s'%(self.name, self.price)
{% endhighlight %}


{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    
</body>
</html>
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
