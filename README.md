# Setting Up a Global Environment for Python Projects

This README provides a structured guide to create and use a global Python environment that allows shared access to certain libraries, minimizing redundancy and storage issues when working across multiple projects.

---

## **Purpose**

When working on multiple Python projects, creating isolated virtual environments often leads to redundant installations of common packages like `numpy`, `pandas`, or `scikit-learn`. A global environment solves this problem by:

- Allowing shared access to globally installed libraries.
- Reducing storage usage by avoiding duplicate package installations.
- Simplifying setup for frequently used packages.

---

## **Steps to Create and Use a Global Environment**

### **1. Create a Global Virtual Environment**

Run the following command to create a virtual environment that can access globally installed packages:

```bash
pythonx.yy -m venv ~/global_env --system-site-packages
```

- `~/global_env`: The directory where the global environment will be created. You can replace this with your preferred location.
- `--system-site-packages`: Enables the environment to access Python packages installed globally.

---

### **2. Activate the Environment**

To use the global environment, activate it with:

#### On macOS/Linux:

```bash
source ~/global_env/bin/activate
```

#### On Windows:

```cmd
~/global_env\Scripts\activate
```

Once activated, you can use the global environment for your Python projects.

---

### **3. Install Additional Packages**

If you need to install new packages that are not globally available, you can install them directly into the global environment. For example:

```bash
pip install pandas
```

These packages will only be available within the global environment.

To install packages from a `requirements.txt`, use the following command:

```bash
pip install --requirement /path/to/requirements.txt
```

Or:

```bash
pip install -r /path/to/requirements.txt
```

Specify the version you need if necessary in the requirements.txt, following example:

```text
package==x.yy.zz
```

---

### **4. Use the Global Environment in Projects**

#### **PyCharm**

To use the global environment in PyCharm:

1. Open the project settings.
2. Go to **Python Interpreter**.
3. Click **Add Interpreter** > **Existing Environment**.
4. Browse to the path of the `python` executable in `~/global_env/bin/` (or `~/global_env\Scripts\` on Windows).

#### **Other Editors/IDEs**

Specify the path to `~/global_env/bin/python` as the interpreter for your project.

---

### **5. Verify Package Access**

To check if a package like `numpy` is accessible from the global environment:

```bash
python -c "import numpy; print(numpy.__version__)"
```

If the package is found and the version is printed, the setup is working correctly.

---

### **6. Enable Global Packages in an Existing Virtual Environment**

If you want an existing virtual environment to access global packages:

1. Locate the `pyvenv.cfg` file in the virtual environment directory.
2. Open the file and update the following line:
   ```plaintext
   include-system-site-packages = true
   ```
3. Reactivate the virtual environment.

---

## **Best Practices**

- **Avoid Installing Too Many Global Packages:** Limit global installations to frequently used, lightweight libraries (e.g., `numpy`, `scipy`). Install project-specific packages within project environments.
- **Keep the Global Environment Updated:** Periodically update packages in the global environment to avoid compatibility issues:
  ```bash
  pip list --outdated
  pip install --upgrade <package-name>
  ```
- **Use Virtual Environments for Large Projects:** For projects with unique or conflicting dependencies, create isolated virtual environments instead of relying on the global one.

---

## **Troubleshooting**

### **Global Package Not Found**

If a globally installed package is not accessible:

- Ensure the `--system-site-packages` flag was used when creating the global environment.
- Verify that the global package is installed via:
  ```bash
  pip list --user
  ```

### **Conflict Between Global and Local Packages**

If a package installed in the global environment conflicts with a package in the virtual environment, the local package takes precedence. Use `pip uninstall` to remove the conflicting package if necessary.

---

By following this guide, you can streamline your Python workflow while managing storage and dependencies effectively. Happy coding!

