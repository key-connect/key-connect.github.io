# Key Connect Website

Public website, powered by [Jekyll](https://jekyllrb.com/docs/)

## Run locally

```shell
bundle exec jekyll serve
```

And browse to <http://localhost:4000>.

## Generate api-docs site

```shell
npm install -g redoc-cli
cd api-docs
redoc-cli bundle path/to/api.yaml
rm index.html
mv .\redoc-static.html .\index.html
```
