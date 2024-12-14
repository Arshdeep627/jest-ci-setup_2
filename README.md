# GitHub Actions and Jest Testing

## Introduction
This project demonstrates the use of GitHub CLI and GitHub Actions to automate Jest tests. It is part of an assignment to practice creating YAML files and automating workflows. The repository includes the setup of Jest for unit testing and the creation of a GitHub Actions workflow to automatically run tests on every push to the main branch.

## Prerequisites
Before setting up the project, ensure the following tools are installed:
- **GitHub CLI**: To manage repositories and authenticate with GitHub directly from the terminal.
- **Node.js**: Required for running Jest and other dependencies.
- **Jest**: The testing framework used in this project.

## Steps to Set Up

### 1. Install GitHub CLI
To install the GitHub CLI, follow the instructions on the official website: [GitHub CLI Installation](https://cli.github.com/). Once installed, verify by running:
```bash
gh --version
This should display the version of the GitHub CLI installed.

2. Authenticate GitHub CLI
Authenticate the GitHub CLI to connect it to your GitHub account:
gh auth login
Select HTTPS when prompted, and paste your Personal Access Token (PAT) when asked for the password.

3. Clone the Repository
Clone your repository locally using the following commands:
gh repo clone <username>/<repository-name>
cd <repository-name>

4. Set Up Jest
Initialize a Node.js project and install Jest:
npm init -y
npm install jest --save-dev
mkdir __tests__
touch __tests__/example.test.js
In the __tests__/example.test.js file, add the following test:

test('adds 1 + 2 to equal 3', () => {
  expect(1 + 2).toBe(3);
});

Run the tests locally to ensure Jest is set up correctly:
npx jest

5. Commit and Push Code to GitHub
Add, commit, and push the changes to GitHub:
git add .
git commit -m "Initial project setup"
git push -u origin main

6. Set Up GitHub Actions Workflow
Create a .github/workflows/ci.yml file to automate Jest tests on every push:

name: Jest CI

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '16'
      - run: npm install
      - run: npm test

Commit and push the workflow file:
git add .github/workflows/ci.yml
git commit -m "Add CI workflow"
git push

7. Test the Workflow
To test the workflow, make a small change in your code and push:
echo "// Test change" >> index.js
git add .
git commit -m "Test workflow"
git push
Visit the Actions tab in your GitHub repository to see the workflow run and check the Jest test results.

Challenges Faced
Permission Denied Error: While running Jest tests in the workflow, I encountered a "Permission denied" error. This was resolved by ensuring that the necessary permissions were granted to the Node modules directory using the chmod +x command.
Conclusion
This project successfully demonstrates the integration of GitHub CLI, Jest, and GitHub Actions to automate testing workflows. The workflow runs Jest tests on every push to the main branch, ensuring that tests are always up-to-date and pass successfully.

