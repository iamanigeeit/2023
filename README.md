# 10.020 Data Driven World

This is an experimental course website for 10.020 Data Driven World module.

You can contribute by forking this repository and creating pull requests 😊

## Getting Started (For your own use only)

1. Clone this project, then `npm install`
2. Afterwards, type `npm start`
3. You can publish this site to github automatically by pushing this to your `master` branch. See `.github/workflows/deploy.yml` action script
4. You need to give **read and write** Action permission in your workflow
   ![](images/README/2023-07-13-10-45-47.png)
5. Edit `docusaurus.config.js` accordingly to use on your site and deploy it on your repo, namely the `baseUrl`
6. The file `src/pages/index.js` contains the homepage. Edit it to your liking.

## How to Contribute

1. The website is built from files in this repo using Github workflows.
2. To contribute, fork this repo, then create `docusaurus.local.config.js` locally. This allows you to create a self-hosted site to test any changes.
3. In `docusaurus.local.config.js`, add this:
   ```javascript
   const config = {
       url: YOUR_NEW_URL,
       baseUrl: "/2023/", // or your new baseURL
       organizationName: YOUR_USERNAME,
       projectName: "2023", // or your new projectName
   }
   ```
4. If you want Github Pages to deploy the site for you, do:
   ```shell
   git add docusaurus.local.config.js
   git commit -m 'Local'
   git push
   ```
5. In Github > Actions, check that the workflow to build is triggered. If it doesn't work, you may need to set the permissions under Actions > General. When successful, Github should create a new branch `gh-pages` for the built website files and the site should be up at your given URL.
6. Now we should remove this `'Local'` commit to avoid it going into the PR for the upstream repo, but still retain `docusaurus.local.config.js` for Github Actions.
7. Add `docusaurus.local.config.js` to `.gitignore`. Run `git update-index --assume-unchanged .gitignore` to avoid committing the `.gitignore` itself.
8. On your next change, amend the `'Local'` commit:
   ```shell
   git add .
   git commit --amend -m 'First change'
   git push --force
   ```
9. Now, your commit history should not contain `docusaurus.local.config.js`, but should have your new changes. Then you can start the pull request.


## Building Locally

1. If you have admin / sudo rights to your workstation, it could be easier to build the site locally.
2. [Install Node Version Manager](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm), reopen Terminal and `nvm install 18`. Important: you **must** install Node v18 because v20 breaks Docusaurus!
3. Clone this project, `cd` to the root folder and run `nvm install`.
4. Run `npm start`. The site should be up.


## Possible Customizations

1. The file `src/pages/index.js` contains the homepage. Edit it to your liking.
2. Add icons to /static/img
3. Add setting to the docusaurus search local to include other docs route base path like psets labs etc
4. Enable brython `npm i docusaurus-live-brython`
5. Swizzled Admonitions: see `docusaurus.config.js`
6. Custom components: see `src/components`

## Markdown features

### Admonitions

You can generate admonitions using:

```
:::[keyword]
<your content>
:::
```

where `[keyword]` can be any of the following:

```
keywords: [
    "info",
    "success",
    "danger",
    "note",
    "tip",
    "warning",
    "important",
    "caution",
    "keyword",
    "think",
],
```

Edit `/src/theme/Admonition.index.js` to add more custom admonition, and add it in `docusaurus.config.js`.

### Custom markdown snippets and Keybinding

It's advisable to add custom markdown snippets as follows in your VSCode's `markdown.json`:

````
...
  "Red block": {
    "prefix": "redwords",
    "body": [
      "<span style={{ \"color\":\"red\", \"fontWeight\": \"bold\" }}>$TM_SELECTED_TEXT$1</span>"
    ],
    "description": "custom redword block"
  },
    "Image Block React": {
    "prefix": "imageblockreact",
    "body": [
      "<ImageCard path={require(\"./$1\").default} widthPercentage=\"70%$2\"/>"
    ],
    "description": "custom image block in React"
  },
  "Image Block React With Prefix": {
    "prefix": "imageblockreactwithprefix",
    "body": [
      "<ImageCard path={require(\"./images/$1\").default} widthPercentage=\"70%$2\"/>"
    ],
    "description": "custom image block in React with prefix"
  },
  "Deep Dive React": {
    "prefix": "deepdivereact",
    "body": [
      "<DeepDive title=\"Show Pseudocode\">\n\n$1\n```\n$2\n```\n\n</DeepDive>\n$3"
    ],
    "description": "custom deepdive block in React"
  },
  "Front Matter MDX": {
    "prefix": "frontmattermdx",
    "body": [
      "---\nsidebar_position: $1\n---\n\nimport CollapsibleAnswer from '@site/src/components/CollapsibleAnswer';\nimport DeepDive from '@site/src/components/DeepDive';\nimport ImageCard from '@site/src/components/ImageCard';\nimport ChatBaseBubble from \"@site/src/components/ChatBaseBubble\";\n\n$2\n\n<ChatBaseBubble/>\n\n$3"
    ],
    "description": "custom yaml frontmatter block"
  },
  "Keywords React": {
    "prefix": "keywordsreact",
    "body": [":::keyword Keywords\n$1\n:::"],
    "description": "custom keyword admonition"
  },
  "Admonitions React": {
    "prefix": "admonitionsreact",
    "body": [":::$1\n$2\n:::"],
    "description": "shortcut admonition"
  }
  ...
````

Then bind it to a keyboard shortcut in VSCode's `keybindings.json`:

```
...
  {
    "key": "ctrl+alt+e",
    "command": "editor.action.insertSnippet",
    "args": {
      "name": "Image Block React"
    },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+g",
    "command": "editor.action.insertSnippet",
    "args": {
      "name": "Image Block React With Prefix"
    },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+d",
    "command": "editor.action.insertSnippet",
    "args": {
      "name": "Deep Dive React"
    },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+f",
    "command": "editor.action.insertSnippet",
    "args": {
      "name": "Front Matter MDX"
    },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  {
    "key": "ctrl+alt+o",
    "command": "editor.action.insertSnippet",
    "args": {
      "name": "Keywords React"
    },
    "when": "editorTextFocus && markdownShortcuts:enabled"
  },
  ...
```

### Images

Images should be placed in the same directory as the markdown file, inside `/images` folder. See `/docs` for reference.

VSCode extension: `mushan.vscode-paste-image` is immensely useful. [You can install it from here](https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image).

You can then bind it to some key to paste image on your clipboard:

```
  {
    "key": "ctrl+alt+v",
    "command": "extension.pasteImage",
    "when": "editorTextFocus"
  },
```

Then set the extension settings as follows:

![](/images/README/2023-07-13-10-54-53.png)

![](/images/README/2023-07-13-10-56-14.png)

This way, the extension is going to paste simply the path from current working directory, like `/images/bfs/2023-07-13-10-58-22.png` into `ImageBlock` component.

## Adding new folder

Lecture notes goes to `docs` folder by default. But, you can create new folder in the root, such as `projects`, `labs`, etc. First, create an entry point: `intro.md` (or any other name, just match it when declaring it in docusaurus config later) inside the new folder.

Now update `docusaurus.config.js`.

**Step 1**: register it under `@docusaurus/plugin-content-docs`:

```
  plugins: [
    [
      "@docusaurus/plugin-content-docs",
      {
        id: "projects",
        path: "projects",
        routeBasePath: "projects",
        sidebarPath: require.resolve("./sidebars.js"),
      },
    ],
    [
      "@docusaurus/plugin-content-docs",
      {
        id: "your-folder-name",
        path: "your-folder-name",
        routeBasePath: "your-folder-name",
        sidebarPath: require.resolve("./sidebars.js"),
      },
    ],
```

**Step 2**: under `themes`, register it as `docsRouteBasePath`:

```
  themes: [
    [
      require.resolve("@easyops-cn/docusaurus-search-local"),
      {
        docsRouteBasePath: ["projects", "notes", "about", "your-folder-name..."],
      },
    ],
```

**Step 3**: update the navbar to include your new folder:

```
      navbar: {
        hideOnScroll: true,
        title: "10.020",
        logo: {
          alt: "DDW Logo",
          src: "img/home-logo.svg",
        },
        items: [
          {
            type: "search",
            position: "right",
          },
          {
            to: "/about/intro",
            label: "About",
            position: "left",
            activeBaseRegex: `/about/`,
          },
          {
            to: "/your-folder-name/intro",
            label: "Navbar-Label",
            position: "left",
            activeBaseRegex: `/your-folder-name/`,
          },
          ...
        ]
        ...
      }
```
