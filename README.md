# Deploy Remix to cPanel-type sites

If your hosting provider only allows you to run the node entrypoint for your web app
and does not let your build your app directly, you can use these deployment scripts
to setup a GitHub action that handles this for you.

The deployment script runs `npm run build` which does the following

- Builds your Remix app in production mode
- Runs `esbuild` to bundle your app into a single file (so no need to have node_modules on server)

The finally it runs the `ftp-action` to copy `dist/index.js` and `public/*` files to your host

NOTE: You need to configure the FTP credentials using GitHub Action Secrets. Navigate to
you repository Settings. Select Security > Secrets > Actions. Then add repository secrets
for:

- FTP_SERVER
- FTP_USERNAME
- FTP_PASSWORD.

On you your host, you can then point to the `index.js` file as your app's entry point.
Make sure the the `public` folder is copied as is. There should be `public` folder at
the root of your app.

The GitHub action will automatically everytime you push your code. You can also manually
deploy using the GitHub action page.
