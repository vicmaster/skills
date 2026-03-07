---
name: deploy
description: Deploy the application to the specified environment
disable-model-invocation: true
argument-hint: [environment]
---

# Deploy

Deploy the application to $ARGUMENTS.

## Instructions

1. Check the current branch and ensure it's clean (`git status`)
2. Run the full test suite — abort if tests fail
3. Run the build process — abort if build fails
4. Determine the deployment method:
   - Check for deployment scripts in `package.json`, `Makefile`, or CI config
   - Look for platform-specific configs (Vercel, Railway, Fly.io, AWS, etc.)
5. Execute the deployment
6. Verify the deployment succeeded (check logs, health endpoint, etc.)
7. Report the deployment status and URL if available
