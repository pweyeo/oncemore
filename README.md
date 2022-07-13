# eyeo Developer Docs Repository

This repository contains the code for eyeo's developer documentation site, which provides content oriented towards developers and filter-list authors.

On this page, you'll find information on how to contribute to the site and how the site is built.

## Docs site overview

Keep the following in mind when working within this repository:

- The docs site is powered by [Hugo](https://gohugo.io/).
- The site uses the open-source [Doks](https://getdoks.org/) theme.
- [Netlify](https://www.netlify.com/) builds and deploys the site from the `main` branch.
- The repository's working branch is `development`.

## Contributing to the site

Anyone at eyeo can contribute to the site's content.

### Contributing outside of GitLab

If you'd like to add or request a change to the docs site but prefer not to use git or GitLab, please post a message in the #developer-docs Mattermost channel or create a ticket on the Jira documentation board.

### Contributing using GitLab

You can contribute directly to the repository in two ways:

- Create a merge request using the GitLab UI.
- Clone the repository and push your commits remotely.

#### Requesting changes using the GitLab UI

To request a change using the GitLab UI, first make sure that you have a GitLab account within the eyeo organization.

Sign in to your GitLab account, then follow these instructions:

1. Create a branch of the `development` branch.
2. Navigate to the file you want to change, then make your edits.
3. Add a commit message describing the requested change.
4. Create and submit a merge request.

#### Cloning the repository and making changes remotely

If you'd prefer to work with your own tools or would like to change multiple repository files, follow these instructions:

1. Clone this repository to your local device.
2. Using the command line or your text editor, run the `git checkout -b your-branch-name` command to create and switch to a new branch.
3. Open the file(s) you want to change, then make your edits.
4. Use the CLI or your text editor to add and commit your changes.
5. Push your branch to the repository.
6. Create and submit a merge request.

## Deploys

Changes merged into `development` branch are merged into the `main` branch on a regular basis. Netlify then builds and deploys any changes to the `main` branch.

If you're requesting a time-sensitive change, please mention it in the body of your merge request.

## Feedback and questions

If you have any questions or feedback, feel free to post a message in the #developer-docs Mattermost channel or message @pwooley on Mattermost.
