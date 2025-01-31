# FF7 Flat Wiki
> Static mirror of [FF Inside Wiki](https://wiki.ffrtt.ru) in [Markdown](https://www.markdownguide.org/basic-syntax/) format

Markdown files automatically build into [ff7-mods.github.io/ff7-flat-wiki](https://ff7-mods.github.io/ff7-flat-wiki).

![alt text](https://i.ibb.co/x2zGG0V/Engine-parts.jpg "Engine parts")

## Rationale
> The existing [FF Inside Wiki](https://wiki.ffrtt.ru) is a vast and amazing treasure trove of information, however, there are questions about resiliency, editability and longevity. In the interest of retaining the knowledge in this area, we should propose at least an independent backup.
This repo contains the migration tool, the migrated data will be loaded persisted in [ff7-flat-wiki](https://ff7-mods.github.io/ff7-flat-wiki)

## Run locally
- Install ruby and bundler (`gem install bundler`)
- Clone repo
- cd into `ff7-flat-wiki/docs`
- Install by `bundle install`
- Run with `bundle exec jekyll serve --baseurl=""`
- Open `localhost:4000`
_Note: [URL links on local jekyll don't behave like they do on Github Pages due to automatic 301s. Not going to fix it. Manually tweaking of the URL is required.](https://github.com/jekyll/jekyll/issues/9450#issuecomment-2127637456)_

## Editing
To be discussed.
