# Jekyll Notes

## Instalation

---

Source: [Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/)

### Install Ruby and other prerequisites

```
sudo apt-get install ruby-full build-essential zlib1g-dev
```

### Setup environment variables

Add the next lines to `./bashrc`

```
export GEM_HOME="$HOME/gems"
export PATH="$HOME/gems/bin:$PATH
```

### Install Jekyll and Blunder

```
gem install jekyll bundler
```


## Create Jekyll site

---

Source: [Quickstart](https://jekyllrb.com/docs/)

### Create a new Jekyll site at `./myblog`

```
jekyll new myblog
```

If you already have files of an old site (from github for example) you can run

```
jekyll new myblog --force
```

It will not delete the posts

### Build the site

```
bundle exec jekyll serve
```

or 

```
bundle exec jekyll serve --livereload
```

To automatically refresh the page after a change