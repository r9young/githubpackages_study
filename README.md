# **Project Notes**

## Purpose of Notes:

The purpose of these notes is to address common questions about learning GitHub Packages. The notes cover setting up GitHub Packages, configuring GitHub Actions, and automating package publishing and create a release.


## Key process of the project:

The project involves creating a basic Node.js project with version control. 
Then it create a workflow to automate the publishing of the package to GitHub Packages using GitHub Actions.
The workflow triggers when a new release is created on GitHub.

So the whole process is: 

1. Create a Node.js project.
2. Create a workflow file which triggers when a new release is created.
3. Setting up an configuration file for the repository
4. a new release is created on GitHub.
5. The workflow runs and publishes the package to GitHub Packages.

So the step 2 and 5 are the key steps in the project. as we create a workflow file in step 3 and then we create a release in step 4 and the workflow runs and publishes the package to GitHub Packages.

## **Reference**
For more details, refer to the [GitHub Packages Documentation](https://docs.github.com/en/packages/quickstart#publishing-your-package).

---

## **Steps 6 to 10: Setting up GitHub Actions**
Follow these steps to configure and automate publishing:

1. **Create a `.github/workflows` directory** in the root of your repository.
2. **Add a new workflow file** in the `.github/workflows` directory. For example:  
   ```plaintext
   .github/workflows/release-package.yml
   ```
3. **Configure npm for scoped publishing**:
   - Use `.npmrc`:
     ```plaintext
     @YOUR-USERNAME:registry=https://npm.pkg.github.com
     ```
   - Or add the `publishConfig` key in `package.json`:
     ```json
     "publishConfig": {
       "@YOUR-USERNAME:registry": "https://npm.pkg.github.com"
     }
     ```
4. **Push your changes** to GitHub.
5. **Create a release**.

---

# **Common Questions**

### **1. What does `release: types: [created]` in a GitHub Actions workflow mean?**

GitHub Actions uses YAML to define workflows. Here's the relevant snippet:

```yaml
on:
  release:
    types: [created]
```

**Explanation**:
- `on`: Specifies the event that triggers the workflow.
- `release`: Refers to release-related events in GitHub.
- `types: [created]`: The workflow triggers when a **new release** is created.

**How It Works**:
- When you create a release on GitHub, the `release: created` event starts the workflow.
- This allows you to automate actions like building, testing, or publishing packages.

---

### **2. What is a "new release" in GitHub?**

A **GitHub Release** allows you to:
- **Version your project** (e.g., `v1.0.0`).
- Package your project as a downloadable `.zip` or `.tar` file.
- Optionally attach additional files (e.g., prebuilt binaries or assets).

Releases are a way to **share project milestones** with users.

---

### **3. What is the relationship between GitHub Releases and npm publishing configuration?**

- **GitHub Releases**: Used for **versioning** and sharing snapshots of your code (human-readable).  
- **npm Configurations**:
   - `.npmrc` and `publishConfig` tell `npm` **where to publish** packages (e.g., GitHub Package Registry).

There is **no direct relationship** between GitHub Releases and npm configurations.  

---

### **4. Does `release: created` automatically publish packages to GitHub Package Registry (GPR)?**

The answer is **no**.  

**Why?**  
- GitHub Releases and npm publishing are independent features.  
- The `release: created` trigger **does not directly publish packages**.  

**Indirect Connection**:  
A GitHub Actions workflow bridges the two:
- The workflow triggers on `release: created`.  
- Inside the workflow, you can add steps to run `npm publish`, which uses `.npmrc` and `publishConfig`.

**Summary**:  
The **connection exists indirectly** through the workflow file, but they are **not inherently related**.

---

### **5. Why did the workflow run before I manually created a release?**

If configured correctly, the workflow **will not run** until a release is manually created.

Check that:
- The `on: release: types: [created]` trigger is properly set.
- No other event (`push`, `workflow_dispatch`, etc.) is mistakenly triggering the workflow.

---

### **Final Notes**
- Use GitHub Releases to **version and share your project**.
- Use GitHub Actions to **automate npm publishing** by linking the release trigger to `npm publish`.

🚀 Let me know if you need further clarifications or examples!