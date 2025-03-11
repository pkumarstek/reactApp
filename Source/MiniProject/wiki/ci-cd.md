To set up a **CI/CD pipeline** for your React To-Do List mini-project using **GitHub Actions**, you'll need to create a **YAML file** that defines the workflow. Additionally, we'll organize the project with an **enterprise-standard folder structure** to store the YAML file and other configuration files.

---

### **Enterprise-Standard Folder Structure**

Here’s the recommended folder structure for your mini-project:

```
todo-app/
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # GitHub Actions workflow file
├── src/                       # React source code
│   ├── components/
│   ├── App.js
│   ├── App.css
│   └── index.js
├── public/                    # Static assets
│   ├── index.html
│   └── favicon.ico
├── tests/                     # Test files
│   └── App.test.js
├── .gitignore                 # Files to ignore
├── package.json               # Project dependencies
├── README.md                  # Project documentation
└── LICENSE                    # License file (optional)
```

---

### **Step 1: Create the GitHub Actions Workflow File**

1. Create a `.github/workflows/` directory in the root of your project.
2. Inside the `workflows` directory, create a file named `ci-cd.yml`.

---

### **Step 2: Define the CI/CD Pipeline**

Below is an example of a **CI/CD pipeline** for a React app using GitHub Actions. This pipeline will:

1. Run tests.
2. Build the app.
3. Deploy the app to **GitHub Pages**.

#### **`.github/workflows/ci-cd.yml`**

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main # Trigger the workflow on pushes to the main branch
  pull_request:
    branches:
      - main # Trigger the workflow on pull requests to the main branch

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      # Step 1: Checkout the repository
      - name: Checkout code
        uses: actions/checkout@v3

      # Step 2: Set up Node.js
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18 # Use the Node.js version your app requires

      # Step 3: Install dependencies
      - name: Install dependencies
        run: npm install

      # Step 4: Run tests
      - name: Run tests
        run: npm test

  build:
    runs-on: ubuntu-latest
    needs: test # Ensure the build job runs only if tests pass

    steps:
      # Step 1: Checkout the repository
      - name: Checkout code
        uses: actions/checkout@v3

      # Step 2: Set up Node.js
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18

      # Step 3: Install dependencies
      - name: Install dependencies
        run: npm install

      # Step 4: Build the app
      - name: Build the app
        run: npm run build

      # Step 5: Upload build artifacts
      - name: Upload build artifacts
        uses: actions/upload-artifact@v3
        with:
          name: build
          path: build/

  deploy:
    runs-on: ubuntu-latest
    needs: build # Ensure the deploy job runs only if the build job succeeds

    steps:
      # Step 1: Checkout the repository
      - name: Checkout code
        uses: actions/checkout@v3

      # Step 2: Set up Node.js
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18

      # Step 3: Install dependencies
      - name: Install dependencies
        run: npm install

      # Step 4: Build the app
      - name: Build the app
        run: npm run build

      # Step 5: Deploy to GitHub Pages
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build # The folder where your built files are located
```

---

### **Step 3: Configure GitHub Pages**

1. Go to your GitHub repository.
2. Navigate to **Settings** > **Pages**.
3. Under **Source**, select the `gh-pages` branch and the `root` folder.
4. Save the settings.

---

### **Step 4: Push the Code to GitHub**

1. Add the `.github/workflows/ci-cd.yml` file to your repository.
2. Commit and push the changes:
   ```bash
   git add .
   git commit -m "Add CI/CD pipeline"
   git push origin main
   ```

---

### **Step 5: Monitor the Workflow**

1. Go to the **Actions** tab in your GitHub repository.
2. You should see the workflow running. If everything is set up correctly, it will:
   - Run tests.
   - Build the app.
   - Deploy the app to GitHub Pages.

---

### **Step 6: Access Your Deployed App**

Once the workflow completes, your app will be live at:

```
https://<username>.github.io/<repository-name>
```

---

### **Enterprise Best Practices for CI/CD**

1. **Environment Variables**:

   - Use GitHub Secrets to store sensitive information (e.g., API keys).

2. **Branch Protection**:

   - Enable branch protection rules for the `main` branch to require status checks before merging.

3. **Artifact Storage**:

   - Use GitHub Actions artifacts to store build outputs for debugging.

4. **Notifications**:

   - Set up notifications for workflow failures (e.g., email, Slack).

5. **Testing**:
   - Include unit tests, integration tests, and end-to-end tests in your pipeline.

---

By following this guide, you’ll have a **CI/CD pipeline** set up for your React To-Do List app using GitHub Actions, along with an **enterprise-standard folder structure**. This ensures your project is scalable, maintainable, and ready for collaboration. 🚀
