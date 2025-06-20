
on:
  push:
    branches: [ "main" ]
    paths:   
      - 'index.html'
      - '.github/workflows/**'
on: Specifies what triggers this workflow.

push: The workflow runs when you push commits.

branches: Limits the workflow to only run on pushes to the main branch.

paths: The workflow only triggers if files matching these paths changed:

'index.html' (your webpage)

Any files in .github/workflows/ directory (your workflow YAML files)

This helps avoid running the workflow unnecessarily if unrelated files change.


permissions:
  contents: read
  pages: write
  id-token: write
permissions: Defines what permissions the workflow token has.

contents: read allows the workflow to read repository contents (code, files).

pages: write allows the workflow to deploy (write) to GitHub Pages.

id-token: write is used for authentication with GitHub's API or other identity features.


jobs:
  build_and_deploy:
    runs-on: ubuntu-latest
jobs: Defines one or more tasks (jobs) the workflow will run.

build_and_deploy: is the ID of the job (you can name it anything but no spaces).

runs-on: ubuntu-latest tells GitHub Actions to use the latest Ubuntu Linux virtual machine for running this job.






   steps:
      - name: Checkout repository
        uses: actions/checkout@v4
steps: Lists the sequential steps inside the job.

This step checks out (downloads) your repository's code into the runner, so the workflow can access your files like index.html.

uses: points to a pre-made action from GitHub Marketplace (actions/checkout@v4 is the standard action to checkout code).



      - name: Set up GitHub Pages
        uses: actions/configure-pages@v5
This sets up the environment specifically for GitHub Pages deployment.

actions/configure-pages@v5 prepares authentication and environment so you can deploy to GitHub Pages properly.


      - name: Upload static web page
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
This step uploads your static site files as an artifact for deployment.

actions/upload-pages-artifact@v3 takes files and packages them for GitHub Pages deployment.

path: '.' means it will upload everything in the root directory (including your index.html).


   - name: Deploy to GitHub Pages
        uses: actions/deploy-pages@v4
This is the final deployment step.

actions/deploy-pages@v4 takes the uploaded artifact and publishes it to GitHub Pages.

After this step completes, your site is live at the GitHub Pages URL.
