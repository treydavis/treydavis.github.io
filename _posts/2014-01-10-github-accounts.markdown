---
layout: post
title:  "Managing multiple GitHub accounts"
date:   2014-01-10
categories: jekyll update
---

I created a new GitHub account for my wife and I to use for research purposes. (You can keep up with our work here: [mcgeedavis.github.io][ourblog]). I pushed to our blog repository without any setup (still not sure how that was possible), but when I tried to push to this blog's repository, I ran into trouble. This is what I encountered when I used `git push`:

{% highlight text %}
remote: Permission to treydavis/treydavis.github.io.git denied to mcgeedavis.
fatal: unable to access 'https://github.com/treydavis/treydavis.github.io.git/': The requested URL returned error: 403
{% endhighlight %}

GitHub was refusing the `git push` because it didn't recognize my ssh key. Turns out someone has created a project to solve this problem: [github-keygen][gkg]. You just clone the repository, run the perl script with your username as an argument, and it creates all the keys and configurations that you'll need. From the documentation:

{% highlight text %}
git clone https://github.com/dolmen/github-keygen.git
cd github-keygen
./github-keygen treydavis
cd ..
rm -Rf github-keygen
{% endhighlight %}

Next you'll have to change the remote URL for your git repository so that the ssh config will pick the right key. Just change any `github.com` to `username.github.com`:

{% highlight text %}
git remote origin set-url treydavis.github.com:treydavis/treydavis.github.io.git
{% endhighlight %}

Now your `git push` should work again.

[ourblog]: http://mcgeedavis.github.io
[gkg]: https://github.com/dolmen/github-keygen
