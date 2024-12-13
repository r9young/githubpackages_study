# Note for the project

## Github pakcages
ref: https://docs.github.com/en/packages/quickstart#publishing-your-package

## From Step 6 to Step 9:

6. Create a .github/workflows directory in the root of your repository.
7. Create a new file in the .github/workflows directory with a name that ends in .yml. For example, .github/workflows/release-package.yml.
8. Tell npm which scope and registry to publish packages.
9. Push your changes to GitHub.
10. Create a release.

# Common Questions:

## 1. What does the release: types: [created] in a GitHub Actions workflow mean?


You are asking me to explain the **GitHub Actions workflow syntax** specifically for the `on: release: types: [created]` trigger. Here is a clear breakdown:

---

### **Workflow Syntax: GitHub Actions**

GitHub Actions uses **YAML syntax** to define workflows. Each workflow describes a set of automated tasks that are executed in response to events.

The syntax:

```yaml
on:
  release:
    types: [created]
```

### **Explanation**:

1. **`on` keyword**:
   - Specifies the **event** that triggers the workflow.
   - This could be `push`, `pull_request`, `schedule`, `workflow_dispatch`, `release`, etc.

2. **`release` event**:
   - Refers to GitHub **release events**.
   - A release event is triggered when actions related to releases occur (e.g., creating, publishing, editing, deleting releases).

### **How It Works**:
1. When a new **GitHub Release** is created in your repository, the `on: release: types: [created]` trigger activates the workflow.
2. The workflow runs the `build` job, which executes the defined steps (e.g., checking out the code and printing a message).


---

## 2. What is meant by a "new release" in GitHub?


In a simplified view, a release can be seen as a way to:

- Version your project.
- Automatically package it as downloadabler zip
- Optionally attach addtional zipped files


## 3. What is the relationship between GitHub Releases and npm publishing configuration (.npmrc and publishConfig)?

npm Configuration (.npmrc and publishConfig):

- These settings tell npm where to publish packages.
- The publishConfig key in package.json and .npmrc file specify the registry (e.g., GitHub Package Registry).


## 4.  Is the release: created trigger used to publish packages to GitHub Package Registry (GPR)?

Yes, the answer is **no**:  

There is **no direct relationship** between GitHub Releases and the `npm` configuration files (`.npmrc` and `publishConfig`).  

---

### **Why?**  
- **GitHub Releases**: These are for **versioning and distributing** project snapshots (like code or binaries) in a human-readable way.  
- **npm Configuration**: These are for **publishing packages** to a registry (like GitHub Package Registry or npm).

---

### **Indirect Connection (Only Through the Workflow)**  
- In the **workflow file**, the GitHub Release event (`release: created`) acts as a **trigger** for the GitHub Actions workflow.  
- Inside the workflow, the `npm publish` command uses `.npmrc` and `publishConfig` settings.  

So, the **connection exists indirectly** through the workflow automation, **not directly**.

---

### Final Answer:  
The **relationship is indirect** because the workflow bridges GitHub Releases and npm publishing, but they are **not inherently related**. 🚀

## 5. Why did the workflow run before I manually created a release?

the workflow will not run before creating a release in this case.




