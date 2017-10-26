# inbo.github.io

An organization-level inbo.github.io website to allow URL redirects when repositories have been renamed or moved. Note: the content of this repository is public at https://inbo.github.io.

Adapted from https://gist.github.com/domenic/1f286d415559b56d725bee51a62c24a7: 

## The problem

You have a repository, e.g. `inbo/repo`. You would like to rename it to `inbo/repository` or transfer it to the organization `trias-project`, so it will become `trias-project/repo`.

However, you make heavy use of the [GitHub Pages](https://pages.github.com/) feature, so that people are often accessing `https://inbo.github.io/repo/`. GitHub will [helpfully redirect](https://github.com/blog/1508-repository-redirects-are-here) all of your repository stuff hosted on github.com after the move, but will not redirect the GitHub Pages hosted on github.io.

## The solution

We solve this by:

1. Moving the repository, thus breaking all the links
2. Having this `inbo/inbo.github.io` repository, which creates an organization-level `https://inbo.github.io` GitHub Pages site
3. Adding a file `repo/index.html` to this repository, which uses `<meta http-equiv="refresh">` to redirect to the new URL. It should look like this:

    ```html
    <!DOCTYPE html>
    <meta charset="utf-8">
    <title>Redirecting to new URL</title>
    <meta http-equiv="refresh" content="0; URL=https://trias-project.github.io/repo/">
    <link rel="canonical" href="https://trias-project.github.io/repo/">
    ```

This means that `https://inbo.github.io/repo/` still exists as a working URL, even though the `inbo/repo` repository does not. And it will redirect to the new URL, e.g. `https://inbo.github.io/repository` (for rename) or `https://trias-project.github.io/repo/` (for transfer).
