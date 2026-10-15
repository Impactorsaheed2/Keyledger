# GitHub-to-Vercel deployment

This guide deploys the **current browser-only KeyLedger preview**. It does not add authentication, a database, Supabase, or cloud storage. A successful Vercel deployment does not make browser-local records private or protected.

## Before you start

The ZIP contains the application source and configuration at its root, including `package.json` and `package-lock.json`. It intentionally excludes generated `.next` output and `node_modules`; those are recreated during installation/build. Node.js 18.18+ is supported by the installed Next.js version; use Node.js 22 LTS where a version choice is available.

## Deploy with GitHub and Vercel

1. **Save the package.** Download and extract `KeyLedger-browser-only-deployment.zip`. Keep the folder structure intact. The extracted `package.json` should be at the project root.
2. **Upload to GitHub.** Create a repository, then use GitHub's web upload flow or Git to add the extracted project files and commit them. Include `package-lock.json`; do not upload `node_modules`, `.next`, `.env.local`, or real secrets.
3. **Import the repository in Vercel.** In Vercel, choose **Add New → Project**, connect GitHub if needed, and select the repository you just created.
4. **Set the project root.** If you uploaded the ZIP contents directly into the repository root, choose `./`. If you placed them in a subfolder, select that folder instead.
5. **Choose the framework preset.** Select **Next.js** (usually detected automatically).
6. **Check build settings.** Use `npm run build` as the build command. Leave the output directory at Vercel's Next.js default; do not set a static `out` directory. Use the lockfile-based/default install command.
7. **Set environment variables.** None are required for this browser-only app. `.env.example` is informational only; copying it to `.env.local` is unnecessary. Never add a Supabase service-role key or other private key to frontend variables.
8. **Deploy.** Select **Deploy** and wait for the first build to finish. Vercel will build the Next.js app from the committed source.
9. **Review deployment logs.** Open the deployment's **Build Logs**. Confirm dependency installation and `next build` complete successfully. If the build fails, check the selected root directory, framework preset, and build log; then commit any correction and redeploy.
10. **Smoke-test the deployed app.** Open the deployment URL and check `/`, `/expenses`, `/reports`, `/budgets`, `/recurring`, and `/data`. Add, edit, search, and remove a disposable test expense; verify dashboard totals update. These checks test the preview only, not authentication or server-side storage.
11. **Supabase redirect URLs: not applicable.** This project has no Supabase client or authentication. There are no callback URLs to configure. Do not create Supabase settings for this package; adding Supabase later requires a separate implementation and security review.
12. **Understand the data boundary.** Records are stored by the browser at this site's origin. Different browsers/devices and different site origins do not share records. Before moving to a different domain, download a JSON backup from **Data tools** and restore it at the new domain. The backup is not encrypted. There is no sign-in, account separation, server-side access control, or Row Level Security; do not treat deployed records as private or use this preview for sensitive multi-user data.

## Environment variables

| Variable | Required? | Purpose |
|---|---:|---|
| None | No | The current app has no external service connection. |

`.env.example` contains no values because no environment variables are used. Keep `.env*` files out of Git except the provided example. Never publish a service-role key.

## Common deployment issues

- **`package.json` not found:** the selected Vercel root directory is wrong. Point it to the folder containing `package.json` and `package-lock.json`.
- **Dependency/build failure:** use Node.js 22 LTS if selectable, confirm the committed lockfile matches `package.json`, and inspect the first error in Build Logs.
- **Wrong framework/output setting:** use the Next.js preset and leave the output directory on Vercel's automatic Next.js setting.
- **Changes appear missing after a domain change:** browser local storage is origin-scoped. Restore a JSON backup on the new origin; Vercel deployments do not transfer this browser data.
- **No sign-in or cross-device sync:** expected for this package; those features are not implemented.
- **Receipt upload or voice capture behaves differently:** receipt files are local-only, and voice support depends on the browser. Neither feature is a cloud integration.

## Deployment status

These instructions are based on the checked-in project configuration. **This package was not deployed to a Vercel account as part of verification.** See [VERIFICATION.md](./VERIFICATION.md) for the actual checks and remaining limitations.
