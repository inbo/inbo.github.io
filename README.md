# inbo.github.io

Organization site to redirect old GitHub Pages URLs.

## Problem

[Renaming](https://docs.github.com/en/repositories/creating-and-managing-repositories/renaming-a-repository) or [transferring](https://docs.github.com/en/repositories/creating-and-managing-repositories/transferring-a-repository) a repository has an impact on URLs:

- ✅ New repo URL `https://github.com/<new_org>/<new_repo>` is created.
- ✅ Old repo URL `https://github.com/<org>/<repo>` will automatically redirect to the new repo URL.
- ✅ New GitHub Pages URL `https://<new_org>.github.io/<new_repo>` is created.
- ❌ Old GitHub Pages URL `https://<org>.github.io/<repo>` returns a 404 error.

Any reference to the old Github Pages URL `https://<org>.github.io/<repo>` is now broken.

## Solution

This `https://github.com/<org>/<org>.github.io` repository has an associated [organization site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site#creating-a-repository-for-your-site), served from `https://<org>.github.io`. By creating subdirectories, we can redirect old GitHub Pages URLs:

1. Rename or transfer your `<repo>`. This will break the old GitHub Pages URL `https://<org>.github.io/<repo>`.
2. Create a directory in this repository, named `<repo>` (see the repo for examples).
3. Add an `index.html` to that directory, with the following content (replace the `URL` with the new GitHub Pages URL):

```html
<html>
  <head>
    <meta http-equiv="refresh" content="0;URL=https://<new_org>.github.io/<new_repo>/">
  </head>
</html>
```

4. Commit.
5. A page will now be served from the old GitHub Pages URL `https://<org>.github.io/<repo>/`. It will redirect without delay to the new GitHub Pages URL.

Note that only the homepage `https://<org>.github.io/<repo>/` will be redirected. This is typically sufficient, since subpages are seldom referenced elsewhere. To redirect subpages, either:

- Add a `404.html` with the same content as `index.html` to redirect all subpages to the new homepage.
- Add a `path/to/subpage/index.html` file (with specific `URL`) to redirect a specific subpage.
