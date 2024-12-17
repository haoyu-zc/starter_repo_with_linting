This repository contains starter configurations for the conventional commit messages as described [here](https://www.conventionalcommits.org/en/v1.0.0/), as well as linter configurations for Python and R.

## How this repository was created
Init repository:
```bash
git init
```

Install Node.js:
    
```bash
# installs nvm (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
# download and install Node.js (you may need to restart the terminal)
nvm install 22
# verifies the right Node.js version is in the environment
node -v # should print `v22.12.0`
# verifies the right npm version is in the environment
npm -v # should print `10.9.0`
```

Install pnpm:

```bash
npm install -g pnpm
```

Install and Init Husky:
```bash
pnpm add --save-dev husky
pnpm exec husky init
```

Install Commitlint CLI and the conventional configuration as development dependencies:
```bash
pnpm add -D @commitlint/config-conventional @commitlint/cli
# extend the Commitlint conventional configuration
echo "export default { extends: ['@commitlint/config-conventional'] };" > commitlint.config.js
```

create a commit-msg file in the .husky folder to add commit message linting to commit-msg hook.
```bash
echo "pnpm dlx commitlint --edit $1" > .husky/commit-msg
# Remove the pre-commit hook created by Husky on initialization
rm .husky/pre-commit
```


## How to use this repository
You'll need to install both Node.js and pnpm to utilize the commit rules configured for this repo.

If you have not, refer to this [link](https://nodejs.org/en/download/package-manager) to install Node.js and this [link](https://pnpm.io/installation) to install pnpm.

Then, run this command at the root of the repository to install the required packages:

```bash
pnpm install
```

Now you can try edit a file and commit it with a unconventional commit message.

```bash
echo "A Random Sentence" >> README.md
git add README.md
git commit -m "A Random Commit Message"
```

You'll see a warning message and the commit will be rejected:

```bash
⧗   input: A Random Commit Message
✖   subject may not be empty [subject-empty]
✖   type may not be empty [type-empty]

✖   found 2 problems, 0 warnings
ⓘ   Get help: https://github.com/conventional-changelog/commitlint/#what-is-commitlint

husky - commit-msg script failed (code 1)
```

You can use an interactive CLI to help you get familiar with the convention by running `pnpm run commit`.
