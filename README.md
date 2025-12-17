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

1. Please create a branch from main for new updates and features
2. Once done, submit a pull request to main

Building and deployment is configured via netlify.

### Editing members

To edit members, edit the `/static/data/members.json`. Each entry has format:

```json
{ 
    "name": "Karl M.", 
    "url": "https://en.wikipedia.org/wiki/Karl_Marx",
    "institution": "Out There"
}
```
