---
layout: default
page_name: Getting Started
---

Getting Started
---

**Install**

```sh
$ npm install -g @bincode/jekpack # or yarn global add @bincode/jekpack
```

**Create a project**

```sh
$ jekpack new hello-world
```

**Install the dependencies**

```sh
$ cd hello-world
$ jekpack bundle
``` 

**Add to existing project**
- create `package.json` in your project with the following settings (or better copy from newly created):
```json
{
  "name": "PROJECT_NAME",
  "version": "1.0.0",
  "private": true,
  "devDependencies": {
    "@bincode/jekpack": "^1.8.0"
  },
  "scripts": {
    "dev": "jekpack dev",
    "build": "jekpack build",
    "bundle": "jekpack bundle"
  }
}
```
- add `gem 'pry'` to Gemfile
- navigate to project folder `$ cd PROJECT_PATH`
- run `$ jekpack bundle`

**Start Dev Servers**

```sh
$ jekpack dev
```

Jekyll and Webpack are working together now.
All you need to know is only follow the Jekyll rules to code everything inside the src folder.
Read [Jekyll Documentation](https://jekyllrb.com/docs/pages/) for more details, if you are not familiar with it.

All files located at `assets` folder are managed by webpack.
For all files named `main.js`(inside assets/javascripts) and 
`main.scss`(inside assets/stylesheets) will be considered as entry files,
these files will be pack via webpack. 
In HTML, include these files via
`{% raw %}{% asset_tag main.css %}{% endraw %}`, 
`{% raw %}{% asset_tag main.js%}{% endraw %}`.
For example, a file located at `src/assets/stylesheets/some/page/main.scss` can be included via: 
```liquid
{% raw %}{% asset_tag some/page/main.css %}{% endraw %} 
```

**Build Distribution**

```sh
$ jekpack build
```

the default output location is `./dist`

**Deploy to S3**

```sh
$ jekpack deploy your-bucket-name
```

If you plan take S3 as website hosting. This command is helpful for you.
Be sure the environment variables
`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` are set already before you run the command.

For make life easier, you can create a file with name `.env`, which contains the following:
```
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
```
These environment variables will be loaded at the beginning of jekpack commands.

If you use CloudFront along with S3,
the argument `--cloud-front-id` can be used to create invalidations. 
```sh
jekpack deploy your-bucket-name --cloud-front-id your-cloud-front-id
```
