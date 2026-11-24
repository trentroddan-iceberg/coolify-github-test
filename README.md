# Coolify GitHub deployment test

This one-file website is a test fixture for a private GitHub repository. It has no package installation, frontend build, database, environment variables or external assets. This package has been prepared locally; it has not been deployed to your server.

## 1. Create the repository

Create a private GitHub repository named `coolify-github-test`. Extract this ZIP and upload `index.html` and this README directly to the repository root. Upload the files, not the ZIP itself or its enclosing folder. Commit the files and note the repository's actual default branch.

## 2. Check the GitHub App connection

In Coolify, open Sources and select the GitHub App for the intended GitHub account or organisation. Registration and installation are separate steps: the App must be installed with access to this test repository. If access is restricted to selected repositories, add the new test repository to that selection.

If no GitHub App source exists, create one using Coolify's automated GitHub App setup. For a personal account, leave the organisation field empty. Register the App, then install it for the selected test repository. Use a publicly reachable Coolify URL for webhooks.

## 3. Create the application

Create a Coolify project called `Deployment Test` and use its default environment, or create an environment called `test` if preferred. Add a resource through Private Repository (with GitHub App), select the deployment server, choose the connected App, and load the private test repository.

| Setting | Value |
| --- | --- |
| Branch | The branch containing index.html |
| Build pack / build strategy | Static |
| Base directory | / |
| Web server | Default Nginx |
| Internal container port, if requested | 80 |
| Install, build and start commands | Leave unset; Static serves the committed HTML |
| Database and environment variables | None |
| Domain | A test hostname resolving to your VPS, or a working generated hostname |

Use Coolify's proxy for the domain. No additional host-port mapping is needed for this test. Deploy, open Deployment Logs and verify the expected repository, branch and commit. Open the test URL and look for `Version 1`.

## 4. Verify automatic deployment

Open the application's Advanced > Deployment settings. Set Auto deploy to Deploy on push (webhooks), if not already enabled. Labels may vary slightly by UI version.

On GitHub, edit this exact HTML line:

```html
<p class="version">Version 1</p>
```

Change it to:

```html
<p class="version">Version 2</p>
```

Commit to the configured branch. Do not press Deploy manually for this check. Confirm all three results:

1. Coolify starts a new deployment automatically.
2. Its commit matches the GitHub change and the deployment succeeds.
3. The live test page displays Version 2 after a refresh.

A successful first deployment confirms repository cloning and static hosting. The second deployment confirms the push-triggered update path. Neither test validates the Python backend, database, file storage or integrations of an Emergent application.

## If automatic deployment does not start

Check the configured branch and Auto deploy setting. For a GitHub App, inspect webhook deliveries under the App's settings; its webhook is not necessarily listed under the individual repository's Settings > Webhooks. Check that GitHub can reach the App webhook endpoint at your Coolify instance.

## Next: one Emergent application

Inspect the exported repository first. Confirm its frontend, backend, database, build and start commands, environment variable names, uploaded-file storage and external authentication or AI integrations. Deploy it to a test hostname with separate test data before changing a live domain.

## Official references

- GitHub App setup: https://coolify.io/docs/applications/sources/github/app
- Static build strategy: https://coolify.io/docs/applications/builds/static
- Automatic deployment: https://coolify.io/docs/applications/sources/github/auto-deploy
- Domains and routing: https://coolify.io/docs/core/networking/domains

Prepared 23 November 2026 against the current official documentation. Your live dashboard determines the exact labels and current connection status.
