# Building my first JAM site
Development notes!

## What is JAM
JAM stands for Javascript - APIs - Markup. That's rather vague. More precisely it's a way of developing and deploying websites suitable mainly for publishing sites like blogs or presentation sites.

Its main principle is that there's no backend. That's how they market it, but that's of course not true. What they mean is that there is no public-facing backend logic. All the public content is generated ahead of time into a set of static html files (hence Markup) that can be served by any server or CDN. (So you still need a backend.)

The HTML generation is handled by one of many static site generators like Gatsby, Hexo, Nuxt, Sapper... there're many! The output in form of the HTML files can then be hosted anywhere. Since the JAM got quite popular there exists very good and sleek hosting solutions that solve basically all the hassle of setting up a server. The deployment is usually as easy as giving the hosting access to a GitHub repo, where it sniffs for your SSG and automatically configures complete CI pipeline for you. Including SSL, rebuild on pushes to master, image optimization, CDN... you name it. To name a few: Netlify, Vercel, Heroku and probably more.

What the JAM marketers usually don't scream out so loudly is where comes the content from. SSG is nice but it has to have some input data to populate the HTML files with. Most SSG are able to work off a bunch of Markdown files in laying in a directory. That works well as long as anyone who will edit the content can work with markdown and git to actually commit her changes. There're solutions like Netlify's Headless CMS that can expose a graphical CMS build on top of just that - bunch of markdown files and git.

Another way, which should(?) be supported by most SSGs is fetch the content from some kind of API. The API can be hosted anywhere and can be powered by anything. It can be WordPress, or Ghost, or SSH with markdown files. In any way you'll need a backend for that. And this time it's a true backend -- with logic. The important thing here is that it's only used by the content editors to alter the content and by the SSG to fetch the content and generate the site out of it. To make this automated you usually setup some kind of web hook that calls your static site hosting solution to regenerate the site.

## This site
The site I'm building is going to be quite simple and I'm very confident it will not need to get any more complicated than outlined below. At least for couple years.

It's a site for a cycling workshop I and my friend are build now. The key features are:
- communicate the basic info about the workshop and us - address, contact information etc.
- show off our bike builds and various other handwork projects. Each project is a bunch of good quality images a heading and maybe a few paragraphs of text.
- straight forward editing workflow. My two pals aren't friends with computers so they might otherwise never put any content up.


## Tech Stack
Let's try to asses what technical requirements these features translate to and then decide what tools and technologies I will use to fulfil them.

As you guessed we will build this with JAM stack. The first thing we will need is a static site generator. I could spend days thinking about which one is best but that would be a waste of time for such a small project. The capabilities are very even so I'll simple go with the one I'm most interested with: Sapper. That's because it's build on top of Svelte which is kind of a new take on component based FE frameworks. (Another contender would be probably Zola because it's written in Rust.)

To fulfill the third feature requirement we will need a CMS. Again there're many. I will use the Netlify CMS because it stores content directly in the git repository. That will enable me to have the whole website contained in a single package without any dependency on a database. The site is expected to be quite heavy on images. To protect the git repository growing huge with binary files I store the images in Git LFS.

To put the pieces together I will deploy everything to Netlify. With their free tier I should be able to configure
- hosting of the generated static files
- complete CI
- CMS including authentication with Netlify Identity

Here's a diagram

```                                        
                                            provide                 authenticate,
            commit changes               authentication            update content     write and edit content
                  :                            :                         :                    :                    
+-------------+   :  +---------------------+   :  +------------------+   :  +-------------+   :  +----------------+
| github repo | <--- | Netlify Git Gateway | <--- | Netlify Identity | <--- | Netlify CMS | <--- | Me and my pals |
+-------------+      +---------------------+      +------------------+      +-------------+      +----------------+
      |
      | fetch after edit
      v
+------------------+      +--------+      +---------------------+      +---------------+
| Netlify Build CI | ---> | Sapper | ---> | Netlify Hosting/CDN | ---> | Site visitors |
+------------------+  :   +--------+  :   +---------------------+  :   +---------------+
                      :               :                            :
        pull repo, run sapper     generate HTML            serve static content
```

You could complain that I'll be locked in with Netlify and you'd be right. However I'm ok with that. All I need is part of the free tier and I do not expect to exceed its limits any time soon. Also as already mentioned the site will be completely contained in the git repository so moving it out of netlify to a more customized hosting solution should be quite easy. Furthermore my learning objectives with this project are in the Sapper and Svelte as that will be my first ever experience with any real front end framework.

## RoadMap
- [x] First create a super basic Sapper app merely rendering front page.
- [ ] Explore how Sapper static content generation works, especially how it handles markdown content sourcing.
- [ ] Add Netlify CMS to manage the markdown content.
- [ ] Deploy to netlify.
- [ ] Create a proper design and structure.
- [ ] Extend the site with post pages.
- [ ] Go public.


## Setting up Sapper
After researching various bootstrapping repos I went with the [official Sapper template](https://github.com/sveltejs/sapper-template) mainly because everything in this world seems outdated already when it comes out. And since this is the official template it has the higher chances to work with the latest Sapper.

Anyway after degitting it and installing deps. Launching it is easy. `npm run dev` and it works, including live reloading which feels like magic when you see it for the first time in your live.
Not everything is that beatiful. First [I noticed](https://stackoverflow.com/questions/61843696/why-sapper-omits-clossing-html-tags) that the html generated with `npm run export` is missing the closing `body` and `html` tags. Weird.
Right after that, without changing any fo the files, the live reloading suddenly does not work. o.O I guess it still counts as magic then.

Another thing that bothers me is that Sapper is supposed to render a static html. However the template includes `server.js` which spins up a polka server. Further the official docs mention several times the server. This makes me a bit nervous since I plan to deploy this to a static file server.

Aha! Worry not, this is actually nicely explained in the [Exporting section](https://sapper.svelte.dev/docs#Exporting) of the docs. I'll just need to make sure all my pages can be reached by crawling from the index page. Should be easy.

The docs states that
> When not to export
>
> The basic rule is this: for an app to be exportable, any two users hitting the same page of your app must get the same content from the server. In other words, any app that involves user sessions or authentication is not a candidate for sapper export.

I will have authenticated users but the content will be handled by the Netlify Identity thingy so that's ok.

## First deploy
That was an easy pie actually. Just committed, pushed, started new site on Netlify and [it's up](https://cyklozalar.netlify.app/).

## TODO fot later
- setup LFS on Netlify

## Resources
- https://github.com/sveltejs/sapper-template
- https://github.com/mrispoli24/sapper-netlify-jamstack-starter
- https://spiffy.tech/blog/setting-up-sapper-with-netlify-cms/
