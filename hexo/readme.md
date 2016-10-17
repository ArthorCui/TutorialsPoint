#Hexo
Hexo is a fast, simple and powerful blog framework. You write posts in `Markdown` (or other languages) and Hexo generates static files with a beautiful theme in seconds.

##Setup & Installation

####requirenments
* NodeJS
* Git

####install hexo
```
$ npm install -g hexo-cli
```
####init blog
```
$ hexo init blog
$ cd blog
$ npm install
```
You can use `tree` command in current folder path.
```
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

#####_config.yml
See [here](#configuration)

#####package.json
Application data.
```
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": "3.2.2"
  },
  "dependencies": {
    "hexo": "^3.2.0",
    "hexo-generator-archive": "^0.1.4",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-index": "^0.2.0",
    "hexo-generator-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.2.0",
    "hexo-renderer-stylus": "^0.3.1",
    "hexo-renderer-marked": "^0.2.10",
    "hexo-server": "^0.2.0"
  }
}
```

#####scaffolds
When you create a new post, Hexo bases the new file on the scaffold.
```
$ hexo new photo "My Gallery"
```

#####source
Source folder. This is where you put your site’s content. Hexo ignores hidden files and files or folders whose names are prefixed with _ (underscore) - except the _posts folder. Renderable files (e.g. Markdown, HTML) will be processed and put into the public folder, while other files will simply be copied.

#####themes
such as system automatic `landscape`, and I found some other simple and liked themes:
* [NexT](https://github.com/iissnan/hexo-theme-next) Contributor by [IIssNan](http://notes.iissnan.com/)
* [Mirror](https://github.com/LoeiFy/Mirror) Contributor by [LoeiFy](http://mirror.am0200.com/)
* [Maupassant](https://github.com/tufu9441/maupassant-hexo) Contributor by [tufu9441](https://www.haomwei.com)
* [Anisina](https://github.com/Haojen/hexo-theme-Anisina) Contributor by [haojen](http://haojen.github.io/)
* [Yilia](https://github.com/litten/hexo-theme-yilia) Contributor by [litten](http://tuijiankan.com/)
* [Striped](https://github.com/battlemidget/hexo-theme-striped) Contributor by [battlemidget](http://blog.astokes.org/)
* [Fexo](https://github.com/forsigner/fexo) Contributor by [forsigner](http://forsigner.com/)
* [Scribble](https://github.com/muan/scribble) Contributor by [muan](http://muan.co/)

##Configuration

##Commands

* **init**

```
$ hexo init [folder]
```

* **new**

```
$ hexo new layout <title>
```

* **generate**

> * -d, --deploy	Deploy after generation finishes
> * -w, --watch	Watch file changes

```
$ hexo generate
```

* **publish**
Publishes a draft.

```
$ hexo publish [layout] <filename>
```

* **server**
Starts a local server. By default, this is at http://localhost:4000/.

> * -p, --port	Override default port
> * -s, --static	Only serve static files
> * -l, --log	Enable logger. Override logger format.

```
$ hexo server
```

* **deploy**
Deploys your website.
> -g, --generate	Generate before deployment

```
$ hexo deploy
```

* **clean**
Cleans the cache file (db.json) and generated files (public).

```
$ hexo clean
```

* **list**
Lists all routes.

```
$ hexo list
```

##Migration

* **RSS**
First, install the `hexo-migrator-rss` plugin.
```
$ npm install hexo-migrator-rss --save
$ hexo migrate rss <source>
```

* **Jekyll**
Move all files in the Jekyll `_posts` folder to the `source/_posts` folder.

Modify the `new_post_name` setting in `_config.yml`:
```
new_post_name: :year-:month-:day-:title.md
```

* **Octopress**
Move all files in the Octopress `_posts` folder to the `source/_posts` folder.

Modify the `new_post_name` setting in `_config.yml`:
```
new_post_name: :year-:month-:day-:title.md
```

* **WordPress**
First, install the hexo-migrator-wordpress plugin.
```
$ npm install hexo-migrator-wordpress --save
$ hexo migrate wordpress <source>
```

* **Joomla**
First, install the hexo-migrator-joomla plugin.
```
$ npm install hexo-migrator-joomla --save
$ hexo migrate joomla  <source>
```