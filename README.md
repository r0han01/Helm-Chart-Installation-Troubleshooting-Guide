# ReactJS Project Setup Guide

This README documents the process of setting up a ReactJS project on a Linux system, the issues encountered during the setup, and how they were resolved.

## **1. Prerequisites**

Ensure the following are installed on your system:

- **Node.js** (recommended version: 16.x or higher)
- **npm** (comes with Node.js)
- **npx** (bundled with npm)

To verify installation, run the following commands in the terminal:

```bash
node -v
npm -v
```
- If `node` or `npm` is not installed, please follow the `Node.js installation guide` [ search on google ] for your operating system.

## **2. Project Setup**
- Creating a React App Using `npx`

We used npx to create a new React app. This command uses the latest version of create-react-app without needing a global installation of the package.

Run the following command to create the app:

```bash
npx create-react-app my-app --legacy-peer-deps
```
- The `--legacy-peer-deps` flag is used to bypass peer dependency conflicts and ensures that the app installs successfully even if some dependencies do not align perfectly.

## **3. Dependency Conflicts and Resolution**
#### Conflict 1: React Version Mismatch
During the setup, we encountered a dependency conflict between the React version and some other packages, notably @testing-library/react, which required a lower version of React.

Error Message:

```text
npm error Found: react@19.0.0
npm error Could not resolve dependency: peer react@"^18.0.0" from @testing-library/react@13.4.0
```
#### Solution:
- We resolved this issue by using the --legacy-peer-deps flag during the create-react-app setup. This flag tells npm to bypass the strict peer dependency checks and proceed with the installation, even if some versions don't match perfectly.

```bash
npx create-react-app my-app --legacy-peer-deps
```
- This allows React 19.x to be installed while still satisfying the requirements of other packages, although it might not be the ideal long-term solution.

#### Conflict 2: Missing web-vitals Package
- After starting the app, we encountered another error related to the missing web-vitals package. This is because create-react-app attempts to import the web-vitals library for performance tracking by default.

Error Message:

```text
ERROR in ./src/reportWebVitals.js 5:4-24
Module not found: Error: Can't resolve 'web-vitals'
```
#### Solution:
To fix this error, we manually installed the web-vitals package:

```bash
npm install web-vitals
```
Once the package was installed, we were able to run the app without encountering any errors:

```bash
npm start
```
#### Optional: Remove web-vitals (If Not Needed)
- If you don't need to track performance metrics, you can safely remove the web-vitals package and its associated code. Here's how:

- Delete the `src/reportWebVitals.js` file.

- Remove the import statement from src/index.js:

```javascript
// Remove or comment out this line
import reportWebVitals from './reportWebVitals';
Remove the call to reportWebVitals() in src/index.js:
```
```javascript
// Remove or comment out this line
reportWebVitals();
```
- Restart the App to ensure everything works without web-vitals:

```bash
npm start
```
## **4. Final Working Setup**
- After performing the above steps, the following setup worked correctly:

- React 19.x was installed despite dependency conflicts.
- All dependencies were installed successfully with the --legacy-peer-deps flag.
- The app compiled successfully without errors.
- The development server started and displayed the default React page in the browser.
## 5. Conclusion
- This README documents the complete process of setting up a React app, handling dependency conflicts, and resolving common setup issues. By using the `--legacy-peer-deps` flag, we were able to bypass dependency conflicts and successfully install the app. We also resolved the missing web-vitals package issue.

## 6. References
- React Documentation [ search this on google ]
- Create React App GitHub [ search this on google ]
- Node.js Installation Guide [ search this on google ]