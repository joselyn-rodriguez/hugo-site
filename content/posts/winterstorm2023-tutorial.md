---
title: "Winter storm 2023 academic website tutorial using Hugo"
date: 2023-01-16T18:49:47-05:00
draft: false
---


### Pre-requisites

1. need homebrew installed (for Mac)
    1. need to install Hugo
2. (optionally need to make a netlify account)
3. need a github account

### Setting things up locally:

- Follow the quickstart guide to get a site up and running quickly: [https://gohugo.io/getting-started/quick-start/](https://gohugo.io/getting-started/quick-start/) (written again below)

    - create the site using the commands below

    ```bash
    hugo new site {site name}

    cd {site name}

    git init
    ```

    - This is what our directory will look like
        
    ![Screen Shot 2023-01-13 at 10.39.12 AM.png](/images/Screen_Shot_2023-01-13_at_10.39.12_AM.png)

    - we can start our local server right away so we can see changes as we make them. In your terminal in the main directory of your folder, type 

    ```bash
    hugo server
    ```
    - this will start your local server so we can see our changes as we make them. Go to your local server (generally it's just http://localhost:1313/) (it should be a blank page for now!)

    ![Screen Shot 2023-01-16 at 7.24.05 PM.png](/images/Screen_Shot_2023-01-16_at_7.24.05_PM.png)



- let’s take a closer look at the config.toml file
    - in your main directory, type the following to open the file in your terminal. 
    ```bash
    nano config.toml

    ```
    - We can see the file below. This file shows us the main information for our site so far. The config file will contain the paramters for our website which will be very important. Generally themes will make heavy use of the parameters in this file. Read more about it here: https://gohugo.io/getting-started/configuration/
    - `baseURL` refers to the URL for the site. This will change when we update our url for github pages 
    - `languageCode` refers to the language of the site (Hugo has support for many different languages)
    - `title` should be pretty self-explanatory. 
    - these parameters can be accessed anywhere else in your website which is why most themes will make heavy use of this file. 

    ```bash
    baseURL = 'http://example.org'
    languageCode = 'en-us'
    title = 'My New Hugo Site'
    ```

- There’s not really much in here yet, so we’ll add to it. First we need a theme.
    - Find one you like here: [https://themes.gohugo.io/](https://themes.gohugo.io/)
    - I will be using [this one](https://github.com/hugcis/hugo-astatine-theme/) (and suggest you use the same, but feel free to use another one if you're up for the challenge)
    - once you've picked a theme, type the following line in your command prompt replacing the necessary blanks with your theme information:

    ```bash
    # adding the theme as a submodule is super important! It won't work correctly if you don't do it this way!
    git submodule add https://github.com/{your-theme} themes/{name of theme}
    ```

    - This adds in the theme as a _submodule_ of your current repository. This means that you're telling github where to find the repository you want without actually copying all the information into your own repository (handy!)
    - Now we can add in the theme information to our config file with the following line of code in the terminal.
    
    ```bash
    # take a look inside this config file!
    echo "theme = '{name of theme}'" >> config.toml
    
    ```

    - let's go ahead and open the file itself again using 

    ```bash
    nano config.toml
    ```

    - we'll see the following lines now:

    ```bash
    baseURL = 'https://joselyn-rodriguez.github.io/winterstorm2023-site/'
    languageCode = 'en-us'
    title = 'Winter Storm 2023 academic website tutorial'
    theme = 'astatine' # you'll see your theme name!
    ```

    - before it'll work, we need to add one more line (for use with github pages). add the following line to this file below theme: 

    ```bash     
    publishDir = 'docs' # this line is important for github pages!
    ```

    - The next part is specific to the theme you're using
      
    - You have to take a close look at the instructions for the theme that you want to use, different themes make use of different ways of putting a site together.
        - what is necessary in the config file? Generally the theme instructions will tell you. Here, we're told to look at the [example config file](https://github.com/hugcis/hugo-astatine-theme/blob/master/exampleSite/config.toml/) (copied below)
        - we only need to copy from line 14 down. 
        
        ```bash
        # This is the configuration file for the example website of the Hugo theme
        # Astatine (see https://github.com/hugcis/hugo-astatine-theme).
        #
        # The URL from which the site will be served
        baseurl = "https://hugcis.github.io/hugo-astatine-theme/"
        # Language used
        languageCode = "en-us"
        # Website title
        title = "Astatine Theme"
        # Theme used
        theme = "hugo-astatine-theme"

        ###### FROM HERE DOWN IS WHAT WE NEED ###### 
        preserveTaxonomyNames = true
        rssLimit = 10
        paginate = 10

        # Code highlighting
        pygmentsCodefences = true
        pygmentsStyle = "native"

        # Taxonomies (only tags and categories are supported out of the box but you can
        # add more)
        [taxonomies]
            category = "categories"  
            tag = "tags"

        # Configure permalinks style
        [permalinks]
            post = "/:slug/"
            page = "/:slug/"

        # Configure main navbar links. They can have a weight to select the order.
        # This links to content within the content/post/ folder
        [[menu.main]]
            name = "Posts"
            url = "/post/"
            weight = -150

        # This links to the page about.md
        [[menu.main]]
            name = "About"
            url = "/about/"
            weight = -110

        # Make the tags and categories pages accessible directly from the navbar.
        [[menu.main]]
            name = "Tags"
            url = "/tags/"
            weight = -120

        [[menu.main]]
            name = "Categories"
            url = "/categories/"
            weight = -130

        # Site wide params and SEO
        [params]
            # Site description. Individual pages can have descriptions too but if
            # missing it will fallback to that one.
            description = """The homepage of Astatine. This website is a demo the of the \
            Hugo theme Astatine."""
            # Author of the site
            authorName = "Jack Harkness"
            # Main image for the author. This will be the default image for SEO.
            [params.imgname]
                name = "img/main.jpg"
                # Add an alt description for the image
                alt = "Profile picture"

            # Indicate if you host Katex yourself. Defaults to using the CDN KaTex.
            # hostedKaTex = false

            # Optional: add a twitter handle and mastodon handle for SEO.
            # [params.twitter]
                # name = "@Jack_harkness"
            # [params.mastodon]
                # name = "@jkharkness"
                # host = "mastodon.social"
            
            # Enable link to feed in footer
            blogrss = true

            # Enable pingback and webmention via webmention.io
            # webmention = "hugocisneros.com"


        # Sitemap location (default is /sitemap.xml)
        [sitemap]
        filename = "sitemap.xml"
        ```
        
    - This site is still missing some things though. If you look in content, nothing is there yet! The theme instructions tell us we need to add in a landing page. 
    - navigate to the content folder and create a new file there using 
    ```bash 
    touch _index.md
    ``` 

    
    - in Hugo, files that start with "_" are special files that are generally used as a landing page for a given set of pages. This theme uses it to display our main content page but every content folder will have it's one `_index.md` file.

    - while we're here, let's also make ourselves a posts folder by typing

    ```bash
    mkdir posts
    ```

    - Once you created the `_index.md` file using `touch` populate the file with the following [content](https://raw.githubusercontent.com/hugcis/hugo-astatine-theme/master/exampleSite/content/_index.md):

    - Notice the three `---` lines in the file enclosing some content. This is indicating that it is front matter, special metadata, embedded inside of the content file. This content isn't necessarily displayed on the page unless it is being called somewhere else in the html files (which it is! in this file in your directory: themes/astatine/layouts/partials/info.html)

```html
<div class="head container grid sm:grid-cols-2 grid-cols-1
            justify-around flex-wrap items-center"
    itemscope itemtype="http://schema.org/Person">
    <div class="picture p-8 max-w-[80%] mx-auto basis-20 grow shrink"
        itemscope itemtype="http://schema.org/ImageObject">
        <picture>
            {{ if .Params.ImgOther }}
            {{ range .Params.ImgOther }}
            <source srcset="{{ .name }}"{{ if .type }} type="{{ .type }}"{{ end }}>
            {{ end }}
            {{ end }}
            <source srcset="{{ .Site.Params.imgname.Name }}"
                    {{ if .Site.Params.imgname.Type }} type="{{ .Site.Params.Imgname.Type }}"{{ end }}>
            <img class="main-image u-photo mx-auto"
            itemprop="contentUrl" alt="{{ .Site.Params.Imgname.Alt }}"
                src="{{ .Site.Params.imgname.Name }}">
        </picture>
    </div>
    <div class="mx-4 ml-8 basis-60 grow shrink-2 leading-snug text-base">
        <a  class="u-url font-bold" rel="me" itemprop="url" href="{{ .Permalink }}">
            <h1 class="text-black dark:text-zinc-300 p-name border-0"
                itemprop="name">{{ .Params.Name }}
            </h1>
        </a>
        {{ if .Params.sameas }}
        {{ range .Params.sameas }}
        <link href="{{ . }}" rel="me" itemprop="sameAs">
        {{ end }}
        {{ end }}
        <h2 itemprop="jobTitle" class="text-xl my-0 border-none">{{ .Params.Personal_title }}</h2>
            {{range .Params.Address }}
            <div itemprop="address" itemscope itemtype="http://schema.org/PostalAddress">
            <span itemprop="streetAddress">
                {{ .name }}
                <br>
                {{ .street }}
            </span>
            <br>
            {{ with .postal_code }}<span itemprop="postalCode">{{ . }}</span>{{ end }}
            {{ with .locality }}<span itemprop="addressLocality">{{ . }}</span>{{ end }}
            <br>
            {{ with .email }}
            <a href="mailto:{{ . }}">{{ . }}</a>
            {{ end }}
            {{ with .emailimg }}
            <picture>
                {{ if .dark }}
                <source srcset="{{ .dark }}" class="email"
                        alt="Email screenshot"
                        media="(prefers-color-scheme: dark)">
                {{ end }}
                {{ if .light }}
                <img class="email h-5 inline" src="{{ .light }}" alt="Email screenshot">
                {{ end }}
            </picture>
            {{ end }}
            <br>
            </div>
            {{ end }}
    </div>
</div>
```

- If you want to change the pictures, you just need to add some new pics in the `static/` folder and then update the link in the `_index.md` file!

- to make new posts, you can go to your main directory then type 
```bash
hugo new posts/{name of post}.md
```
    - all the posts are going to be written in markdown. You can refer to any [markdown guide](https://www.markdownguide.org/basic-syntax/)
    - use any texteditor to edit these files
    - you can set `draft = true` if you don't want to publish pages immediately!

- In general, every theme is going to be different since people use different methods. 
    - For example, some things you might see:
        - different CSS packages (using bootstrap, tailwindcss, etc) which will require additional downloads and preparation on your part.
    - In general, take a look at the example site and understand the structure that the creator of the site has established
        - you’ll likely need to have index files for each of the main subfolders defining the landing page for that section
            - in the main folder: config.toml
            - in the content folder: _index.md


- when you’re ready to build your static pages that will be hosted, you will run the following code to build our html files to host on github. 

```bash
hugo # yes that's it!
```

- once everything is run and you’re ready to launch the site, you proceed to the next step which is preparing your github page.


### Setting up the github pages host:

- assuming that you have a github account set up, create a new repository.
    - if you’d like to use your username, then you should name the repository the same as your username (for example: {username}.github.io) but any repository name will work
        
        ![Screen Shot 2023-01-15 at 9.26.33 PM.png](/images/Screen_Shot_2023-01-15_at_9.26.33_PM.png)
        

- Once you’ve done this, there are still a few things left to do before your site is live
    - First, we need to deal with the action command in order for Github to know how to build the site correctly.
        - Copy this file into the main folder of your site: [https://github.com/joselyn-rodriguez/winterstorm2023-site/blob/master/.github/workflows/hugo.yml](https://github.com/joselyn-rodriguez/winterstorm2023-site/blob/master/.github/workflows/hugo.yml)
            - Replace the branch on line 6 with whatever branch you’re launching from (probably main)

        
- After that, we need to setup our github pages and activate it on this repo.
    - Go to settings, below code an automation, click on “Pages”
        
        ![Screen Shot 2023-01-15 at 9.34.34 PM.png](/images/Screen_Shot_2023-01-15_at_9.34.34_PM.png)
        
        - Under “Branch” choose the branch that you pushed to (it will either be main or master) and then choose “docs” as the folder that the site is built from.


- now we can actually push our files to github

    - add this repository as the remote origin to your local repository by following the “create a new repository on the command line”.
        - in the repository of your new site, type the following: 
        ```bash
        git add .
        git commit -m "first commit!"
        git branch -M main
        git remote add origin {whatever your git repo is}
        git push -u origin main
        ```

- Once that is set, you can check whether it launched correctly by clicking on the link for your page
    
    ![Screen Shot 2023-01-15 at 9.40.48 PM.png](/images/Screen_Shot_2023-01-15_at_9.40.48_PM.png)
    

### Other things!

- Getting your domain name!
    - there are lots of places to get a domain name
        - [godaddy](https://www.godaddy.com/)
        - [domain](https://www.domain.com/)
        - [google](https://domains.google/)
        - [bluhost](https://www.bluehost.com/) (i used this one!)
        - [netlify](https://www.netlify.com/)
        - [cheapnames](https://www.cheapnames.com/)
        - [namecheap](https://www.namecheap.com/)
        - [dreamhost](https://www.dreamhost.com/)
        - and so many more
    - Once you get it, you gotta head to the [github documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site/) to get it setup in github pages (and don't forget to change your hugo site's `config.toml` file baseURL parameter)

- more advanced hugo-ing. 
    - templating is a powerful tool that you can use to start customizing your website (and building your own themes)
        - https://gohugo.io/templates/introduction/
        - https://cloudcannon.com/community/learn/hugo-beginner-tutorial/
            - this is a whole tutorial but goes into templating nicely
    - deploying hugo on different sites
        - https://gohugo.io/hosting-and-deployment/
            - I use and highly recommend using netlify

- examples of phd website using certain themes:
    - congo: [https://themes.gohugo.io/themes/congo/](https://themes.gohugo.io/themes/congo/)
        - [https://antoinesoetewey.com/cv/](https://antoinesoetewey.com/cv/)
        - [https://rohn.tech/](https://rohn.tech/)
            - github: [https://github.com/KevinRohn/KevinRohn.github.io](https://github.com/KevinRohn/KevinRohn.github.io)