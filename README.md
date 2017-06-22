# Never Thought So

Never Thought So is a Jekyll served blog hosted on Github Pages. Additionally, it uses various third party tools for intergration.
This website is available at [https://neverthoughtso.com](https://neverthoughtso.com).

## Getting Started

You can either clone this site or the template I started with. Several parts have modified or added to the template to tailor it to Github Pages. These changes are not required if a different hosting service is  being used because GHPages levies certain restrictions to it's builds.
You can clone this project or the template on your local machine with following instructions.

### Prerequisites

The following dependencies are which I know of, if you find anything is missing, do let me know.

```bash
git
ruby
gem
jekyll
```

If you plan on building directly on the server and not locally, you only need `git`.

### Installing

For hosting on Github Pages using this site:
1. Fork it on Github with the repository name as `yourusername.github.io`
* First clone this repository as follows:
![alt]({{ site.baseurl }}/assets/neverthoughtso/wheretoclick.png)
![alt]({{ site.baseurl }}/assets/neverthoughtso/forking.png)
* Then, rename this repository as `yourname.github.io`

2. Clone locally
```bash
git clone https://github.com/yourusername/yourusername.github.io
```

3. Make changes
```bash
//If you create new files, be sure to add them to git as follows:
git add filename
//Once you are done making changes to a particular file, commit them:
git commit filename -m "Commit message"
//Once you are done with the changes, push these changes to the server:
git push
```

For cloning this repository:
```bash
git clone https://github.com/bhediathewolf/bhediathewolf.github.io
```

## Built With

* [Github Pages](https://pages.github.com) - Used for hosting
* [Jekyll](https://jekyllrb.com) - Parsing engine used by Github Pages to generate static sites
* [CloudFlare](https://cloudflare.com) - Content Delivery Network used for SSL
* [AddThis](http://addthis.com) - Used for Share buttons and Pop up Subscriber form 
* [Disqus](https://disqus.com) - Used for comments on posts
* [TravisCI](https://travisci.org) - Used for online build test; GHPages aren't that useful with errors

## License

This project is licensed under [Apache 2.0]({{site.baseurl}}/LICENSE).

## Acknowledgements

* [CloudCannon](https://github.com/CloudCannon/frisco-jekyll-template) - This template allowed for much cleaner product code than I could have independently done
* [Unsplash](https://unsplash.com) - They will redefine commercial nature of photography with amazing work and such great content
* [MindDust](https://github.com/minddust) - His blog's repository allowed for me add Project Page to my blog
