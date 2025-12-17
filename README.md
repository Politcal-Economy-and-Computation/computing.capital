# Political Economy of Computing Site

## Prerequisites
- `pnpm` to be able to run the project. Rest of dependencies will follow with install

## Getting started

First, clone the repo

To install dependencies, from repo root

```sh
pnpm install
```

For a dev server

```sh
pnpm dev
```

## To make edits

The site uses [SvelteKit](https://svelte.dev/docs/kit/introduction) + [Skeleton](https://www.skeleton.dev/docs/svelte/get-started/introduction) UI for theme and visual components. Familiarity with those is useful but not necessary.

If you want to make changes, please follow this procedure to handle branches and updating main:

1. Create a branch from main for new updates and features.
2. Make your edits.
3. Once done push the branch to remote and **submit a pull request to main.**

**Building and re-deployment is configured via netlify.**

### Editing members

To edit members, edit the `/static/data/members.json`. Each entry has format:

```json
{ 
    "name": "Karl M.", 
    "url": "https://en.wikipedia.org/wiki/Karl_Marx",
    "institution": "Out There"
}
```
