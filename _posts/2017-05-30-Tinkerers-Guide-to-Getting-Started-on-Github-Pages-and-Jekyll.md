---
title: Tinkerers Guide to Getting Started on Github Pages and Jekyll
date: 2017-05-30
description: By the time you will finish this post, you will have your own website
categories:
	- technology
image: https://source.unsplash.com/LUgHXvLe_kM/2000x1322?a=.png
---
If you read the description above, you have been a little misled. You __will__ have your website; it might require a _little_ additional effort. Worry not, that's what the next chapters are for!

### Getting a Template
First, let's pick a starting point for our website. We can use the templates [included in the Github Pages gem](https://pages.github.com/themes/) or, we can use a [third party template](https://drjekyllthemes.github.io). There are [many sites](http://lmgtfy.com/?q=jekyll+templates) to browse templates.

Let's pick [frisco](https://github.com/CloudCannon/frisco-jekyll-template) by [CloudCannon](http://cloudcannon.com).
![alt-text]({{ site.baseurl }}/assets/getting-started/frisco.jpg "Screenshot: Frisco template")
The template is available  on [Github](https://github.com/CloudCannon/frisco-jekyll-template) for one's personal use.

Now, get yourself an account on [Github](https://github.com/join) or, if you have an account already, [log in](https://github.com/login).

### Fork it before you make it
On the template's github page, click on fork to get something like,
![alt-text]({{ site.baseurl }}/assets/getting-started/fork.png "Fork the template")
It should take no more than 5 minutes.

_Notice_, the forked repository will now be your-user-name/frisco-jekyll-template.

Go to the settings, and rename the repository to your-user-name.github.io.
![alt-text]({{ site.baseurl }}/assets/getting-started/rename.png "Rename the repository")
After this, check your repository's settings to find something like this,
![alt-text]({{ site.baseurl }}/assets/getting-started/link.png "Your website is served")

If it is green, it will be already published at the given link. Otherwise, it will be available after the first commit, if everything works out.

### Local Environment
We will be working with this repository a lot. Github Pages does not require you to build it locally. There is no dire need for it unless you are [using custom plugins](https://blog.sorryapp.com/blogging-with-jekyll/2014/01/31/using-jekyll-plugins-on-github-pages.html). We will setup a small ecosystem to work efficiently with our repository.
#### Cloning the repository locally
Let's clone it locally to work more efficiently.
```bash
git clone https://github.com/jekyllblogger/jekyllblogger.github.io.git
cd jekyllblogger.github.io
```
We have successfully cloned our website locally. 

#### Using [Travis-CI](http://travis-ci.org) for build status
Because we are not locally building our site, we rely on Github Pages for error logs if and when our build fails. From experience, it is not wholesome for the [experimentalist](https://www.merriam-webster.com/dictionary/experimentalist). But, the solution is a very simple one. 

Travis-CI is an online tool, in intregration, with Github, that allows users to deploy their code directly from Github to Travis-CI. This means, even though we are not building it locally on our PC, we are building it someplace other than the Github Pages. Plus, it is very easy to setup travis for our repository.

First, let's add Travis-CI to our repository. We can do this by going to the settings -> Integrations and Services. Search and select travis.
![alt-text]({{ site.baseurl }}/assets/getting-started/travis.png "Add travis integration to Github")
Now, we shall [sign into Travis using our Github account](https://travis-ci.org/).

Once, you are in Travis, click on the '+' icon next to My Repositories on the left hand side. That will bring you to something like this,
![alt-text]({{ site.baseurl }}/assets/getting-started/travison.png "Enable Travis for your website")

Locally, we shall write a `.travis.yml` configuration file for Travis-CI. The contents of your .travis.yml are:
```bash
language: ruby
rvm:
- 2.1
script: bundle exec jekyll build
```
Here, we specify the language we will be building the website with, along with the version. We are building with ruby because Jekyll uses ruby. If we were to, or you might be using plugins, we use `.rb` files to do so. `script` is the script we are using travis for.

Once, we are done, we will add, commit and push this file to our repository.
```bash
git add .travis.yml
git commit .travis.yml -m "Initial Commit"
git push
```
We are all set to build our site on travis to check for errors but it won't be until the next push.

On first build though, you will most likely be greeted with a build error like,
![alt-text]({{ site.baseurl }}/assets/getting-started/error.png "Build Fails")
To solve this, we will exclude `vendor` from our `_config.yml`.
```bash
...

exclude:
  - Gemfile
  - Gemfile.lock
  - README.md
  - LICENCE
  - vendor

...
```
After this, simply commit the changes to your repository. We will still run into errors because frisco is built without Github Pages in mind. It is a standalone Jekyll served website. This means, it has plugins and other sections not supported by Github Pages. We will look at those as we encounter them.

#### Slack Integration with Travis-CI
Travis-CI works well but I noticed that it always emails on failure until the state is a success. This is a good practice but clutters your email at times. With such emotion, we will [integrate travis](https://docs.travis-ci.com/user/notifications/#Configuring-slack-notifications) with [Slack](https://slack.com/).

This requires a Slack channel. As I believe not all of you might be interested in this, I am going to assume you have a Slack account and a channel to integrate with. Integration might post to all rooms or a specific one. Here, we will be posting to the room 'build-status'.

__*Note:*__ *Integration with Slack requires use of `gem install`. This is available after installing ruby locally.*

Let's add the travis app in Slack for integration.
![alt-text]({{ site.baseurl }}/assets/getting-started/addapp.png "Add travis app for integration")
Now, search for travis, and install.
![alt-text]({{ site.baseurl }}/assets/getting-started/addapp2.png "Search for Travis")

Now, we come to the part about using `gem install`. It is optional but recommended. We are encrypting our key which allows for communication between travis and slack.

To do this, we will run the given command inside our repository. It will auto append the encrypted values to our `.travis.yml`.
![alt-text]({{ site.baseurl }}/assets/getting-started/slackencrypt.png "Copy the second command")

```bash
cd jekyllblogger.github.io
gem install travis
travis encrypt "yourjekyllblog:<token>#build-status" --add notifications.slack.rooms -r jekyllblogger/jekyllblogger.github.io
```
Once done, your `.travis.yml` will be changed as such,
```bash
...

notifications:
  slack:
    rooms:
      secure: <very long gibberish>

...
```

Additionally, the message to be in a format that gives the information I want in the quickest way I presume. For this, we shall add the following lines. You can format it your using the travis integrations [docs](https://docs.travis-ci.com/user/notifications/#Customizing-slack-notifications) or, aquaint yourself with travis through [this blog post](http://blog.tgrrtt.com/exploring-the-travisci-configuration-file).

With additional template optoins, your config should look like this:
```bash
language: ruby
rvm:
- 2.1
script: bundle exec jekyll build
notifications:
  slack:
    template:
      - "%{repository_slug} :: %{branch}"
      - "%{result} (%{build_number} :: %{build_id})"
      - "%{message}"
      - "%{commit_message}"
    rooms:
      secure: <very long gibberish>
    on_start: never
    on_failure: always
    on_success: change
    on_pull_requests: false
```

### Conclusion
This is end of this post. As promised, you have your website served. Also, you have a nice Travis-CI build with notifications being sent to your Slack. 
We have traction with our blog, let's develop it further, together.