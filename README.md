# Build Vue and deploy it to Github Pages
This Action will Build your Vue Project and deploy it to Github Pages

## Getting Started

1.
- For Vue 2 : Create the `vue.config.js` file
- For Vue 3 : You should have a `vite.config.js` or a `vite.config.ts` file at the root of your directory. Create one if you don't.
2.
- For Vue 2 : Add this to your `vue.config.js` (and rename "YourRepoName" to your repo name)
```javascript
module.exports = {
    publicPath: '/YourRepoName/'
}
```
- For Vue 3 : Add this to you `vite.config.js` or `vite.config.ts` (and rename "YourRepoName" to your repo name)
```javascript
export default defineConfig({
  ... // Already existing configurations
  base: '/YourRepoName/'
});
```
3.
- Create a Github Actions Workflow file and add this to it (and replace "YourGithubName" and "YourRepoName" with the names)
```yml
name: Build Vue
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

permissions:
  contents: write # Permission for Action

jobs:
  build_vue:
    runs-on: ubuntu-latest
    name: Build Vue
    steps:
    - uses: actions/checkout@v2
    - id: Build-Vue
      uses: BitDEVil2K16/VuePagesAction@1.0.0
      with:
        username: 'YourGithubName'
        reponame: 'YourRepoName'
        token: ${{ secrets.GITHUB_TOKEN }} # Leave this line unchanged
```
4. Go to Settings -> Scroll down to GitHub Pages -> Select `gh-pages` as branch and `/` as directory 

## Options 🔧
|   Name   |            Description           |     Default    | Required |
|:--------:|:--------------------------------:|:--------------:|:--------:|
| username |           Your username          |        -       |     ✅    |
| reponame |       Your repository name       |        -       |     ✅    |
|   token  | Please leave this line unchanged |        -       |     ✅    |
| gitemail |         Git commit email         | CI@example.com |     ❌    |
|  gitname |          Git commit name         |       CI       |     ❌    |
|  gitmsg  |        Git commit message        |     deploy     |     ❌    |
|   cname  |           Custom domain          |        -       |     ❌    |
|  useyarn |         Use yarn to build        |      false     |     ❌    |

## Optional Custom Domain | cname
Change in ``package.json`` your Homepage and append cname in your yml.  
After token:
```yml
cname: 'yourcustomDomain.tdl'
```  

Full example with custom domain
```yml
name: Build React App

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

permissions:
  contents: write

jobs:
  build_react:
    runs-on: ubuntu-latest
    name: Build Vue
    steps:
    - uses: actions/checkout@v2
    - id: Build-Vue-App
      uses: BitDEVil2K16/VuePagesAction@1.0.0
      with:
        username: 'YourGithubName'
        reponame: 'YourRepoName'
        token: ${{ secrets.GITHUB_TOKEN }} # Leave this line unchanged
        cname: 'example.com'
```  

## License
The scripts and documentation in this project are released under the [MIT License](https://github.com/BitDEVil2K16/VuePagesAction/blob/master/LICENSE).
