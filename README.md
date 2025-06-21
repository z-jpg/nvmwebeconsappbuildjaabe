//npm.pkg.github.com/:_authToken=TOKEN
$ npm login --scope=@NAMESPACE --auth-type=legacy --registry=https://npm.pkg.github.com

> Username: USERNAME
> Password: TOKEN
@NAMESPACE:registry=https://npm.pkg.github.com

$ git add .
# Adds the file to your local repository and stages it for commit. To unstage a file, use 'git reset HEAD YOUR-FILE'.

$ git commit -m "Add existing file"
# Commits the tracked changes and prepares them to be pushed to a remote repository. To remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again.

$ git push origin YOUR_BRANCH
# Pushes the changes in your local repository up to the remote repository you specified as the origin

@my-org/test.

https://github.com/my-org/test.git.
npm publish

"publishConfig": {
  "registry": "https://npm.pkg.github.com"
},
https://github.com/my-org/test.git.
npm publish

#
name: Create and publish a Docker image

# Configures this workflow to run every time a change is pushed to the branch called `release`.
on:
  push:
    branches: ['release']

# Defines two custom environment variables for the workflow. These are used for the Container registry domain, and a name for the Docker image that this workflow builds.
env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}

# There is a single job in this workflow. It's configured to run on the latest available version of Ubuntu.
jobs:
  build-and-push-image:
    runs-on: ubuntu-latest
    # Sets the permissions granted to the `GITHUB_TOKEN` for the actions in this job.
    permissions:
      contents: read
      packages: write
      attestations: write
      id-token: write
      #
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      # Uses the `docker/login-action` action to log in to the Container registry registry using the account and password that will publish the packages. Once published, the packages are scoped to the account defined here.
      - name: Log in to the Container registry
        uses: docker/login-action@65b78e6e13532edd9afa3aa52ac7964289d1a9c1
        with:
          registry: ${{ env.REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      # This step uses [docker/metadata-action](https://github.com/docker/metadata-action#about) to extract tags and labels that will be applied to the specified image. The `id` "meta" allows the output of this step to be referenced in a subsequent step. The `images` value provides the base name for the tags and labels.
      - name: Extract metadata (tags, labels) for Docker
        id: meta
        uses: docker/metadata-action@9ec57ed1fcdbf14dcef7dfbe97b2010124a938b7
        with:
          images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
      # This step uses the `docker/build-push-action` action to build the image, based on your repository's `Dockerfile`. If the build succeeds, it pushes the image to GitHub Packages.
      # It uses the `context` parameter to define the build's context as the set of files located in the specified path. For more information, see [Usage](https://github.com/docker/build-push-action#usage) in the README of the `docker/build-push-action` repository.
      # It uses the `tags` and `labels` parameters to tag and label the image with the output from the "meta" step.
      - name: Build and push Docker image
        id: push
        uses: docker/build-push-action@f2a1d5e99d037542a71f64918e516c093c6f3fc4
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
      
      # This step generates an artifact attestation for the image, which is an unforgeable statement about where and how it was built. It increases supply chain security for people who consume the image. For more information, see [Using artifact attestations to establish provenance for builds](/actions/security-guides/using-artifact-attestations-to-establish-provenance-for-builds).
      - name: Generate artifact attestation
        uses: actions/attest-build-provenance@v2
        with:
          subject-name: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME}}
          subject-digest: ${{ steps.push.outputs.digest }}
          push-to-registry: true
      

"repository":"https://github.com/OWNER/REPOSITORY",

{
  "name": "@my-org/server",
  "version": "1.0.0",
  "description": "Server app that uses the ORGANIZATION_NAME/PACKAGE_NAME package",
  "main": "index.js",
  "author": "",
  "license": "MIT",
  "dependencies": {
    "ORGANIZATION_NAME/PACKAGE_NAME": "1.0.0"
  }
}
npm install

@NAMESPACE:registry=https://npm.pkg.github.com
@NAMESPACE:registry=https://npm.pkg.github.com

#
name: Demo Push

# This workflow runs when any of the following occur:
# - A push is made to a branch called `main` or `seed`
# - A tag starting with "v" is created
# - A pull request is created or updated
on:
  push:
    branches:
      - main
      - seed
    tags:
      - v*
  pull_request:
  # This creates an environment variable called `IMAGE_NAME ` with the value `ghtoken_product_demo`.
env:
  IMAGE_NAME: ghtoken_product_demo
#
jobs:
  # This pushes the image to GitHub Packages.
  push:
    runs-on: ubuntu-latest
    permissions:
      packages: write
      contents: read
      #
    steps:
      - uses: actions/checkout@v4

      - name: Build image
        run: docker build . --file Dockerfile --tag $IMAGE_NAME --label "runnumber=${GITHUB_RUN_ID}"

      - name: Log in to registry
        run: echo "${{ secrets.GITHUB_TOKEN }}" | docker login ghcr.io -u ${{ github.actor }} --password-stdin
        #
      - name: Push image
        run: |
          IMAGE_ID=ghcr.io/${{ github.repository_owner }}/$IMAGE_NAME

          # This changes all uppercase characters to lowercase.
          IMAGE_ID=$(echo $IMAGE_ID | tr '[A-Z]' '[a-z]')
          # This strips the git ref prefix from the version.
          VERSION=$(echo "${{ github.ref }}" | sed -e 's,.*/\(.*\),\1,')
          # This strips the "v" prefix from the tag name.
          [[ "${{ github.ref }}" == "refs/tags/"* ]] && VERSION=$(echo $VERSION | sed -e 's/^v//')
          # This uses the Docker `latest` tag convention.
          [ "$VERSION" == "main" ] && VERSION=latest
          echo IMAGE_ID=$IMAGE_ID
          echo VERSION=$VERSION
          docker tag $IMAGE_NAME $IMAGE_ID:$VERSION
          docker push $IMAGE_ID:$VERSIONs











#!/usr/bin/env bash

set -e

echo 'Updating test mocks...'

MOCKS_DIR="$PWD/test/fast/Unit tests/mocks"

echo "creating $MOCKS_DIR"
mkdir -p "$MOCKS_DIR"

\. "$NVM_DIR/nvm.sh" --no-use
nvm deactivate 2> /dev/null
nvm_is_version_installed() {
  return 1
}

nvm_make_alias() {
  # prevent local alias creation
  return 0
}

nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote.txt"
nvm_ls_remote_iojs > "$MOCKS_DIR/nvm_ls_remote_iojs.txt"
NVM_LTS=* nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote LTS.txt"
NVM_LTS=argon nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote LTS argon.txt"
nvm_download -L -s "https://nodejs.org/download/nightly/index.tab" -o - > "$MOCKS_DIR/nodejs.org-download-nightly-index.tab"
nvm_download -L -s "$(nvm_get_mirror iojs std)/index.tab" -o - > "$MOCKS_DIR/iojs.org-dist-index.tab"
NVM_COLORS=0ygre nvm ls-remote > "$MOCKS_DIR/nvm ls-remote.txt"
NVM_COLORS=0ygre nvm ls-remote --lts > "$MOCKS_DIR/nvm ls-remote lts.txt"
NVM_COLORS=0ygre nvm ls-remote node > "$MOCKS_DIR/nvm ls-remote node.txt"
NVM_COLORS=0ygre nvm ls-remote iojs > "$MOCKS_DIR/nvm ls-remote iojs.txt"
nvm_print_implicit_alias remote stable > "$MOCKS_DIR/nvm_print_implicit_alias remote stable.txt"
nvm_ls_remote stable > "$MOCKS_DIR/nvm_ls_remote stable.txt"
nvm alias "lts/*" > "$MOCKS_DIR/lts-star.txt"

set +e
NVM_NODEJS_ORG_MIRROR=https://nodejs.org/download/nightly/ nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote nightly.txt"
nvm_download -L -s "$(nvm_get_mirror node std)/index.tab" -o - > "$MOCKS_DIR/nodejs.org-dist-index.tab"
NVM_NODEJS_ORG_MIRROR=https://nodejs.org/download/nightly/ nvm_print_implicit_alias remote stable > "$MOCKS_DIR/nvm_print_implicit_alias remote stable nightly.txt"
NVM_NODEJS_ORG_MIRROR=https://nodejs.org/download/nightly/ nvm_ls_remote stable > "$MOCKS_DIR/nvm_ls_remote stable nightly.txt"
NVM_NODEJS_ORG_MIRROR=https://nodejs.org/download/nightly/ NVM_LTS=* nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote LTS nightly.txt"
NVM_NODEJS_ORG_MIRROR=https://nodejs.org/download/nightly/ NVM_LTS=argon nvm_ls_remote > "$MOCKS_DIR/nvm_ls_remote LTS nightly argon.txt"
set -e

ALIAS_PATH="$MOCKS_DIR/nvm_make_alias LTS alias calls.txt"
: > "$ALIAS_PATH"
LTS_NAMES_PATH="$MOCKS_DIR/LTS_names.txt"
: > "$LTS_NAMES_PATH"
nvm_make_alias() {
  # prevent local alias creation, and store arguments
  echo "${1}|${2}" >> "$ALIAS_PATH"
  if [ "${1}" != 'lts/*' ]; then
    echo "${1#lts/}" >> "$LTS_NAMES_PATH"
  fi
}
nvm ls-remote --lts > /dev/null

echo "done! Don't forget to git commit them."

4b4154ea040349bfd40215ec4e4cc9f372fe95f3# nvmwebeconsappbuildjaabe
nvm webeconsappbuildjaabe
# NVM Web – Minimal Starter

# Contributing to the Firebase JS SDK

We'd love for you to contribute to our source code and to help make the Firebase JS SDK even better
than it is today! Here are the guidelines we'd like you to follow:

 - [Code of Conduct](#coc)
 - [Question or Problem?](#question)
 - [Issues and Bugs](#issue)
 - [Submission Guidelines](#submit)
 - [Updating Documentation](#docs)

## <a name="coc"></a> Code of Conduct

As contributors and maintainers of the Firebase JS SDK project, we pledge to respect everyone who
contributes by posting issues, updating documentation, submitting pull requests, providing feedback
in comments, and any other activities.

Communication through any of Firebase's channels (GitHub, StackOverflow, X, etc.)
must be constructive and never resort to personal attacks, trolling, public or private harassment,
insults, or other unprofessional conduct.

We promise to extend courtesy and respect to everyone involved in this project regardless of gender,
gender identity, sexual orientation, disability, age, race, ethnicity, religion, or level of
experience. We expect anyone contributing to the project to do the same.

If any member of the community violates this code of conduct, the maintainers of the Firebase JS SDK
project may take action, removing issues, comments, and PRs or blocking accounts as deemed
appropriate.

If you are subject to or witness unacceptable behavior, or have any other concerns, please drop us a
line at firebase-code-of-conduct@google.com.

## <a name="question"></a> Got a Question?

If you have questions about how to use the Firebase JS SDK, please direct these to
[StackOverflow][stackoverflow] and use the `firebase` and `javascript` tags. You can also use the
[Firebase Google Group][firebase-google-group] or [Slack][slack] to contact members of the Firebase
team for help.

## <a name="issue"></a> Found an Issue?

If you find a bug in the source code, a mistake in the documentation, or some other issue, you can
help us by submitting an issue to our [GitHub Repository][github]. Even better you can submit a Pull
Request with a test demonstrating the bug and a fix!

See [below](#submit) for some guidelines.

## <a name="other-issue"></a> Production Issues

If you have a production issue, please [contact Firebase support][support] who will work with you to
resolve the issue.

## <a name="submit"></a> Submission Guidelines

### Submitting an Issue

Before you submit your issue, try searching [past issues][archive], [StackOverflow][stackoverflow],
and the [Firebase Google Group][firebase-google-group] for issues similar to your own. You can help
us to maximize the effort we spend fixing issues, and adding new features, by not reporting
duplicate issues.

If you encounter an issue that appears to be a bug that has not been reported before, please
[open a new issue in the repo](https://github.com/firebase/firebase-js-sdk/issues/new/choose). When
filling out the new issue report form, be sure to include as much information as possible, such as
reproduction steps, the error message you received, and any screenshots or other relevant data. The
more context you can provide the better we will be able to understand the issue, route it to the
appropriate team, and provide you with the help you need.

Also as a great rule of thumb:

**If you get help, help others. Good karma rulez!**

## Before you Contribute

### Sign our Contributor License Agreement

Contributions to this project must be accompanied by a
[Contributor License Agreement](https://cla.developers.google.com/about) (CLA).
You (or your employer) retain the copyright to your contribution; this simply
gives us permission to use and redistribute your contributions as part of the
project.

If you or your current employer have already signed the Google CLA (even if it
was for a different project), you probably don't need to do it again.

Visit <https://cla.developers.google.com/> to see your current agreements or to
sign a new one.

### Review our community guidelines

This project follows
[Google's Open Source Community Guidelines](https://opensource.google/conduct/).

### Submitting a Pull Request

All submissions, including submissions by project members, require review. We use GitHub pull
requests for this purpose. Consult
[GitHub Help](https://help.github.com/articles/about-pull-requests/) for more information on using
pull requests.

If you plan to work on a larger contribution, you should get in touch with us first through the
issue tracker with your idea so that we can help out and possibly guide you. Coordinating up front
makes it much easier to avoid frustration later on. Some pull requests (large contributions, API
additions/changes, etc) may be subject to additional internal review, we appreciate your patience as
we fully validate your contribution.

#### Pull Request Guidelines

* Search [GitHub](https://github.com/firebase/firebase-js-sdk/pulls) for an open or closed Pull
Request that relates to your submission. You don't want to duplicate effort.
* Create an issue to discuss a change before submitting a PR. We'd hate to have to turn down your
contributions because of something that could have been communicated early on.
* [Create a fork of the GitHub repo][fork-repo] to ensure that you can push your changes for us to
review.
* Make your changes in a new git branch:

  ```shell
  git checkout -b my-fix-branch main
  ```

* Create your change, **including appropriate test cases**. Changes with tests are more likely to be
merged.
* Avoid checking in files that shouldn't be tracked (e.g `node_modules`, `gulp-cache`, `.tmp`,
`.idea`). If your development setup automatically creates some of these files, please add them to
the `.gitignore` at the root of the package (click [here][gitignore] to read more on how to add
entries to the `.gitignore`).
* Commit your changes

     ```shell
     git commit -a
     ```
  _Note: the optional commit `-a` command line option will automatically "add" and "rm" edited
  files._

* Test your changes locally to ensure everything is in good working order:

    ```shell
   npm test
    ```

* Push your branch to your fork on GitHub:

    ```shell
    git push origin my-fix-branch
    ```

* In GitHub, create a pull request against the `firebase-js-sdk:main` branch.
* Add changeset. See [Adding changeset to PR](#adding-changeset-to-pr).
* All pull requests must be reviewed by a member of the Firebase JS SDK team, who will merge it
when/if they feel it is good to go.

That's it! Thank you for your contribution!

#### Adding changeset to PR
The repository uses changesets to associate PR contributions with major and minor version releases
and patch releases. If your change is a feature or a behavioral change (either of which should
correspond to a version bump) then you will need to generate a changeset in your PR to track the
change.

Start the changeset creation process by running the following command in the base directory of the
repository:

```shell
yarn changeset
```

You will be asked to create a description (here's an [example](https://github.com/firebase/firebase-js-sdk/pull/3284#issuecomment-649718617)). You
should include the version bump for your package as well as the description for the change. Valid
version bump types are major, minor or patch, where:

 * a major version is an incompatible API change
 * a minor version is a backwards compatible API change
 * a patch version is a backwards compatible bug fix or any change that does not affect the API. A
   refactor, for example.

Please always include the firebase package with the same version bump type as your package. This is
to ensure that the version of the firebase package will be bumped correctly, 

 For example,

```
---
"@firebase/storage": minor
"firebase": minor
---

This is a test.
```

You do not need to create a Changeset for the following changes:

 * the addition or alteration of a test
 * documentation updates
 * updates to the repository’s CI

#### Multiple changeset files

If your PR touches multiple SDKs or addresses multiple issues that require
different version bump or different description, you can create multiple
changeset files in the PR.

## <a name="docs"></a> Updating Documentation

Reference docs for the Firebase [JS SDK](https://firebase.google.com/docs/reference/js/) and
[Node (client) SDK](https://firebase.google.com/docs/reference/node/) are generated by
[Typedoc](https://typedoc.org/).

Typedoc generates this documentation from the main
[firebase index.d.ts type definition file](packages/firebase/compat/index.d.ts).  Any updates to
documentation should be made in that file.

If any pages are added or removed by your change (by adding or removing a class or interface), the
[js/toc.yaml](scripts/docgen/content-sources/js/toc.yaml) and/or
[node/toc.yaml](scripts/docgen/content-sources/node/toc.yaml) need to be modified to reflect this.

# Formatting Code
A Formatting Check CI failure in your PR indicates that the code does not follow the repo's
formatting guidelines. In your local build environment, please run the code formatting tool locally
by executing the command `yarn format`. Once the code is formatted, commit the changes and push your
branch. The push should cause the CI to re-check your PR's changes.

# Generating Documentation HTML Files

If the Doc Change Check fails in your PR, it indicates that the documentation has not been generated
correctly for the changes. In your local build environment, please run the following commands in the
root directory to generate the documentation locally:

```
yarn
yarn docgen:all
```

This will generate reference docs and the toc in `docs-devsite/`. Commit and push the generated
documentation changes to GitHub following the [PR submission guidelines](#submit). Your push
to the remote repository should force any failing documentation checks to execute again.

**NOTE:** These files are formatted to be inserted into Google's documentation site, which adds some
styling and navigation, so the raw files will be missing navigation elements and may not look
polished. However, it should be enough to preview the content.

[archive]: https://github.com/firebase/firebase-js-sdk/issues?utf8=%E2%9C%93&q=is%3Aissue
[file-an-issue]: https://github.com/firebase/firebase-js-sdk/issues/new
[firebase-google-group]: https://groups.google.com/forum/#!forum/firebase-talk
[fork-repo]: https://github.com/firebase/firebase-js-sdk/fork
[github]: https://github.com/firebase/firebase-js-sdk
[gitignore]: https://git-scm.com/docs/gitignore
[google-cla]: https://cla.developers.google.com/about/google-individual
[js-style-guide]: http://google.github.io/styleguide/javascriptguide.xml
[jsbin]: http://jsbin.com/rinilu/edit?js,console
[slack]: https://firebase-community.appspot.com/
[stackoverflow]: http://stackoverflow.com/questions/tagged/firebase
[support]: https://firebase.google.com/support/

## Features

- **Backend (Node.js/Express):** REST API for nvm commands (list Node.js versions)
- **Frontend (React):** Displays Node.js versions from backend
- **Dockerized:** Run both with `docker-compose up`

## Quick Start
# nvm-web Google Cloud Quickstart

This guide shows how to deploy your nvm-web project (Node.js backend + React frontend, both in Docker) to Google Cloud using **Cloud Run**.

---

## Prerequisites

- [Google Cloud account](https://console.cloud.google.com/)
- [Google Cloud SDK (gcloud) installed](https://cloud.google.com/sdk/docs/install)
- [Docker installed](https://docs.docker.com/get-docker/)
- Your project code ready in two folders: `backend/` and `frontend/`

---

## 1. Set Up Google Cloud

```bash
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
gcloud config set run/region YOUR_REGION
```

---

## 2. Enable Required APIs

```bash
gcloud services enable run.googleapis.com artifactregistry.googleapis.com
```

---

## 3. Build & Push Docker Images

1. **Create Artifact Registry:**

   ```bash
   gcloud artifacts repositories create nvm-web-repo --repository-format=docker --location=YOUR_REGION
   ```

2. **Build and Push Backend:**

   ```bash
   docker build -t YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-backend:latest ./backend
   docker push YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-backend:latest
   ```

3. **Build and Push Frontend:**

   ```bash
   docker build -t YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-frontend:latest ./frontend
   docker push YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-frontend:latest
   ```

---

## 4. Deploy to Cloud Run

1. **Deploy Backend:**

   ```bash
   gcloud run deploy nvm-web-backend \
     --image YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-backend:latest \
     --platform managed \
     --allow-unauthenticated \
     --port 4000
   ```

2. **Deploy Frontend:**

   ```bash
   gcloud run deploy nvm-web-frontend \
     --image YOUR_REGION-docker.pkg.dev/YOUR_PROJECT_ID/nvm-web-repo/nvm-web-frontend:latest \
     --platform managed \
     --allow-unauthenticated \
     --port 80
   ```

---

## 5. Access Your Services

- After deployment, Cloud Run will give you unique URLs for frontend and backend.
- Set your frontend to use the backend’s URL for API calls (edit `.env` or config before building frontend).

---

## 6. (Optional) Use a Custom Domain

- [Map a custom domain to your Cloud Run services](https://cloud.google.com/run/docs/mapping-custom-domains).
- Set up HTTPS automatically with Google-managed certificates.

---

## 7. Clean Up

To avoid charges:

```bash
gcloud run services delete nvm-web-backend
gcloud run services delete nvm-web-frontend
gcloud artifacts repositories delete nvm-web-repo --location=YOUR_REGION
```

---

## Resources

- [Cloud Run Quickstart](https://cloud.google.com/run/docs/quickstarts)
- [Artifact Registry Quickstart](https://cloud.google.com/artifact-registry/docs/docker/quickstart)
- [Cloud Run Custom Domains](https://cloud.google.com/run/docs/mapping-custom-domains)

---

**You’re ready!** 🚀

1. **Install Docker & Docker Compose**
2. `docker-compose up --build`
3. Visit:
   - Backend: [http://localhost:4000/api/nvm/versions](http://localhost:4000/api/nvm/versions)
   - Frontend: [http://localhost:3000](http://localhost:3000)

_Note: For nvm commands to work, nvm must be installed on the backend container or host. For development, you may want to run backend locally with nvm installed._

## Next Steps

- Add more nvm features (install, uninstall, switch)
- Add authentication
- Improve error handling and UI
- Skip to main content
Firebase
More
Search
/


English
Blog
Studio
Go to console
Sign in
Documentation
Overview
Fundamentals

AI

Build

Run

Reference
Samples
Filter

Here's everything we announced at I/O, from new Firebase Studio features to more ways to integrate AI. Read blog.
Firebase
Documentation
Reference
Was this helpful?

Send feedbackFirebase CLI reference 

bookmark_border


The Firebase CLI (GitHub) provides a variety of tools for managing, viewing, and deploying to Firebase projects.

Before using the Firebase CLI, set up a Firebase project.

Set up or update the CLI
Install the Firebase CLI
You can install the Firebase CLI using a method that matches your operating system, experience level, and/or use case. Regardless of how you install the CLI, you have access to the same functionality and the firebase command.

Windows macOS Linux

Windows
You can install the Firebase CLI for Windows using one of the following options:

Option	Description	Recommended for...
standalone binary	Download the standalone binary for the CLI. Then, you can access the executable to open a shell where you can run the firebase command.	New developers

Developers not using or unfamiliar with Node.js
npm	Use npm (the Node Package Manager) to install the CLI and enable the globally available firebase command.	Developers using Node.js
standalone binary
npm
To download and run the binary for the Firebase CLI, follow these steps:

Download the Firebase CLI binary for Windows.

Access the binary to open a shell where you can run the firebase command.

Continue to log in and test the CLI.

macOS or Linux
You can install the Firebase CLI for macOS or Linux using one of the following options:

Option	Description	Recommended for...
automatic install script	Run a single command that automatically detects your operating system, downloads the latest CLI release, then enables the globally available firebase command.	New developers

Developers not using or unfamiliar with Node.js

Automated deploys in a CI/CD environment
standalone binary	Download the standalone binary for the CLI. Then, you can configure and run the binary to suit your workflow.	Fully customizable workflows using the CLI
npm	Use npm (the Node Package Manager) to install the CLI and enable the globally available firebase command.	Developers using Node.js
auto install script
standalone binary
npm
To install the Firebase CLI using the automatic install script, follow these steps:

Run the following cURL command:

curl -sL https://firebase.tools | bash
This script automatically detects your operating system, downloads the latest Firebase CLI release, then enables the globally available firebase command.

Continue to log in and test the CLI.

For more examples and details about the automatic install script, refer to the script's source code at firebase.tools.

Log in and test the Firebase CLI
After installing the CLI, you must authenticate. Then you can confirm authentication by listing your Firebase projects.

Log into Firebase using your Google account by running the following command:

firebase login
This command connects your local machine to Firebase and grants you access to your Firebase projects.

Note: The firebase login command opens a web page that connects to localhost on your machine. If you're using a remote machine and don't have access to localhost, run the command with the flag --no-localhost.
Note: You can also use the Firebase CLI with CI systems.
Test that the CLI is properly installed and accessing your account by listing your Firebase projects. Run the following command:


firebase projects:list
The displayed list should be the same as the Firebase projects listed in the Firebase console.

Update to the latest CLI version
Generally, you want to use the most up-to-date Firebase CLI version.

In many cases, new features and bug fixes are available only with the latest version of the Firebase CLI. It's a good practice to frequently update the CLI to its latest version.
How you update the CLI version depends on your operating system and how you installed the CLI.

Windows
macOS
Linux
standalone binary: Download the new version, then replace it on your system
npm: Run npm install -g firebase-tools
Use the CLI with CI systems
We recommend that you authenticate using Application Default Credentials when using the CLI with CI systems.

(Recommended) Use Application Default Credentials
The Firebase CLI will detect and use Application Default Credentials if they're set. The simplest way to authenticate the CLI in CI and other headless environments is to set up Application Default Credentials.

(Legacy) Use FIREBASE_TOKEN
Alternatively, you can authenticate using FIREBASE_TOKEN. This is less secure than Application Default Credentials and is no longer recommended.

On a machine with a browser, install the Firebase CLI.

Start the signin process by running the following command:


firebase login:ci
Visit the URL provided, then log in using a Google account.

Print a new refresh token. The current CLI session will not be affected.

Store the output token in a secure but accessible way in your CI system.

Use this token when running firebase commands. You can use either of the following two options:

Option 1: Store the token as the environment variable FIREBASE_TOKEN. Your system will automatically use the token.

Option 2: Run all firebase commands with the --token TOKEN flag in your CI system.
This is the order of precedence for token loading: flag, environment variable, desired Firebase project.

Note: On any machine with the Firebase CLI installed, you can immediately revoke access for the specified token by running the following command: firebase logout --token TOKEN
Initialize a Firebase project
Many common tasks performed using the CLI, such as deploying to a Firebase project, require a project directory. You establish a project directory using the firebase init command. A project directory is usually the same directory as your source control root, and after running firebase init, the directory contains a firebase.json configuration file.

To initialize a new Firebase project, run the following command from within your app's directory:


firebase init
Note: The firebase init command does not create a new directory. If you're starting a new app, you must first make a directory, then run firebase init from within that directory.
The firebase init command steps you through setting up your project directory and some Firebase products. During project initialization, the Firebase CLI asks you to complete the following tasks:

Select a default Firebase project.

This step associates the current project directory with a Firebase project so that project-specific commands (like firebase deploy) run against the appropriate Firebase project.

It's also possible to associate multiple Firebase projects (such as a staging project and a production project) with the same project directory.

Select desired Firebase products to set up in your Firebase project.

This step prompts you to set configurations for specific files for the selected products. For more details on these configurations, refer to the specific product's documentation (for example, Hosting). Note that you can always run firebase init later to set up more Firebase products.

At the end of initialization, Firebase automatically creates the following two files at the root of your local app directory:

A firebase.json configuration file that lists your project configuration.

A .firebaserc file that stores your project aliases.

The firebase.json file
The firebase init command creates a firebase.json configuration file in the root of your project directory.

The firebase.json file is required to deploy assets with the Firebase CLI because it specifies which files and settings from your project directory are deployed to your Firebase project. Since some settings can be defined in either your project directory or the Firebase console, make sure that you resolve any potential deployment conflicts.

You can configure most Firebase Hosting options directly in the firebase.json file. However, for other Firebase services that can be deployed with the Firebase CLI, the firebase init command creates specific files where you can define settings for those services, such as an index.js file for Cloud Functions. You can also set up predeploy or postdeploy hooks in the firebase.json file.

Note: If you run firebase init again for any Firebase service, the command will overwrite the corresponding section of the firebase.json file back to the default configuration for that service.
The following is an example firebase.json file with default settings if you select Firebase Hosting, Cloud Firestore, and Cloud Functions for Firebase (with TypeScript source and lint options selected) during initialization.


{
  "hosting": {
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  },
  "firestore": {
      "rules": "firestore.rules",
      "indexes": "firestore.indexes.json"
  },
  "functions": {
    "predeploy": [
      "npm --prefix \"$RESOURCE_DIR\" run lint",
      "npm --prefix \"$RESOURCE_DIR\" run build"
    ]
  }
}
While firebase.json is used by default, you can pass the --config PATH flag to specify an alternate configuration file.

Configuration for multiple Cloud Firestore databases
When you run firebase init, your firebase.json file will contain a single firestore key corresponding to your project's default database, as shown above.

If your project contains multiple Cloud Firestore databases, edit your firebase.json file to associate different Cloud Firestore Security Rules and database index source files with each database. Modify the file with a JSON array, with one entry for each database.

      "firestore": [
        {
          "database": "(default)",
          "rules": "firestore.default.rules",
          "indexes": "firestore.default.indexes.json"
        },
        {
          "database": "ecommerce",
          "rules": "firestore.ecommerce.rules",
          "indexes": "firestore.ecommerce.indexes.json"
        }
      ],
Cloud Functions files to ignore on deploy
At function deployment time, the CLI automatically specifies a list of files in the functions directory to ignore. This prevents deploying to the backend extraneous files that could increase the data size of your deployment.

The list of files ignored by default, shown in JSON format, is:

"ignore": [
  ".git",
  ".runtimeconfig.json",
  "firebase-debug.log",
  "firebase-debug.*.log",
  "node_modules"
]
If you add your own custom values for ignore in firebase.json, make sure that you keep (or add, if it is missing) the list of files shown above.

Manage project aliases
You can associate multiple Firebase projects with the same project directory. For example, you might want to use one Firebase project for staging and another for production. By using different project environments, you can verify changes before deploying to production. The firebase use command allows you to switch between aliases as well as create new aliases.

Add a project alias
When you select a Firebase project during project initialization, the project is automatically assigned the alias of default. However, to allow project-specific commands to run against a different Firebase project but still use the same project directory, run the following command from within your project directory:

firebase use --add
This command prompts you to select another Firebase project and assign the project as alias. Alias assignments are written to a .firebaserc file inside your project directory.

Use project aliases
To use assigned Firebase project aliases, run any of the following commands from within your project directory.

Command	Description
firebase use	View a list of currently defined aliases for your project directory
firebase use \
PROJECT_ID|ALIAS	Directs all commands to run against the specified Firebase project.
The CLI uses this project as the currently "active project".
firebase use --clear	Clears the active project.
Run firebase use PROJECT_ID|ALIAS to set a new active project before running other CLI commands.

firebase use \
--unalias PROJECT_ALIAS	Removes an alias from your project directory.
You can override what's being used as the currently active project by passing the --project flag with any CLI command. As an example: You can set your CLI to run against a Firebase project that you've assigned the staging alias. If you want to run a single command against the Firebase project that you've assigned the prod alias, then you can run, for example, firebase deploy --project=prod.

Source control and project aliases
In general, you should check your .firebaserc file into source control to allow your team to share project aliases. However, for open source projects or starter templates, you should generally not check in your .firebaserc file.

If you have a development project that's for your use only, you can either pass the --project flag with each command or run firebase use PROJECT_ID without assigning an alias to the Firebase project.

Serve and test your Firebase project locally
You can view and test your Firebase project on locally hosted URLs before deploying to production. If you only want to test select features, you can use a comma-separated list in a flag on the firebase serve command.

Run the following command from the root of your local project directory if you want to do either of the following tasks:

View the static content for your Firebase-hosted app.
Use Cloud Functions to generate dynamic content for Firebase Hosting and you want to use your production (deployed) HTTP functions to emulate Hosting on a local URL.
firebase serve --only hosting
Emulate your project using local HTTP functions
Run any of the following commands from your project directory to emulate your project using local HTTP functions.

To emulate HTTP functions and hosting for testing on local URLs, use either of the following commands:

firebase serve
firebase serve --only functions,hosting // uses a flag
To emulate HTTP functions only, use the following command:

firebase serve --only functions
Test from other local devices
By default, firebase serve only responds to requests from localhost. This means that you'll be able to access your hosted content from your computer's web browser but not from other devices on your network. If you'd like to test from other local devices, use the --host flag, like so:

firebase serve --host 0.0.0.0  // accepts requests to any host
Deploy to a Firebase project
The Firebase CLI manages deployment of code and assets to your Firebase project, including:

New releases of your Firebase Hosting sites
New, updated, or existing Cloud Functions for Firebase
New or updated schemas and connectors for Firebase Data Connect
Rules for Firebase Realtime Database
Rules for Cloud Storage for Firebase
Rules for Cloud Firestore
Indexes for Cloud Firestore
To deploy to a Firebase project, run the following command from your project directory:

firebase deploy
You can optionally add a comment to each of your deployments. This comment will display with the other deployment information on your project's Firebase Hosting page. For example:

firebase deploy -m "Deploying the best new feature ever."
When you use the firebase deploy command, be aware of the following:

To deploy resources from a project directory, the project directory must have a firebase.json file. This file is automatically created for you by the firebase init command.

By default, firebase deploy creates a release for all deployable resources in your project directory. To deploy specific Firebase services or features, use partial deployment.

Deployment conflicts for security rules
For Firebase Realtime Database, Cloud Storage for Firebase, and Cloud Firestore, you can define security rules either in your local project directory or in the Firebase console.

Note: When you deploy security rules using the Firebase CLI, the rules defined in your project directory overwrite any existing rules in the Firebase console. So, if you choose to define or edit your security rules using the Firebase console, make sure that you also update the rules defined in your project directory.
Another option to avoid deployment conflicts is to use partial deployment and only define rules in the Firebase console.

Deployment quotas
It's possible (though unlikely) that you might exceed a quota that limits the rate or volume of your Firebase deployment operations. For example, when deploying very large numbers of functions, you might receive an HTTP 429 Quota error message. To solve such issues, try using partial deployment.

Roll back a deployment
You can roll back a Firebase Hosting deployment from your project's Firebase Hosting page by selecting the Rollback action for the desired release.

It's not currently possible to roll back releases of security rules for Firebase Realtime Database, Cloud Storage for Firebase, or Cloud Firestore.

Deploy specific Firebase services
If you only want to deploy specific Firebase services or features, you can use a comma-separated list in a flag on the firebase deploy command. For example, the following command deploys Firebase Hosting content and Cloud Storage security rules.

firebase deploy --only hosting,storage
The following table lists the services and features available for partial deployment. The names in the flags correspond to the keys in your firebase.json configuration file.

Flag syntax	Service or feature deployed
--only hosting	Firebase Hosting content
--only database	Firebase Realtime Database rules
--only dataconnect	Firebase Data Connect schemas and connectors
--only storage	Cloud Storage for Firebase rules
--only firestore	Cloud Firestore rules and indexes for all configured databases
--only functions	Cloud Functions for Firebase (more specific versions of this flag are possible)
Note: The --only rules syntax used by older versions of the CLI is deprecated.
Deploy specific functions
When deploying functions, you can target specific functions. For example:

firebase deploy --only functions:function1
firebase deploy --only functions:function1,functions:function2
Another option is to group functions into export groups in your /functions/index.js file. Grouping functions allows you to deploy multiple functions using a single command.

For example, you can write the following functions to define a groupA and a groupB:

var functions = require('firebase-functions/v1');

exports.groupA = {
  function1: functions.https.onRequest(...),
  function2: functions.database.ref('\path').onWrite(...)
}
exports.groupB = require('./groupB');
In this example, a separate functions/groupB.js file contains additional functions that specifically define the functions in groupB. For example:

var functions = require('firebase-functions/v1');

exports.function3 = functions.storage.object().onChange(...);
exports.function4 = functions.analytics.event('in_app_purchase').onLog(...);
In this example, you can deploy all the groupA functions by running the following command from your project directory:

firebase deploy --only functions:groupA
Or you can target a specific function within a group by running the following command:

firebase deploy --only functions:groupA.function1,groupB.function4
Important: To avoid running to quota errors and other server errors, limit function group size to 10 or fewer for each deployment operation.
Delete functions
The Firebase CLI supports the following commands and options for deleting previously deployed functions:

Deletes all functions that match the specified name in all regions:

firebase functions:delete FUNCTION-1_NAME
Deletes a specified function running in a non-default region:

firebase functions:delete FUNCTION-1_NAME --region REGION_NAME
Deletes more than one function:

firebase functions:delete FUNCTION-1_NAME FUNCTION-2_NAME
Deletes a specified functions group:

firebase functions:delete GROUP_NAME
Bypasses the confirmation prompt:

firebase functions:delete FUNCTION-1_NAME --force
Set up predeploy and postdeploy scripted tasks
You can connect shell scripts to the firebase deploy command to perform predeploy or postdeploy tasks. For example, a predeploy script could transpile TypeScript code into JavaScript, and a postdeploy hook could notify administrators of new site content deploys to Firebase Hosting.

To set up predeploy or postdeploy hooks, add bash scripts to your firebase.json configuration file. You can define brief scripts directly in the firebase.json file, or you can reference other files that are in your project directory.

For example, the following script is the firebase.json expression for a postdeploy task that sends a Slack message upon successful deployment to Firebase Hosting.

"hosting": {
  // ...

  "postdeploy": "./messageSlack.sh 'Just deployed to Firebase Hosting'",
  "public": "public"
}
The messageSlack.sh script file resides in the project directory and looks like this:

curl -X POST -H 'Content-type: application/json' --data '{"text":"$1"}'
     \https://SLACK_WEBHOOK_URL
You can set up predeploy and postdeploy hooks for any of the assets that you can deploy. Note that running firebase deploy triggers all the predeploy and postdeploy tasks defined in your firebase.json file. To run only those tasks associated with a specific Firebase service, use partial deployment commands.

Both predeploy and postdeploy hooks print the standard output and error streams of the scripts to the terminal. For failure cases, note the following:

If a predeploy hook fails to complete as expected, deployment is canceled.
If deployment fails for any reason, postdeploy hooks are not triggered.
Environment variables
Within scripts running in the predeploy and postdeploy hooks, the following environment variables are available:

$GCLOUD_PROJECT: The active project's project ID
$PROJECT_DIR: The root directory containing the firebase.json file
$RESOURCE_DIR: (For hosting and functions scripts only) The location of the directory that contains the Hosting or Cloud Functions resources to be deployed
Manage multiple Realtime Database instances
A Firebase project can have multiple Firebase Realtime Database instances. By default, CLI commands interact with your default database instance.

However, you can interact with a non-default database instance by using the --instance DATABASE_NAME flag. The following commands support the --instance flag:

firebase database:get
firebase database:profile
firebase database:push
firebase database:remove
firebase database:set
firebase database:update
Command reference
CLI administrative commands
Command	Description
help	Displays help information about the CLI or specific commands.
init	Associates and sets up a new Firebase project in the current directory. This command creates a firebase.json configuration file in the current directory.
login	Authenticates the CLI with your Google Account. Requires access to a web browser.
To log into the CLI in remote environments that don't allow access to localhost, use the --no-localhost flag.
login:ci	Generates an authentication token for use in non-interactive environments.
logout	Signs out your Google Account from the CLI.
open	Opens a browser to relevant project resources.
projects:list	Lists all the Firebase projects to which you have access.
use	Sets the active Firebase project for the CLI.
Manages project aliases.
Project management commands
Command	Description
Management of Firebase projects
projects:addfirebase	Adds Firebase resources to an existing Google Cloud project.
projects:create	Creates a new Google Cloud project, then adds Firebase resources to the new project.
projects:list	Lists all the Firebase projects to which you have access.
Management of Firebase Apps (iOS, Android, Web)
apps:create	Creates a new Firebase App in the active project.
apps:list	Lists the registered Firebase Apps in the active project.
apps:sdkconfig	Prints the Google services configuration of a Firebase App.
setup:web	Deprecated. Instead, use apps:sdkconfig and specify web as the platform argument.
Prints the Google services configuration of a Firebase Web App.
Management of SHA certificate hashes (Android only)
apps:android:sha:create \
FIREBASE_APP_ID SHA_HASH	Adds the specified SHA certificate hash to the specified Firebase Android App.
apps:android:sha:delete \
FIREBASE_APP_ID SHA_HASH	Deletes the specified SHA certificate hash from the specified Firebase Android App.
apps:android:sha:list \
FIREBASE_APP_ID	Lists the SHA certificate hashes for the specified Firebase Android App.
Deployment and local development
These commands let you deploy and interact with your Firebase Hosting site.

Command	Description
deploy	Deploys code and assets from your project directory to the active project. For Firebase Hosting, a firebase.json configuration file is required.
serve	Starts a local web server with your Firebase Hosting configuration. For Firebase Hosting, a firebase.json configuration file is required.
App Distribution commands
Command	Description
appdistribution:distribute \
--app FIREBASE_APP_ID	Makes the build available to testers.
appdistribution:testers:add	Adds testers to the project.
appdistribution:testers:remove	Removes testers from the project.
App Hosting commands
Command	Description
apphosting:backends:create \
--project PROJECT_ID \
--location REGION --app APP_ID	Creates the collection of managed resources linked to a single codebase that comprises an App Hosting backend. Optionally specify an existing Firebase Web app by its Firebase app ID.
apphosting:backends:get \
BACKEND_ID \
--project PROJECT_ID \
--location REGION	Retrieves specific details, including the public URL, of a backend.
apphosting:backends:list \
--project PROJECT_ID	Retrieves a list of all active backends associated with a project.
firebase apphosting:backends:delete \
BACKEND_ID \
--project PROJECT_ID \
--location REGION	Deletes a backend from the project.
firebase apphosting:config:export \
--project PROJECT_ID \
--secrets ENVIRONMENT_NAME	Exports secrets for use in app emulation.
Defaults to secrets stored in apphosting.yaml, or takes --secrets to specify any environment that has a corresponding apphosting.ENVIRONMENT_NAME.yaml file.
firebase apphosting:rollouts:create \
BACKEND_ID \
--git_branch BRANCH_NAME \
--git_commit COMMIT_ID	Creates a manually triggered rollout.
Optionally specify the latest commit to a branch or a specific commit. If no options are provided, prompts selection from a list of branches.
apphosting:secrets:set KEY --project PROJECT_ID \
--location REGION \
--data-file DATA_FILE_PATH	Stores secret material in Secret Manager.
Optionally provide a file path from which to read secret data. Set to _ to read secret data from standard input.
apphosting:secrets:grantaccess KEY BACKEND_ID \
--project PROJECT_ID \
--location REGION	Grants the backend service account access to the provided secret so that it can be accessed by App Hosting at build or run time.
apphosting:secrets:describe KEY \
--project PROJECT_ID	Gets the metadata for a secret and its versions.
firebase apphosting:secrets:access \
KEY[@version] \
--project PROJECT_ID	Accesses a secret value given the secret and its version. Defaults to accessing the latest version.
Authentication (user management) commands
Command	Description
auth:export	Exports the active project's user accounts to a JSON or CSV file. For more details, refer to the auth:import and auth:export page.
auth:import	Imports the user accounts from a JSON or CSV file into the active project. For more details, refer to the auth:import and auth:export page.
Cloud Firestore commands
Command	Description
firestore:locations	
List available locations for your Cloud Firestore database.

firestore:databases:create DATABASE_ID	
Create a database instance in native mode in your Firebase project.

The command takes the following flags:

--location <region name> to specify the deployment location for the database. Note you can run firebase firestore:locations to list available locations. Required.
--delete-protection <deleteProtectionState> to allow or prevent deletion of the specified database. Valid values are ENABLED or DISABLED. Defaults to DISABLED.
--point-in-time-recovery <PITRState> to set whether point-in-time recovery is enabled. Valid values are ENABLED or DISABLED. Defaults to DISABLED. Optional.
firestore:databases:list	
List databases in your Firebase project.

firestore:databases:get DATABASE_ID	
Get database configuration for a specified database in your Firebase project.

firestore:databases:update DATABASE_ID	
Update database configuration of a specified database in your Firebase project.

At least one flag is required. The command takes the following flags:

--delete-protection <deleteProtectionState> to allow or prevent deletion of the specified database. Valid values are ENABLED or DISABLED. Defaults to DISABLED.
--point-in-time-recovery <PITRState> to set whether point-in-time recovery is enabled. Valid values are ENABLED or DISABLED. Defaults to DISABLED. Optional.
firestore:databases:delete DATABASE_ID	
Delete a database in your Firebase project.

firestore:indexes	
List indexes for a database in your Firebase project.

The command takes the following flag:

--database DATABASE_ID to specify the name of the database for which to list indexes. If not provided, indexes are listed for the default database.
firestore:delete	
Deletes documents in the active project's database. Using the CLI, you can recursively delete all the documents in a collection.

Note that deleting Cloud Firestore data with the CLI incurs read and delete costs. For more information, see Understand Cloud Firestore billing.

The command takes the following flag:

--database DATABASE_ID to specify the name of the database from which documents are deleted. If not specified, documents are deleted from the default database. Optional.
Cloud Functions for Firebase commands
Command	Description
functions:config:clone	Clones another project's environment into the active Firebase project.
functions:config:get	Retrieves existing configuration values of the active project's Cloud Functions.
functions:config:set	Stores runtime configuration values of the active project's Cloud Functions.
functions:config:unset	Removes values from the active project's runtime configuration.
functions:log	Reads logs from deployed Cloud Functions.
For more information, refer to the environment configuration documentation.

Crashlytics commands
Command	Description
crashlytics:mappingfile:generateid \
--resource-file=PATH/TO/ANDROID_RESOURCE.XML	Generates a unique mapping file ID in the specified Android resource (XML) file.
crashlytics:mappingfile:upload \
--app=FIREBASE_APP_ID \
--resource-file=PATH/TO/ANDROID_RESOURCE.XML \
PATH/TO/MAPPING_FILE.TXT	Uploads a Proguard-compatible mapping (TXT) file for this app, and associates it with the mapping file ID declared in the specified Android resource (XML) file.
crashlytics:symbols:upload \
--app=FIREBASE_APP_ID \
PATH/TO/SYMBOLS	Generates a Crashlytics-compatible symbol file for native library crashes on Android and uploads it to Firebase servers.
Data Connect commands
These commands and their use cases are covered in more detail in the Data Connect CLI reference guide.

Command	Description
dataconnect:services:list	Lists all deployed Data Connect services in your Firebase project.
dataconnect:sql:diff \
SERVICE_ID	For the specified service, displays the differences between a local Data Connect schema and your Cloud SQL database schema.
dataconnect:sql:migrate \
--force \
SERVICE_ID	Migrates your Cloud SQL database's schema to match your local Data Connect schema.
dataconnect:sql:grant\
--role=ROLE \
--email=EMAIL \
SERVICE_ID	Grants the SQL role to the specified user or service account email.
For the --role flag, the SQL role to grant is one of: owner, writer, or reader.
For the --email flag, provide the email address of the user or service account to grant the role to.
dataconnect:sdk:generate	Generates typed SDKs for your Data Connect connectors.
Extensions commands
Command	Description
ext	Displays information on how to use Firebase Extensions commands.
Lists the extension instances installed in the active project.
ext:configure \
EXTENSION_INSTANCE_ID	Reconfigures the parameter values of an extension instance in your extension manifest.
ext:info \
PUBLISHER_ID/EXTENSION_ID	Prints detailed information about an extension.
ext:install \
PUBLISHER_ID/EXTENSION_ID	Adds a new instance of an extension into your extension manifest.
ext:list	Lists all the extension instances installed in a Firebase project.
Prints the instance ID for each extension.
ext:uninstall \
EXTENSION_INSTANCE_ID	Removes an extension instance from your extension manifest.
ext:update \
EXTENSION_INSTANCE_ID	Updates an extension instance to the latest version in your extension manifest.
ext:export	Exports all installed extension instances from your project to your extension manifest.
Extensions publisher commands
Command	Description
ext:dev:init	Initializes a skeleton codebase for a new extension in the current directory.
ext:dev:list \
PUBLISHER_ID	Prints a list of all extensions uploaded by a publisher.
ext:dev:register	Registers a Firebase project as an extensions publisher project.
ext:dev:deprecate \
PUBLISHER_ID/EXTENSION_ID \
VERSION_PREDICATE	Deprecates extension versions that match the version predicate.
A version predicate can be a single version (such as 1.0.0), or a range of versions (such as >1.0.0).
If no version predicate is provided, deprecates all versions of that extension.
ext:dev:undeprecate \
PUBLISHER_ID/EXTENSION_ID \
VERSION_PREDICATE	Undeprecates extension versions that match the version predicate.
A version predicate can be a single version (such as 1.0.0), or a range of versions (such as >1.0.0).
If no version predicate is provided, undeprecates all versions of that extension.
ext:dev:upload \
PUBLISHER_ID/EXTENSION_ID	Uploads a new version of an extension.
ext:dev:usage \
PUBLISHER_ID	Displays install counts and usage metrics for extensions uploaded by a publisher.
Hosting commands
Command	Description
hosting:disable	
Stops serving Firebase Hosting traffic for the active Firebase project.

Your project's Hosting URL will display a "Site Not Found" message after running this command.

Management of Hosting sites
firebase hosting:sites:create \
SITE_ID	
Creates a new Hosting site in the active Firebase project using the specified SITE_ID

(Optional) Specify an existing Firebase Web App to associate with the new site by passing the following flag: --app FIREBASE_APP_ID

firebase hosting:sites:delete \
SITE_ID	
Deletes the specified Hosting site

The CLI displays a confirmation prompt before deleting the site.

(Optional) Skip the confirmation prompt by passing the following flags: -f or --force

firebase hosting:sites:get \
SITE_ID	
Retrieves information about the specified Hosting site

firebase hosting:sites:list	
Lists all Hosting sites for the active Firebase project

Management of preview channels
firebase hosting:channel:create \
CHANNEL_ID	
Creates a new preview channel in the default Hosting site using the specified CHANNEL_ID

This command does not deploy to the channel.

firebase hosting:channel:delete \
CHANNEL_ID	
Deletes the specified preview channel

You cannot delete a site's live channel.

firebase hosting:channel:deploy \
CHANNEL_ID	
Deploys your Hosting content and config to the specified preview channel

If the preview channel does not yet exist, this command creates the channel in the default Hosting site before deploying to the channel.

firebase hosting:channel:list	Lists all channels (including the "live" channel) in the default Hosting site
firebase hosting:channel:open \
CHANNEL_ID	Opens a browser to the specified channel's URL or returns the URL if opening in a browser isn't possible
Version cloning
firebase hosting:clone \
SOURCE_SITE_ID:SOURCE_CHANNEL_ID \
TARGET_SITE_ID:TARGET_CHANNEL_ID	
Clones the most recently deployed version on the specified "source" channel to the specified "target" channel

This command also deploys to the specified "target" channel. If the "target" channel does not yet exist, this command creates a new preview channel in the "target" Hosting site before deploying to the channel.

firebase hosting:clone \
SOURCE_SITE_ID:@VERSION_ID \
TARGET_SITE_ID:TARGET_CHANNEL_ID	
Clones the specified version to the specified "target" channel

This command also deploys to the specified "target" channel. If the "target" channel does not yet exist, this command creates a new preview channel in the "target" Hosting site before deploying to the channel.

You can find the VERSION_ID in the Hosting dashboard of the Firebase console.

Realtime Database commands
Note that you can create your initial, default Realtime Database instance in the Firebase console or by using the general firebase init workflow or the specific firebase init database flow.

Once instances are created, you can manage them as discussed in Manage multiple Realtime Database instances.

Command	Description
database:get	Fetches data from the active project's database and displays it as JSON. Supports querying on indexed data.
database:instances:create	Creates a database instance with a specified instance name. Accepts the --location option for creating a database in a specified region. For region names to use with this option, see select locations for your project. If no database instance exists for the current project, you are prompted to run the firebase init flow to create an instance.
database:instances:list	List all database instances for this project. Accepts the --location option for listing databases in a specified region. For region names to use with this option see select locations for your project.
database:profile	Builds a profile of operations on the active project's database. For more details, refer to Realtime Database operation types.
database:push	Pushes new data to a list at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
database:remove	Deletes all data at a specified location in the active project's database.
database:set	Replaces all data at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
database:update	Performs a partial update at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
Remote Config commands
Command	Description
remoteconfig:versions:list \
--limit NUMBER_OF_VERSIONS	Lists the most recent ten versions of the template. Specify 0 to return all existing versions, or optionally pass the --limit option to limit the number of versions being returned.
remoteconfig:get \
--v, version_number VERSION_NUMBER
--o, output FILENAME	Gets the template by version (defaults to the latest version) and outputs the parameter groups, parameters, and condition names and version into a table. Optionally, you can write the output to a specified file with -o, FILENAME.
remoteconfig:rollback \
--v, version_number VERSION_NUMBER
--force	Rolls back Remote Config template to a specified previous version number or defaults to the immediate previous version (current version -1). Unless --force is passed, prompts Y/N before proceeding to rollback.
Send feedback
Except as otherwise noted, the content of this page is licensed under the Creative Commons Attribution 4.0 License, and code samples are licensed under the Apache 2.0 License. For details, see the Google Developers Site Policies. Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-06-04 UTC.

Learn
Developer guides
SDK & API reference
Samples
Libraries
GitHub
Stay connected
Check out the blog
Find us on Reddit
Follow on X
Subscribe on YouTube
Attend an event
Support
Contact support
Stack Overflow
Slack community
Google group
Release notes
Brand guidelines
FAQs
Google Developers
Android
Chrome
Firebase
Google Cloud Platform
All products
Terms
Privacy

English

skip to:contentpackage searchsign in
❤
Pro
Teams
Pricing
Documentation
npm
Search packages
Search
firebase
TypeScript icon, indicating that this package has built-in type declarations
11.9.1 • Public • Published 4 days ago
Build Status Version Coverage Status

Firebase - App success made simple
Upgrade to Version 9
Version 9 has a redesigned API that supports tree-shaking. Read the Upgrade Guide to learn more.

Overview
Firebase provides the tools and infrastructure you need to develop, grow, and earn money from your app. This package supports web (browser), mobile-web, and server (Node.js) clients.

For more information, visit:

Firebase Realtime Database - The Firebase Realtime Database lets you store and query user data, and makes it available between users in realtime.
Cloud Firestore - Cloud Firestore is a flexible, scalable database for mobile, web, and server development from Firebase and Google Cloud Platform.
Firebase Storage - Firebase Storage lets you upload and store user generated content, such as files, and images.
Cloud Functions for Firebase - Cloud Functions for Firebase is a serverless framework that lets you automatically run backend code in response to events triggered by Firebase features and HTTPS requests.
Firebase Cloud Messaging - Firebase Cloud Messaging is a cross-platform messaging solution that lets you reliably deliver messages at no cost.
Firebase Performance Monitoring - Firebase Performance Monitoring helps you gain insight into your app's performance issues.
Google Analytics - Google Analytics is a free app measurement solution that provides insight on app usage and user engagement.
Remote Config - Firebase Remote Config is a cloud service that lets you change the behavior and appearance of your app without requiring users to reload your app.
App Check - App Check helps protect your backend resources from abuse, such as billing fraud and phishing. It works with both Firebase services and your own backends to keep your resources safe.
Create and setup your account - Get started using Firebase for free.
This SDK is intended for end-user client access from environments such as the Web, mobile Web (e.g. React Native, Ionic), Node.js desktop (e.g. Electron), or IoT devices running Node.js. If you are instead interested in using a Node.js SDK which grants you admin access from a privileged environment (like a server), you should use the Firebase Admin Node.js SDK.

Install the SDK
Install the Firebase NPM module:

$ npm init
$ npm install --save firebase
import { initializeApp } from 'firebase/app';

// TODO: Replace the following with your app's Firebase project configuration
const firebaseConfig = {
  //...
};

const app = initializeApp(firebaseConfig);
Access Firebase services in your app
Firebase services (like Cloud Firestore, Authentication, Realtime Database, Remote Config, and more) are available to import within individual sub-packages.

The example below shows how you could use the Cloud Firestore Lite SDK to retrieve a list of data.

import { initializeApp } from 'firebase/app';
import { getFirestore, collection, getDocs } from 'firebase/firestore/lite';
// Follow this pattern to import other Firebase services
// import { } from 'firebase/<service>';

// TODO: Replace the following with your app's Firebase project configuration
const firebaseConfig = {
  //...
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

// Get a list of cities from your database
async function getCities(db) {
  const citiesCol = collection(db, 'cities');
  const citySnapshot = await getDocs(citiesCol);
  const cityList = citySnapshot.docs.map(doc => doc.data());
  return cityList;
}
Use a module bundler for size reduction
The Firebase Web SDK is designed to work with module bundlers to remove any unused code (tree-shaking). We strongly recommend using this approach for production apps. Tools such as the Angular CLI, Next.js, Vue CLI, or Create React App automatically handle module bundling for libraries installed through npm and imported into your codebase.

See Using module bundlers with Firebase for more information.

Script include
You can also load Firebase packages as script modules in browsers that support native ES modules.

<!-- use script module by specifying type="module" -->
<script type="module">
    import { initializeApp } from 'https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-app.js';
    import { getFirestore, collection, getDocs } from 'https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-firestore-lite.js';
    // Follow this pattern to import other Firebase services
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-analytics.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-app-check.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-auth.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-functions.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-firestore.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-storage.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-performance.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-remote-config.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-messaging.js";
    // import {} from "https://www.gstatic.com/firebasejs/${FIREBASE_VERSION}/firebase-database.js";
    
    // TODO: Replace the following with your app's Firebase project configuration
    const firebaseConfig = {
    //...
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    // Get a list of cities from your database
    async function getCities(db) {
    const citiesCol = collection(db, 'cities');
    const citySnapshot = await getDocs(citiesCol);
    const cityList = citySnapshot.docs.map(doc => doc.data());
    return cityList;
    }
</script>
Note: To get a filled in version of the above code snippet, go to the Firebase console for your app and click on "Add Firebase to your web app".

Get the code (Node.js - server and command line)
Install the SDK
While you can write entire Firebase applications without any backend code, many developers want to write server applications or command-line utilities using the Node.js JavaScript runtime.

You can use the same npm module to use Firebase in the Node.js runtime (on a server or running from the command line):

$ npm init
$ npm install --save firebase
In your code, you can access Firebase using:

const { initializeApp } = require('firebase/app');
const { getFirestore, collection, getDocs } = require('firebase/firestore');
// ...
If you are using native ES6 module with --experimental-modules flag (or Node 12+) you should do:

import { initializeApp } from 'firebase/app';
import { getFirestore, collection, getDocs } from 'firebase/firestore';
// ...
Please see Environment Support for which packages are available in Node.js.

Compat packages
Version 9 provides a set of compat packages that are API compatible with Version 8. They are intended to be used to make the upgrade to the modular API easier by allowing you to upgrade your app piece by piece. See the Upgrade Guide for more detail.

To access the compat packages, use the subpath compat like so:

// v9 compat packages are API compatible with v8 code
import firebase from 'firebase/compat/app';
import 'firebase/compat/auth';
import 'firebase/compat/firestore';
Changelog
The Firebase changelog can be found at firebase.google.com.

Browser/environment compatibility
Please see Environment Support.

Readme
Keywords
authenticationdatabaseFirebasefirebaserealtimestorageperformanceremote-config
Package Sidebar
Install
npm i firebase

Repository
github.com/firebase/firebase-js-sdk

Homepage
firebase.google.com/

Weekly Downloads
2,822,766

Version
11.9.1

License
Apache-2.0

Unpacked Size
25.9 MB

Total Files
2756

Last publish
21 hours ago

Collaborators
firebase-ops
feiyang.chen
google-wombot
chholland
Try on RunKit
Report malware
Footer
Support
Help
Advisories
Status
Contact npm
Company
About
Blog
Press
Terms & Policies
Policies
Terms of Use
Code of Conduct
Privacy

Skip to main content
Firebase
More
Search
/


English
Blog
Studio
Go to console

Documentation
Overview
Fundamentals

AI

Build

Run

Test Lab
App Distribution
Crashlytics
Performance Monitoring
Remote Config
A/B Testing
Analytics
Cloud Messaging
In-App Messaging
Dynamic Links
Google AdMob
Google Ads
Reference
Samples
Filter

Here's everything we announced at I/O, from new Firebase Studio features to more ways to integrate AI. Read blog.
Firebase
Documentation
Reference
Was this helpful?

Send feedbackFirebase CLI reference 

bookmark_border


The Firebase CLI (GitHub) provides a variety of tools for managing, viewing, and deploying to Firebase projects.

Before using the Firebase CLI, set up a Firebase project.

Set up or update the CLI
Install the Firebase CLI
You can install the Firebase CLI using a method that matches your operating system, experience level, and/or use case. Regardless of how you install the CLI, you have access to the same functionality and the firebase command.

Windows macOS Linux

Windows
You can install the Firebase CLI for Windows using one of the following options:

Option	Description	Recommended for...
standalone binary	Download the standalone binary for the CLI. Then, you can access the executable to open a shell where you can run the firebase command.	New developers

Developers not using or unfamiliar with Node.js
npm	Use npm (the Node Package Manager) to install the CLI and enable the globally available firebase command.	Developers using Node.js
standalone binary
npm
To download and run the binary for the Firebase CLI, follow these steps:

Download the Firebase CLI binary for Windows.

Access the binary to open a shell where you can run the firebase command.

Continue to log in and test the CLI.

macOS or Linux
You can install the Firebase CLI for macOS or Linux using one of the following options:

Option	Description	Recommended for...
automatic install script	Run a single command that automatically detects your operating system, downloads the latest CLI release, then enables the globally available firebase command.	New developers

Developers not using or unfamiliar with Node.js

Automated deploys in a CI/CD environment
standalone binary	Download the standalone binary for the CLI. Then, you can configure and run the binary to suit your workflow.	Fully customizable workflows using the CLI
npm	Use npm (the Node Package Manager) to install the CLI and enable the globally available firebase command.	Developers using Node.js
auto install script
standalone binary
npm
To install the Firebase CLI using the automatic install script, follow these steps:

Run the following cURL command:

curl -sL https://firebase.tools | bash
This script automatically detects your operating system, downloads the latest Firebase CLI release, then enables the globally available firebase command.

Continue to log in and test the CLI.

For more examples and details about the automatic install script, refer to the script's source code at firebase.tools.

Log in and test the Firebase CLI
After installing the CLI, you must authenticate. Then you can confirm authentication by listing your Firebase projects.

Log into Firebase using your Google account by running the following command:

firebase login
This command connects your local machine to Firebase and grants you access to your Firebase projects.

Note: The firebase login command opens a web page that connects to localhost on your machine. If you're using a remote machine and don't have access to localhost, run the command with the flag --no-localhost.
Note: You can also use the Firebase CLI with CI systems.
Test that the CLI is properly installed and accessing your account by listing your Firebase projects. Run the following command:


firebase projects:list
The displayed list should be the same as the Firebase projects listed in the Firebase console.

Update to the latest CLI version
Generally, you want to use the most up-to-date Firebase CLI version.

In many cases, new features and bug fixes are available only with the latest version of the Firebase CLI. It's a good practice to frequently update the CLI to its latest version.
How you update the CLI version depends on your operating system and how you installed the CLI.

Windows
macOS
Linux
standalone binary: Download the new version, then replace it on your system
npm: Run npm install -g firebase-tools
Use the CLI with CI systems
We recommend that you authenticate using Application Default Credentials when using the CLI with CI systems.

(Recommended) Use Application Default Credentials
The Firebase CLI will detect and use Application Default Credentials if they're set. The simplest way to authenticate the CLI in CI and other headless environments is to set up Application Default Credentials.

(Legacy) Use FIREBASE_TOKEN
Alternatively, you can authenticate using FIREBASE_TOKEN. This is less secure than Application Default Credentials and is no longer recommended.

On a machine with a browser, install the Firebase CLI.

Start the signin process by running the following command:


firebase login:ci
Visit the URL provided, then log in using a Google account.

Print a new refresh token. The current CLI session will not be affected.

Store the output token in a secure but accessible way in your CI system.

Use this token when running firebase commands. You can use either of the following two options:

Option 1: Store the token as the environment variable FIREBASE_TOKEN. Your system will automatically use the token.

Option 2: Run all firebase commands with the --token TOKEN flag in your CI system.
This is the order of precedence for token loading: flag, environment variable, desired Firebase project.

Note: On any machine with the Firebase CLI installed, you can immediately revoke access for the specified token by running the following command: firebase logout --token TOKEN
Initialize a Firebase project
Many common tasks performed using the CLI, such as deploying to a Firebase project, require a project directory. You establish a project directory using the firebase init command. A project directory is usually the same directory as your source control root, and after running firebase init, the directory contains a firebase.json configuration file.

To initialize a new Firebase project, run the following command from within your app's directory:


firebase init
Note: The firebase init command does not create a new directory. If you're starting a new app, you must first make a directory, then run firebase init from within that directory.
The firebase init command steps you through setting up your project directory and some Firebase products. During project initialization, the Firebase CLI asks you to complete the following tasks:

Select a default Firebase project.

This step associates the current project directory with a Firebase project so that project-specific commands (like firebase deploy) run against the appropriate Firebase project.

It's also possible to associate multiple Firebase projects (such as a staging project and a production project) with the same project directory.

Select desired Firebase products to set up in your Firebase project.

This step prompts you to set configurations for specific files for the selected products. For more details on these configurations, refer to the specific product's documentation (for example, Hosting). Note that you can always run firebase init later to set up more Firebase products.

At the end of initialization, Firebase automatically creates the following two files at the root of your local app directory:

A firebase.json configuration file that lists your project configuration.

A .firebaserc file that stores your project aliases.

The firebase.json file
The firebase init command creates a firebase.json configuration file in the root of your project directory.

The firebase.json file is required to deploy assets with the Firebase CLI because it specifies which files and settings from your project directory are deployed to your Firebase project. Since some settings can be defined in either your project directory or the Firebase console, make sure that you resolve any potential deployment conflicts.

You can configure most Firebase Hosting options directly in the firebase.json file. However, for other Firebase services that can be deployed with the Firebase CLI, the firebase init command creates specific files where you can define settings for those services, such as an index.js file for Cloud Functions. You can also set up predeploy or postdeploy hooks in the firebase.json file.

Note: If you run firebase init again for any Firebase service, the command will overwrite the corresponding section of the firebase.json file back to the default configuration for that service.
The following is an example firebase.json file with default settings if you select Firebase Hosting, Cloud Firestore, and Cloud Functions for Firebase (with TypeScript source and lint options selected) during initialization.


{
  "hosting": {
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  },
  "firestore": {
      "rules": "firestore.rules",
      "indexes": "firestore.indexes.json"
  },
  "functions": {
    "predeploy": [
      "npm --prefix \"$RESOURCE_DIR\" run lint",
      "npm --prefix \"$RESOURCE_DIR\" run build"
    ]
  }
}
While firebase.json is used by default, you can pass the --config PATH flag to specify an alternate configuration file.

Configuration for multiple Cloud Firestore databases
When you run firebase init, your firebase.json file will contain a single firestore key corresponding to your project's default database, as shown above.

If your project contains multiple Cloud Firestore databases, edit your firebase.json file to associate different Cloud Firestore Security Rules and database index source files with each database. Modify the file with a JSON array, with one entry for each database.


      "firestore": [
        {
          "database": "(default)",
          "rules": "firestore.default.rules",
          "indexes": "firestore.default.indexes.json"
        },
        {
          "database": "ecommerce",
          "rules": "firestore.ecommerce.rules",
          "indexes": "firestore.ecommerce.indexes.json"
        }
      ],
Cloud Functions files to ignore on deploy
At function deployment time, the CLI automatically specifies a list of files in the functions directory to ignore. This prevents deploying to the backend extraneous files that could increase the data size of your deployment.

The list of files ignored by default, shown in JSON format, is:


"ignore": [
  ".git",
  ".runtimeconfig.json",
  "firebase-debug.log",
  "firebase-debug.*.log",
  "node_modules"
]
If you add your own custom values for ignore in firebase.json, make sure that you keep (or add, if it is missing) the list of files shown above.

Manage project aliases
You can associate multiple Firebase projects with the same project directory. For example, you might want to use one Firebase project for staging and another for production. By using different project environments, you can verify changes before deploying to production. The firebase use command allows you to switch between aliases as well as create new aliases.

Add a project alias
When you select a Firebase project during project initialization, the project is automatically assigned the alias of default. However, to allow project-specific commands to run against a different Firebase project but still use the same project directory, run the following command from within your project directory:


firebase use --add
This command prompts you to select another Firebase project and assign the project as alias. Alias assignments are written to a .firebaserc file inside your project directory.

Use project aliases
To use assigned Firebase project aliases, run any of the following commands from within your project directory.

Command	Description
firebase use	View a list of currently defined aliases for your project directory
firebase use \
PROJECT_ID|ALIAS	Directs all commands to run against the specified Firebase project.
The CLI uses this project as the currently "active project".
firebase use --clear	Clears the active project.
Run firebase use PROJECT_ID|ALIAS to set a new active project before running other CLI commands.

firebase use \
--unalias PROJECT_ALIAS	Removes an alias from your project directory.
You can override what's being used as the currently active project by passing the --project flag with any CLI command. As an example: You can set your CLI to run against a Firebase project that you've assigned the staging alias. If you want to run a single command against the Firebase project that you've assigned the prod alias, then you can run, for example, firebase deploy --project=prod.

Source control and project aliases
In general, you should check your .firebaserc file into source control to allow your team to share project aliases. However, for open source projects or starter templates, you should generally not check in your .firebaserc file.

If you have a development project that's for your use only, you can either pass the --project flag with each command or run firebase use PROJECT_ID without assigning an alias to the Firebase project.

Serve and test your Firebase project locally
You can view and test your Firebase project on locally hosted URLs before deploying to production. If you only want to test select features, you can use a comma-separated list in a flag on the firebase serve command.

Run the following command from the root of your local project directory if you want to do either of the following tasks:

View the static content for your Firebase-hosted app.
Use Cloud Functions to generate dynamic content for Firebase Hosting and you want to use your production (deployed) HTTP functions to emulate Hosting on a local URL.

firebase serve --only hosting
Emulate your project using local HTTP functions
Run any of the following commands from your project directory to emulate your project using local HTTP functions.

To emulate HTTP functions and hosting for testing on local URLs, use either of the following commands:


firebase serve

firebase serve --only functions,hosting // uses a flag
To emulate HTTP functions only, use the following command:


firebase serve --only functions
Test from other local devices
By default, firebase serve only responds to requests from localhost. This means that you'll be able to access your hosted content from your computer's web browser but not from other devices on your network. If you'd like to test from other local devices, use the --host flag, like so:


firebase serve --host 0.0.0.0  // accepts requests to any host
Deploy to a Firebase project
The Firebase CLI manages deployment of code and assets to your Firebase project, including:

New releases of your Firebase Hosting sites
New, updated, or existing Cloud Functions for Firebase
New or updated schemas and connectors for Firebase Data Connect
Rules for Firebase Realtime Database
Rules for Cloud Storage for Firebase
Rules for Cloud Firestore
Indexes for Cloud Firestore
To deploy to a Firebase project, run the following command from your project directory:


firebase deploy
You can optionally add a comment to each of your deployments. This comment will display with the other deployment information on your project's Firebase Hosting page. For example:


firebase deploy -m "Deploying the best new feature ever."
When you use the firebase deploy command, be aware of the following:

To deploy resources from a project directory, the project directory must have a firebase.json file. This file is automatically created for you by the firebase init command.

By default, firebase deploy creates a release for all deployable resources in your project directory. To deploy specific Firebase services or features, use partial deployment.

Deployment conflicts for security rules
For Firebase Realtime Database, Cloud Storage for Firebase, and Cloud Firestore, you can define security rules either in your local project directory or in the Firebase console.

Note: When you deploy security rules using the Firebase CLI, the rules defined in your project directory overwrite any existing rules in the Firebase console. So, if you choose to define or edit your security rules using the Firebase console, make sure that you also update the rules defined in your project directory.
Another option to avoid deployment conflicts is to use partial deployment and only define rules in the Firebase console.

Deployment quotas
It's possible (though unlikely) that you might exceed a quota that limits the rate or volume of your Firebase deployment operations. For example, when deploying very large numbers of functions, you might receive an HTTP 429 Quota error message. To solve such issues, try using partial deployment.

Roll back a deployment
You can roll back a Firebase Hosting deployment from your project's Firebase Hosting page by selecting the Rollback action for the desired release.

It's not currently possible to roll back releases of security rules for Firebase Realtime Database, Cloud Storage for Firebase, or Cloud Firestore.

Deploy specific Firebase services
If you only want to deploy specific Firebase services or features, you can use a comma-separated list in a flag on the firebase deploy command. For example, the following command deploys Firebase Hosting content and Cloud Storage security rules.


firebase deploy --only hosting,storage
The following table lists the services and features available for partial deployment. The names in the flags correspond to the keys in your firebase.json configuration file.

Flag syntax	Service or feature deployed
--only hosting	Firebase Hosting content
--only database	Firebase Realtime Database rules
--only dataconnect	Firebase Data Connect schemas and connectors
--only storage	Cloud Storage for Firebase rules
--only firestore	Cloud Firestore rules and indexes for all configured databases
--only functions	Cloud Functions for Firebase (more specific versions of this flag are possible)
Note: The --only rules syntax used by older versions of the CLI is deprecated.
Deploy specific functions
When deploying functions, you can target specific functions. For example:


firebase deploy --only functions:function1

firebase deploy --only functions:function1,functions:function2
Another option is to group functions into export groups in your /functions/index.js file. Grouping functions allows you to deploy multiple functions using a single command.

For example, you can write the following functions to define a groupA and a groupB:


var functions = require('firebase-functions/v1');

exports.groupA = {
  function1: functions.https.onRequest(...),
  function2: functions.database.ref('\path').onWrite(...)
}
exports.groupB = require('./groupB');
In this example, a separate functions/groupB.js file contains additional functions that specifically define the functions in groupB. For example:


var functions = require('firebase-functions/v1');

exports.function3 = functions.storage.object().onChange(...);
exports.function4 = functions.analytics.event('in_app_purchase').onLog(...);
In this example, you can deploy all the groupA functions by running the following command from your project directory:


firebase deploy --only functions:groupA
Or you can target a specific function within a group by running the following command:


firebase deploy --only functions:groupA.function1,groupB.function4
Important: To avoid running to quota errors and other server errors, limit function group size to 10 or fewer for each deployment operation.
Delete functions
The Firebase CLI supports the following commands and options for deleting previously deployed functions:

Deletes all functions that match the specified name in all regions:


firebase functions:delete FUNCTION-1_NAME
Deletes a specified function running in a non-default region:


firebase functions:delete FUNCTION-1_NAME --region REGION_NAME
Deletes more than one function:


firebase functions:delete FUNCTION-1_NAME FUNCTION-2_NAME
Deletes a specified functions group:


firebase functions:delete GROUP_NAME
Bypasses the confirmation prompt:


firebase functions:delete FUNCTION-1_NAME --force
Set up predeploy and postdeploy scripted tasks
You can connect shell scripts to the firebase deploy command to perform predeploy or postdeploy tasks. For example, a predeploy script could transpile TypeScript code into JavaScript, and a postdeploy hook could notify administrators of new site content deploys to Firebase Hosting.

To set up predeploy or postdeploy hooks, add bash scripts to your firebase.json configuration file. You can define brief scripts directly in the firebase.json file, or you can reference other files that are in your project directory.

For example, the following script is the firebase.json expression for a postdeploy task that sends a Slack message upon successful deployment to Firebase Hosting.


"hosting": {
  // ...

  "postdeploy": "./messageSlack.sh 'Just deployed to Firebase Hosting'",
  "public": "public"
}
The messageSlack.sh script file resides in the project directory and looks like this:


curl -X POST -H 'Content-type: application/json' --data '{"text":"$1"}'
     \https://SLACK_WEBHOOK_URL
You can set up predeploy and postdeploy hooks for any of the assets that you can deploy. Note that running firebase deploy triggers all the predeploy and postdeploy tasks defined in your firebase.json file. To run only those tasks associated with a specific Firebase service, use partial deployment commands.

Both predeploy and postdeploy hooks print the standard output and error streams of the scripts to the terminal. For failure cases, note the following:

If a predeploy hook fails to complete as expected, deployment is canceled.
If deployment fails for any reason, postdeploy hooks are not triggered.
Environment variables
Within scripts running in the predeploy and postdeploy hooks, the following environment variables are available:

$GCLOUD_PROJECT: The active project's project ID
$PROJECT_DIR: The root directory containing the firebase.json file
$RESOURCE_DIR: (For hosting and functions scripts only) The location of the directory that contains the Hosting or Cloud Functions resources to be deployed
Manage multiple Realtime Database instances
A Firebase project can have multiple Firebase Realtime Database instances. By default, CLI commands interact with your default database instance.

However, you can interact with a non-default database instance by using the --instance DATABASE_NAME flag. The following commands support the --instance flag:

firebase database:get
firebase database:profile
firebase database:push
firebase database:remove
firebase database:set
firebase database:update
Command reference
CLI administrative commands
Command	Description
help	Displays help information about the CLI or specific commands.
init	Associates and sets up a new Firebase project in the current directory. This command creates a firebase.json configuration file in the current directory.
login	Authenticates the CLI with your Google Account. Requires access to a web browser.
To log into the CLI in remote environments that don't allow access to localhost, use the --no-localhost flag.
login:ci	Generates an authentication token for use in non-interactive environments.
logout	Signs out your Google Account from the CLI.
open	Opens a browser to relevant project resources.
projects:list	Lists all the Firebase projects to which you have access.
use	Sets the active Firebase project for the CLI.
Manages project aliases.
Project management commands
Command	Description
Management of Firebase projects
projects:addfirebase	Adds Firebase resources to an existing Google Cloud project.
projects:create	Creates a new Google Cloud project, then adds Firebase resources to the new project.
projects:list	Lists all the Firebase projects to which you have access.
Management of Firebase Apps (iOS, Android, Web)
apps:create	Creates a new Firebase App in the active project.
apps:list	Lists the registered Firebase Apps in the active project.
apps:sdkconfig	Prints the Google services configuration of a Firebase App.
setup:web	Deprecated. Instead, use apps:sdkconfig and specify web as the platform argument.
Prints the Google services configuration of a Firebase Web App.
Management of SHA certificate hashes (Android only)
apps:android:sha:create \
FIREBASE_APP_ID SHA_HASH	Adds the specified SHA certificate hash to the specified Firebase Android App.
apps:android:sha:delete \
FIREBASE_APP_ID SHA_HASH	Deletes the specified SHA certificate hash from the specified Firebase Android App.
apps:android:sha:list \
FIREBASE_APP_ID	Lists the SHA certificate hashes for the specified Firebase Android App.
Deployment and local development
These commands let you deploy and interact with your Firebase Hosting site.

Command	Description
deploy	Deploys code and assets from your project directory to the active project. For Firebase Hosting, a firebase.json configuration file is required.
serve	Starts a local web server with your Firebase Hosting configuration. For Firebase Hosting, a firebase.json configuration file is required.
App Distribution commands
Command	Description
appdistribution:distribute \
--app FIREBASE_APP_ID	Makes the build available to testers.
appdistribution:testers:add	Adds testers to the project.
appdistribution:testers:remove	Removes testers from the project.
App Hosting commands
Command	Description
apphosting:backends:create \
--project PROJECT_ID \
--location REGION --app APP_ID	Creates the collection of managed resources linked to a single codebase that comprises an App Hosting backend. Optionally specify an existing Firebase Web app by its Firebase app ID.
apphosting:backends:get \
BACKEND_ID \
--project PROJECT_ID \
--location REGION	Retrieves specific details, including the public URL, of a backend.
apphosting:backends:list \
--project PROJECT_ID	Retrieves a list of all active backends associated with a project.
firebase apphosting:backends:delete \
BACKEND_ID \
--project PROJECT_ID \
--location REGION	Deletes a backend from the project.
firebase apphosting:config:export \
--project PROJECT_ID \
--secrets ENVIRONMENT_NAME	Exports secrets for use in app emulation.
Defaults to secrets stored in apphosting.yaml, or takes --secrets to specify any environment that has a corresponding apphosting.ENVIRONMENT_NAME.yaml file.
firebase apphosting:rollouts:create \
BACKEND_ID \
--git_branch BRANCH_NAME \
--git_commit COMMIT_ID	Creates a manually triggered rollout.
Optionally specify the latest commit to a branch or a specific commit. If no options are provided, prompts selection from a list of branches.
apphosting:secrets:set KEY --project PROJECT_ID \
--location REGION \
--data-file DATA_FILE_PATH	Stores secret material in Secret Manager.
Optionally provide a file path from which to read secret data. Set to _ to read secret data from standard input.
apphosting:secrets:grantaccess KEY BACKEND_ID \
--project PROJECT_ID \
--location REGION	Grants the backend service account access to the provided secret so that it can be accessed by App Hosting at build or run time.
apphosting:secrets:describe KEY \
--project PROJECT_ID	Gets the metadata for a secret and its versions.
firebase apphosting:secrets:access \
KEY[@version] \
--project PROJECT_ID	Accesses a secret value given the secret and its version. Defaults to accessing the latest version.
Authentication (user management) commands
Command	Description
auth:export	Exports the active project's user accounts to a JSON or CSV file. For more details, refer to the auth:import and auth:export page.
auth:import	Imports the user accounts from a JSON or CSV file into the active project. For more details, refer to the auth:import and auth:export page.
Cloud Firestore commands
Command	Description
firestore:locations	
List available locations for your Cloud Firestore database.

firestore:databases:create DATABASE_ID	
Create a database instance in native mode in your Firebase project.

The command takes the following flags:

--location <region name> to specify the deployment location for the database. Note you can run firebase firestore:locations to list available locations. Required.
--delete-protection <deleteProtectionState> to allow or prevent deletion of the specified database. Valid values are ENABLED or DISABLED. Defaults to DISABLED.
--point-in-time-recovery <PITRState> to set whether point-in-time recovery is enabled. Valid values are ENABLED or DISABLED. Defaults to DISABLED. Optional.
firestore:databases:list	
List databases in your Firebase project.

firestore:databases:get DATABASE_ID	
Get database configuration for a specified database in your Firebase project.

firestore:databases:update DATABASE_ID	
Update database configuration of a specified database in your Firebase project.

At least one flag is required. The command takes the following flags:

--delete-protection <deleteProtectionState> to allow or prevent deletion of the specified database. Valid values are ENABLED or DISABLED. Defaults to DISABLED.
--point-in-time-recovery <PITRState> to set whether point-in-time recovery is enabled. Valid values are ENABLED or DISABLED. Defaults to DISABLED. Optional.
firestore:databases:delete DATABASE_ID	
Delete a database in your Firebase project.

firestore:indexes	
List indexes for a database in your Firebase project.

The command takes the following flag:

--database DATABASE_ID to specify the name of the database for which to list indexes. If not provided, indexes are listed for the default database.
firestore:delete	
Deletes documents in the active project's database. Using the CLI, you can recursively delete all the documents in a collection.

Note that deleting Cloud Firestore data with the CLI incurs read and delete costs. For more information, see Understand Cloud Firestore billing.

The command takes the following flag:

--database DATABASE_ID to specify the name of the database from which documents are deleted. If not specified, documents are deleted from the default database. Optional.
Cloud Functions for Firebase commands
Command	Description
functions:config:clone	Clones another project's environment into the active Firebase project.
functions:config:get	Retrieves existing configuration values of the active project's Cloud Functions.
functions:config:set	Stores runtime configuration values of the active project's Cloud Functions.
functions:config:unset	Removes values from the active project's runtime configuration.
functions:log	Reads logs from deployed Cloud Functions.
For more information, refer to the environment configuration documentation.

Crashlytics commands
Command	Description
crashlytics:mappingfile:generateid \
--resource-file=PATH/TO/ANDROID_RESOURCE.XML	Generates a unique mapping file ID in the specified Android resource (XML) file.
crashlytics:mappingfile:upload \
--app=FIREBASE_APP_ID \
--resource-file=PATH/TO/ANDROID_RESOURCE.XML \
PATH/TO/MAPPING_FILE.TXT	Uploads a Proguard-compatible mapping (TXT) file for this app, and associates it with the mapping file ID declared in the specified Android resource (XML) file.
crashlytics:symbols:upload \
--app=FIREBASE_APP_ID \
PATH/TO/SYMBOLS	Generates a Crashlytics-compatible symbol file for native library crashes on Android and uploads it to Firebase servers.
Data Connect commands
These commands and their use cases are covered in more detail in the Data Connect CLI reference guide.

Command	Description
dataconnect:services:list	Lists all deployed Data Connect services in your Firebase project.
dataconnect:sql:diff \
SERVICE_ID	For the specified service, displays the differences between a local Data Connect schema and your Cloud SQL database schema.
dataconnect:sql:migrate \
--force \
SERVICE_ID	Migrates your Cloud SQL database's schema to match your local Data Connect schema.
dataconnect:sql:grant\
--role=ROLE \
--email=EMAIL \
SERVICE_ID	Grants the SQL role to the specified user or service account email.
For the --role flag, the SQL role to grant is one of: owner, writer, or reader.
For the --email flag, provide the email address of the user or service account to grant the role to.
dataconnect:sdk:generate	Generates typed SDKs for your Data Connect connectors.
Extensions commands
Command	Description
ext	Displays information on how to use Firebase Extensions commands.
Lists the extension instances installed in the active project.
ext:configure \
EXTENSION_INSTANCE_ID	Reconfigures the parameter values of an extension instance in your extension manifest.
ext:info \
PUBLISHER_ID/EXTENSION_ID	Prints detailed information about an extension.
ext:install \
PUBLISHER_ID/EXTENSION_ID	Adds a new instance of an extension into your extension manifest.
ext:list	Lists all the extension instances installed in a Firebase project.
Prints the instance ID for each extension.
ext:uninstall \
EXTENSION_INSTANCE_ID	Removes an extension instance from your extension manifest.
ext:update \
EXTENSION_INSTANCE_ID	Updates an extension instance to the latest version in your extension manifest.
ext:export	Exports all installed extension instances from your project to your extension manifest.
Extensions publisher commands
Command	Description
ext:dev:init	Initializes a skeleton codebase for a new extension in the current directory.
ext:dev:list \
PUBLISHER_ID	Prints a list of all extensions uploaded by a publisher.
ext:dev:register	Registers a Firebase project as an extensions publisher project.
ext:dev:deprecate \
PUBLISHER_ID/EXTENSION_ID \
VERSION_PREDICATE	Deprecates extension versions that match the version predicate.
A version predicate can be a single version (such as 1.0.0), or a range of versions (such as >1.0.0).
If no version predicate is provided, deprecates all versions of that extension.
ext:dev:undeprecate \
PUBLISHER_ID/EXTENSION_ID \
VERSION_PREDICATE	Undeprecates extension versions that match the version predicate.
A version predicate can be a single version (such as 1.0.0), or a range of versions (such as >1.0.0).
If no version predicate is provided, undeprecates all versions of that extension.
ext:dev:upload \
PUBLISHER_ID/EXTENSION_ID	Uploads a new version of an extension.
ext:dev:usage \
PUBLISHER_ID	Displays install counts and usage metrics for extensions uploaded by a publisher.
Hosting commands
Command	Description
hosting:disable	
Stops serving Firebase Hosting traffic for the active Firebase project.

Your project's Hosting URL will display a "Site Not Found" message after running this command.

Management of Hosting sites
firebase hosting:sites:create \
SITE_ID	
Creates a new Hosting site in the active Firebase project using the specified SITE_ID

(Optional) Specify an existing Firebase Web App to associate with the new site by passing the following flag: --app FIREBASE_APP_ID

firebase hosting:sites:delete \
SITE_ID	
Deletes the specified Hosting site

The CLI displays a confirmation prompt before deleting the site.

(Optional) Skip the confirmation prompt by passing the following flags: -f or --force

firebase hosting:sites:get \
SITE_ID	
Retrieves information about the specified Hosting site

firebase hosting:sites:list	
Lists all Hosting sites for the active Firebase project

Management of preview channels
firebase hosting:channel:create \
CHANNEL_ID	
Creates a new preview channel in the default Hosting site using the specified CHANNEL_ID

This command does not deploy to the channel.

firebase hosting:channel:delete \
CHANNEL_ID	
Deletes the specified preview channel

You cannot delete a site's live channel.

firebase hosting:channel:deploy \
CHANNEL_ID	
Deploys your Hosting content and config to the specified preview channel

If the preview channel does not yet exist, this command creates the channel in the default Hosting site before deploying to the channel.

firebase hosting:channel:list	Lists all channels (including the "live" channel) in the default Hosting site
firebase hosting:channel:open \
CHANNEL_ID	Opens a browser to the specified channel's URL or returns the URL if opening in a browser isn't possible
Version cloning
firebase hosting:clone \
SOURCE_SITE_ID:SOURCE_CHANNEL_ID \
TARGET_SITE_ID:TARGET_CHANNEL_ID	
Clones the most recently deployed version on the specified "source" channel to the specified "target" channel

This command also deploys to the specified "target" channel. If the "target" channel does not yet exist, this command creates a new preview channel in the "target" Hosting site before deploying to the channel.

firebase hosting:clone \
SOURCE_SITE_ID:@VERSION_ID \
TARGET_SITE_ID:TARGET_CHANNEL_ID	
Clones the specified version to the specified "target" channel

This command also deploys to the specified "target" channel. If the "target" channel does not yet exist, this command creates a new preview channel in the "target" Hosting site before deploying to the channel.

You can find the VERSION_ID in the Hosting dashboard of the Firebase console.

Realtime Database commands
Note that you can create your initial, default Realtime Database instance in the Firebase console or by using the general firebase init workflow or the specific firebase init database flow.

Once instances are created, you can manage them as discussed in Manage multiple Realtime Database instances.

Command	Description
database:get	Fetches data from the active project's database and displays it as JSON. Supports querying on indexed data.
database:instances:create	Creates a database instance with a specified instance name. Accepts the --location option for creating a database in a specified region. For region names to use with this option, see select locations for your project. If no database instance exists for the current project, you are prompted to run the firebase init flow to create an instance.
database:instances:list	List all database instances for this project. Accepts the --location option for listing databases in a specified region. For region names to use with this option see select locations for your project.
database:profile	Builds a profile of operations on the active project's database. For more details, refer to Realtime Database operation types.
database:push	Pushes new data to a list at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
database:remove	Deletes all data at a specified location in the active project's database.
database:set	Replaces all data at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
database:update	Performs a partial update at a specified location in the active project's database. Takes input from a file, STDIN, or a command-line argument.
Remote Config commands
Command	Description
remoteconfig:versions:list \
--limit NUMBER_OF_VERSIONS	Lists the most recent ten versions of the template. Specify 0 to return all existing versions, or optionally pass the --limit option to limit the number of versions being returned.
remoteconfig:get \
--v, version_number VERSION_NUMBER
--o, output FILENAME	Gets the template by version (defaults to the latest version) and outputs the parameter groups, parameters, and condition names and version into a table. Optionally, you can write the output to a specified file with -o, FILENAME.
remoteconfig:rollback \
--v, version_number VERSION_NUMBER
--force	Rolls back Remote Config template to a specified previous version number or defaults to the immediate previous version (current version -1). Unless --force is passed, prompts Y/N before proceeding to rollback.
Send feedback
Except as otherwise noted, the content of this page is licensed under the Creative Commons Attribution 4.0 License, and code samples are licensed under the Apache 2.0 License. For details, see the Google Developers Site Policies. Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-06-04 UTC.

Learn
Developer guides
SDK & API reference
Samples
Libraries
GitHub
Stay connected
Check out the blog
Find us on Reddit
Follow on X
Subscribe on YouTube
Attend an event
Support
Contact support
Stack Overflow
Slack community
Google group
Release notes
Brand guidelines
FAQs
Google Developers
Android
Chrome
Firebase
Google Cloud Platform
All products
Terms
Privacy

English
The new page has loaded..

type User @table {
  displayName: String!
  email: String
  photoUrl: String
  shippingAddress: String
  createdAt: Timestamp!
}

type Product @table {
  name: String!
  description: String!
  price: Float!
  imageUrl: String!
  inventoryCount: Int
  category: String
  createdAt: Timestamp!
}

type Order @table {
  user: User!
  orderDate: Timestamp!
  totalAmount: Float!
  status: String!
  shippingAddress: String
  trackingNumber: String
}

type OrderItem @table {
  order: Order!
  product: Product!
  quantity: Int!
  price: Float!
}

type Category @table {
  name: String!
  description: String
  createdAt: Timestamp!
}

Skip to main content
Firebase
More
Search
/


English
Blog
Studio
Go to console

Documentation
Crashlytics
Overview
Fundamentals

AI

Build

Run

Test Lab
App Distribution
Crashlytics
Performance Monitoring
Remote Config
A/B Testing
Analytics
Cloud Messaging
In-App Messaging
Dynamic Links
Google AdMob
Google Ads
Reference
Samples
Filter

Here's everything we announced at I/O, from new Firebase Studio features to more ways to integrate AI. Read blog.
Firebase
Documentation
Crashlytics
Run
Was this helpful?

Send feedbackGet started with Firebase Crashlytics 

bookmark_border
iOS+ Android Flutter Unity


This quickstart describes how to set up Firebase Crashlytics in your app with the Firebase Crashlytics SDK so that you can get comprehensive crash reports in the Firebase console. With Crashlytics for Android, you get reports for crashes, non-fatal errors, and "Application Not Responding" (ANR) errors.

Setting up Crashlytics requires tasks both in the Firebase console and your IDE (like adding a Firebase configuration file and the Crashlytics SDK). To finish setup, you'll need to force a test crash to send your first crash report to Firebase.

Before you begin
If you haven't already, add Firebase to your Android project. If you don't have an Android app, you can download a sample app.

Recommended: To automatically get breadcrumb logs to understand user actions leading up to a crash, non-fatal, or ANR event, you need to enable Google Analytics in your Firebase project.

If your existing Firebase project doesn't have Google Analytics enabled, you can enable Google Analytics from the Integrations tab of your settings > Project settings in the Firebase console.

If you're creating a new Firebase project, enable Google Analytics during the project creation workflow.

Make sure your app has the following minimum required versions:

Gradle 8.0
Android Gradle plugin 8.1.0
Google services Gradle plugin 4.4.1
Step 1: Add the Crashlytics SDK to your app
Does your app use NDK? Go to the NDK crash reporting documentation to learn how to configure Crashlytics to report crashes that occur in your app's underlying NDK libraries.
In your module (app-level) Gradle file (usually <project>/<app-module>/build.gradle.kts or <project>/<app-module>/build.gradle), add the dependency for the Crashlytics library for Android. We recommend using the Firebase Android BoM to control library versioning.
To take advantage of breadcrumb logs, also add the Firebase SDK for Google Analytics to your app. Make sure that Google Analytics is enabled in your Firebase project.


dependencies {
    // Import the BoM for the Firebase platform
    implementation(platform("com.google.firebase:firebase-bom:33.15.0"))

    // Add the dependencies for the Crashlytics and Analytics libraries
    // When using the BoM, you don't specify versions in Firebase library dependencies
    implementation("com.google.firebase:firebase-crashlytics")
    implementation("com.google.firebase:firebase-analytics")
}
By using the Firebase Android BoM, your app will always use compatible versions of Firebase Android libraries.

(Alternative)  Add Firebase library dependencies without using the BoM

Looking for a Kotlin-specific library module? Starting in October 2023 (Firebase BoM 32.5.0), both Kotlin and Java developers can depend on the main library module (for details, see the FAQ about this initiative).
Step 2: Add the Crashlytics Gradle plugin to your app
In your root-level (project-level) Gradle file (<project>/build.gradle.kts or <project>/build.gradle), add the Crashlytics Gradle plugin to the plugins block:

Kotlin
Groovy
Are you still using the buildscript syntax? Learn how to add Firebase plugins using that syntax.
plugins {
    // Make sure that you have the AGP plugin 8.1+ dependency
    id("com.android.application") version "8.1.4" apply false
    // ...

    // Make sure that you have the Google services Gradle plugin 4.4.1+ dependency
    id("com.google.gms.google-services") version "4.4.2" apply false

    // Add the dependency for the Crashlytics Gradle plugin
    id("com.google.firebase.crashlytics") version "3.0.4" apply false
}
Is your app using a lower version of Gradle? Consider upgrading; otherwise, you should use v2.9.9 of the Crashlytics Gradle plugin.
In your module (app-level) Gradle file (usually <project>/<app-module>/build.gradle.kts or <project>/<app-module>/build.gradle), add the Crashlytics Gradle plugin:

Kotlin
Groovy
plugins {
  id("com.android.application")
  // ...

  // Make sure that you have the Google services Gradle plugin
  id("com.google.gms.google-services")

  // Add the Crashlytics Gradle plugin
  id("com.google.firebase.crashlytics")
}
Step 3: Force a test crash to finish setup
To finish setting up Crashlytics and see initial data in the Crashlytics dashboard of the Firebase console, you need to force a test crash.

Add code to your app that you can use to force a test crash.

You can use the following code in your app's MainActivity to add a button to your app that, when pressed, causes a crash. The button is labeled "Test Crash".

Kotlin
Java
val crashButton = Button(this)
crashButton.text = "Test Crash"
crashButton.setOnClickListener {
   throw RuntimeException("Test Crash") // Force a crash
}

addContentView(crashButton, ViewGroup.LayoutParams(
       ViewGroup.LayoutParams.MATCH_PARENT,
       ViewGroup.LayoutParams.WRAP_CONTENT))
Build and run your app.

Force the test crash in order to send your app's first crash report:

Open your app from your test device or emulator.

In your app, press the "Test Crash" button that you added using the code above.

After your app crashes, restart it so that your app can send the crash report to Firebase.

Go to the Crashlytics dashboard of the Firebase console to see your test crash.

If you've refreshed the console and you're still not seeing the test crash after five minutes, enable debug logging to see if your app is sending crash reports.



And that's it! Crashlytics is now monitoring your app for crashes, non-fatal errors, and ANRs. Visit the Crashlytics dashboard to view and investigate all your reports and statistics.

Next steps
Customize your crash report setup by adding opt-in reporting, logs, keys, and tracking of non-fatal errors.
Integrate with Google Play so that you can filter your Android app's crash reports by Google Play track directly in the Crashlytics dashboard. This allows you to better focus your dashboard on specific builds.
In Android Studio, view and filter Crashlytics data.
Use the App Quality Insights (AQI) window in Android Studio to view Crashlytics data alongside your code — no need to jump back and forth between the Crashlytics dashboard and the IDE to start debugging top issues.
Learn how to use the AQI window in the Android Studio documentation.
We'd love to hear from you! Send us feedback about the AQI window by filing a bug report.
Send feedback
Except as otherwise noted, the content of this page is licensed under the Creative Commons Attribution 4.0 License, and code samples are licensed under the Apache 2.0 License. For details, see the Google Developers Site Policies. Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2025-06-12 UTC.

Learn
Developer guides
SDK & API reference
Samples
Libraries
GitHub
Stay connected
Check out the blog
Find us on Reddit
Follow on X
Subscribe on YouTube
Attend an event
Support
Contact support
Stack Overflow
Slack community
Google group
Release notes
Brand guidelines
FAQs
Google Developers
Android
Chrome
Firebase
Google Cloud Platform
All products
Terms
Privacy

English



