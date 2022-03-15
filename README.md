# inbo.github.io

An organization-level inbo.github.io website to allow URL redirects when our repositories have been renamed or moved.

## Rationale

Adapted from https://gist.github.com/domenic/1f286d415559b56d725bee51a62c24a7: 

### The problem

We have a repository, e.g. `inbo/repo`. We would like to rename it to `inbo/repo-new` or transfer it to the organization `trias-project`, so it will become `trias-project/repo`.

However, we make heavy use of the [GitHub Pages](https://pages.github.com/) feature for that repository, so that people are often accessing `https://inbo.github.io/repo/`. GitHub will [helpfully redirect](https://github.com/blog/1508-repository-redirects-are-here) all of our repository stuff hosted on github.com after the move, but will not redirect the GitHub Pages hosted on github.io.

### The solution

We solve this by having this `inbo/inbo.github.io` repository, which creates an organization-level `https://inbo.github.io` GitHub Pages website. We now can:

1. Rename or transfer the repository, thus breaking all the links
2. Add a file `repo/index.html` to this repository, which uses `<meta http-equiv="refresh">` to redirect to the new URL. The `index.html` file should look like this (also documented in the [rOpenSci devguide](https://devguide.ropensci.org/redirect.html)):

    ```html
    <html>
      <head>
        <meta http-equiv="refresh" content="0;URL=https://inbo.github.io/camtraptor/">
      </head>
    </html>
    ```

Once done, `https://inbo.github.io/repo/` will still exists as a working URL, even though the `inbo/repo` repository does not. And it will redirect to the new URL.
