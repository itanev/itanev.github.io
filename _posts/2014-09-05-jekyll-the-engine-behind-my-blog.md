---
layout: post
title: Jekyll - The engine behind my blog
description: "In this post I will explain what is Jekyll and some of its basics."
modified: 2014-09-05
tags: [Jekyll, Blog, Engine, Parser, GitHub pages]
image:
  feature: abstract-3.jpg
comments: true
share: true
---

Jekyll is free, simple, blog-aware, static site generator written in Ruby by GitHub's co-founder - Tom Preston-Werner, it is perfect for small projects but not so good for big ones. Think of it like a file-based CMS, without all the complexity. Jekyll takes your content, renders Markdown and Liquid templates, and spits out a complete, static website ready to be served by Apache, Nginx or another web server.

### But what exactly is Jekyll ?

Jekyll is **not Blogging Software** it is a **parsing engine**. It is the engine behind **GitHub Pages**, which you can use to host sites right from your GitHub repositories.

The most important thing to realize about Jekyll is that it creates a static representation of your website requiring only a static web-server.

> "Developers like Jekyll because they can write content like they write code"

Therefore if you like the **KISS** (Keep it simple, stupid) principle and you prefer the command-line over an UI, then give Jekyll a try.

### Jekyll structure
	
Because Jekyll is a parsing engine it has very strict folder structure.	

#### Basic structure
		
This is the structure according to the [official documentation](http://jekyllrb.com/docs/structure/).

<span><i class="small fa fa-file"></i>&nbsp;&nbsp;***_config.yml*** </span> <br />
<span><i class="small fa fa-folder"></i>&nbsp;&nbsp;***_drafts***</span> <br />
<span>&nbsp;&nbsp;&nbsp;&nbsp;<i class="small fa fa-file"></i>&nbsp;&nbsp;***some-post-draft-in.textile***</span> <br />
<span>&nbsp;&nbsp;&nbsp;&nbsp;<i class="small fa fa-file"></i>&nbsp;&nbsp;***some-post-draft-in.markdown***</span> <br />
<span><i class="small fa fa-folder"></i>&nbsp;&nbsp;***_includes***</span> <br />
<span>&nbsp;&nbsp;&nbsp;&nbsp;<i class="small fa fa-file"></i>&nbsp;&nbsp;***footer.html***</span> <br />
<span>&nbsp;&nbsp;&nbsp;&nbsp;<i class="small fa fa-file"></i>&nbsp;&nbsp;***header.html***</span> <br />
<span><i class="small fa fa-folder"></i>&nbsp;&nbsp;***_layouts***</span> <br />
<span>&nbsp;&nbsp;&nbsp;&nbsp;<i class="small fa fa-file"></i>&nbsp;&nbsp;***default.html***</span> <br />
<span>&nbsp;&nbsp;&nbsp;&nbsp;<i class="small fa fa-file"></i>&nbsp;&nbsp;***post.html***</span> <br />
<span><i class="small fa fa-folder"></i>&nbsp;&nbsp;***_posts***</span> <br />
<span>&nbsp;&nbsp;&nbsp;&nbsp;<i class="small fa fa-file"></i>&nbsp;&nbsp;***2014-09-05-what-is-jekyll.md***</span> <br />
<span>&nbsp;&nbsp;&nbsp;&nbsp;<i class="small fa fa-file"></i>&nbsp;&nbsp;***2014-09-01-some-test-post.md***</span> <br />
<span><i class="small fa fa-folder"></i>&nbsp;&nbsp;***_data***</span> <br />
<span>&nbsp;&nbsp;&nbsp;&nbsp;<i class="small fa fa-file"></i>&nbsp;&nbsp;***members.yml***</span> <br />
<span><i class="small fa fa-file"></i>&nbsp;&nbsp;***index.html***</span> <br />

| File/Directory | Description |
|:-------------: |:------------|
| _config.yml	 | Stores [configuration](http://jekyllrb.com/docs/configuration/) data. |
|-----------------------------------------------------------------------------------------|       
| _drafts		 | Drafts are unpublished posts. The format of these files is without a date. |
|----        
| _includes		 | This folder contains all the partial files that will be reused by your layouts and posts. |
|----            
| _layouts		 | Here are the templates that wrap posts. You could have different layouts for different posts. The liquid tag {{content}} is used to inject content into the web page. |
|----            
| _posts		 | Your dynamic content, so to speak. The naming convention of these files is important, and must follow the format: ***YEAR-MONTH-DAY-title.MARKUP***. | 
|----            
| _data			 | Well-formatted site data should be placed here. The jekyll engine will autoload all yaml files (ends with ***.yml*** or ***.yaml***) in this directory. If there's a file ***members.yml*** under the directory, then you can access contents of the file through ***site.data.members***. |
|----            
| _site			 | This is where the generated site will be placed. | 
|----
| index.html	 | Every file with a [YAML Front Matter](http://jekyllrb.com/docs/frontmatter/) section, it will be transformed by Jekyll. |
| and other      | The same will happen for any ***.html***, ***.markdown***, ***.md***, or ***.textile*** file in your site’s |
| HTML, Markdown, Textile files | root directory or directories not listed above. |
|----
| Other Files/Folders | Every other directory and file except for those listed above—such as ***css*** and ***images*** folders, ***favicon.ico*** files, and so forth—will be copied verbatim to the generated site. |
|----
{: border="1" cellspacing="0" cellpadding="10" }

If you plan to deploy your site on ***GitHub Pages*** you don't need _site directory in your repository. As I mention above Jekyll is the engine behind GitHub Pages so your files will be build on their servers.
		
[Here is one very simple guide of how to deploy on GitHub Pages](https://pages.github.com)

#### Basic Components
	
##### Posts
			
Posts are created by properly formatting a file and placing it the ***_posts*** folder. A post must have a valid filename in the form ***YEAR-MONTH-DATE-title.MARKUP***. Additionally, each file must have [YAML Front-Matter](http://jekyllrb.com/docs/frontmatter/) prepended to its content.
		
##### Pages
	
Pages are similar to posts. They are created by properly formatting a file and placing it anywhere in the root directory or subdirectories that do not start with an underscore. Pages do not compute categories nor tags so defining them will have no effect.
	
##### Drafts
	 	
Drafts are posts without a date. They’re posts you’re still working on and don’t want to publish yet. They are placed in the ***_drafts*** folder in your site's root.
	 	
##### Tags 
	 	
Posts can have tags associated with them as part of their meta-data. Tags may be placed on posts by providing them in the post's YAML front matter. You have access to the post-specific tags in the templates. These tags also get added to the sitewide collection.
	
##### Categories
		
Posts may be categorized by providing one or more categories in the YAML front matter. Categories offer more significance over tags in that they can be reflected in the URL path to the given post

### Jekyll setup

Jekyll comes as a Ruby gem so all you need to install it are just [Ruby](https://www.ruby-lang.org/en/downloads/), [RubyGems](http://rubygems.org/pages/download) and some operation system, it works well everywhere. Jekyll comes with a built-in development server that will allow you to preview your site.

#### Install

All you need to do to install Jekyll is this command.

{% highlight css %}
gem install jekyll
{% endhighlight %}

All of Jekyll’s gem dependencies are automatically installed by the above command.

[More about Jekyll installation](http://jekyllrb.com/docs/installation/)

### Basic commands

{% highlight css %}
jekyll build
{% endhighlight %}

As I mentioned Jekyll works using Markdown and Liquid. This command initialize the parsing of these languages to build the HTML pages that represent your site. The result could be found in the _site directory.

{% highlight css %}
jekyll serve
{% endhighlight %}

With this command you start the built-in development server that will allow you to preview what the generated site will look like in your browser locally and it is runned at  http://localhost:4000

##### The watch switch
		
You could call any of the above commands with the --watch switch. With it your changes will be regenerated automatically which means you will be able to see your changes without having to call the command again, except if you've changed the _config.yml file.

examples: 
{% highlight css %}
jekyll build --watch 
jekyll serve --watch
{% endhighlight %}

##### The drafts switch
		
To preview your site with drafts, simply run ***jekyll serve*** or ***jekyll build*** with the ***--drafts*** switch. Each will be assigned the value modification time of the draft file for its date, and thus you will see currently edited drafts as the latest posts.

examples: 
{% highlight css %}
jekyll build --drafts 
jekyll serve --drafts
{% endhighlight %}
	
[More about the commands](http://jekyllrb.com/docs/usage/)