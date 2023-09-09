# 🧪 Alchemy Docs

The Alchemy docs are hosted at [alchemyswift.com](https://alchemyswift.com/) and powered by [Mintlify](https://mintlify.com).

You can submit fixes or updates via PR to this repo.

### 👩‍💻 Development

Install the [Mintlify CLI](https://www.npmjs.com/package/mintlify) to preview the documentation changes locally. To install, use the following command

```
npm i -g mintlify
```

Run the following command at the root of your documentation (where mint.json is)

```
mintlify dev
```

### 😎 Publishing Changes

Changes will be deployed to production automatically after pushing to the main branch.

You can also preview changes using PRs, which generates a preview link of the docs.

#### Troubleshooting

-   Mintlify dev isn't running - Run `mintlify install` it'll re-install dependencies.
-   Page loads as a 404 - Make sure you are running in a folder with `mint.json`
