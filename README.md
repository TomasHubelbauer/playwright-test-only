# Playwright `test.only`

I ran into an issue with `test.only` in Playwright in a work project.

In this repository I am trying to reproduce the issue.

I set up both the work repository and this one by following the Getting Started
guide on https://playwright.dev with the exception that the work repository is a
monorepo that uses PNPM and I do not yet know if that makes a difference.

https://playwright.dev/docs/intro

1. `npm init playwright@latest` (I am using Node 20.2.0 and NPM 9.6.6)
   
   - TypeScript because that's what the work repository is using
  
     I don't know if the same issue reproduces in JavaScript.
   
   - `tests` as the directory for the tests

     In the work repository, I moved them straight to the directory root, but I
     do not think this matters.
     I will play around with this if I gain a suspicion it might play a role.
   
   - No to adding the GitHub Actions workflow

     I do make use of it in the work repository, but this problem happens in the
     IDE not in the workflow runtime so this should be unnecessary.

   
   - Install Playwright browsers automatically

     The workflow repository does it too and the workflow updates them there.

   At this point `npx playwright test` works successfully when I add `test.todo`
   to one of the generated sample tests.

2. Remove the non-Chromium projects

   The reproduction should be unrelated to the browser at hand so let's simplify
   the setup.

3. Change `playwright.config.ts` to look for tests in the repository directory
   root instead of in `tests`.
   
   - Change `testDir` from `./tests` to `.`.

   Maybe this does play a role after all?
   Looks like that's not the case, `npx playwright test` still runs the sole
   test.

4. Be confused.
   Next step: let's try to extract the reproduction out from the work repository
   instead.

   I will replace this repository with the result of that if I succeed.

   It is possible I just need to bump Playwright version in that repository?
