## appendix

### How To Triger Auto Compile

This workflow `compile-release.yml` is already set up to automatically trigger when you push a tag to your Git repository that starts with the letter "v". Here's how it works:

* **`on:`**: This section defines the events that will trigger the workflow.
* **`push:`**: This specifies that the workflow will run when code is pushed.
* **`tags:`**: This further refines the `push` event to only trigger when tags are pushed.
* **`- 'v*'`**: This is a pattern that matches any tag that begins with the letter "v" (e.g., `v1.0`, `v0.5-beta`, `v2025.3.18`).

**Therefore, to automatically trigger the LaTeX compilation and release process, all you need to do is the following:**

1.  **Tag your commit:** In your local Git repository, create a tag for the commit you want to release. Make sure the tag name starts with "v". For example, you can use a command like:
    ```bash
    git tag v1.0
    ```
    You can replace `v1.0` with your desired tag name. You can also add a message to your tag:
    ```bash
    git tag -a v1.0 -m "Release version 1.0 of my LaTeX notes"
    ```

2.  **Push the tag:** Push the tag to your remote repository (e.g., GitHub, GitLab, Bitbucket):
    ```bash
    git push origin v1.0
    ```
    If you added a message to your tag with `-a`, you might need to use:
    ```bash
    git push origin --tags
    ```

Once you push a tag starting with "v", GitHub Actions will automatically detect this event and start running the `build-and-release` job defined in your workflow file. This will:

* Checkout your code.
* Set up the necessary LaTeX environment with Chinese fonts.
* Find all `note.tex` files in your repository's subdirectories.
* Compile each `note.tex` file into a PDF.
* Create a new release in your repository with the tag name.
* Upload all the compiled PDF files as assets to the release.
* Automatically generate release notes.

> [!IMPORTANT]
> The tag should be unique.