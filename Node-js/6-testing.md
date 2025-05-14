Here are answers and explanations for each **Testing and CI/CD** question relevant to Node.js development:

---

### **1. How do you test Node.js applications? Which libraries do you use (Jest, Mocha, Supertest)?**

**Testing in Node.js** is typically done using:

* **Jest** – All-in-one testing framework from Meta, includes mocking, assertions, code coverage.
* **Mocha** – Test runner; often paired with **Chai** (assertions) and **Sinon** (mocking/stubs).
* **Supertest** – Used for HTTP assertions, commonly in Express.js applications.
* **Testing Library** – For React or frontend portions (not Node.js core but often used together).

#### Example with Jest + Supertest:

```ts
import request from 'supertest';
import app from '../src/app';

describe('GET /api/users', () => {
  it('should return 200 and a list of users', async () => {
    const res = await request(app).get('/api/users');
    expect(res.status).toBe(200);
    expect(Array.isArray(res.body)).toBe(true);
  });
});
```

---

### **2. What is the difference between unit, integration, and end-to-end testing in Node.js?**

| Type            | Description                                         | Example                          |
| --------------- | --------------------------------------------------- | -------------------------------- |
| **Unit Test**   | Tests a **single function/component** in isolation. | Testing a pure function.         |
| **Integration** | Tests **multiple components** working together.     | API route + DB call.             |
| **End-to-End**  | Tests the **entire app flow** as the user would.    | Login page > dashboard > logout. |

> Use Jest for unit/integration, and Playwright or Cypress for E2E.

---

### **3. How do you mock database or API calls in tests?**

* **Mocking** prevents tests from calling actual services or databases.

#### Options:

* **Jest**:

  ```ts
  jest.mock('../db/users', () => ({
    getUsers: jest.fn().mockResolvedValue([{ id: 1, name: 'John' }])
  }));
  ```

* **Sinon** (with Mocha):

  ```ts
  sinon.stub(db, 'getUsers').returns([{ id: 1, name: 'John' }]);
  ```

* **nock**: for mocking HTTP requests:

  ```ts
  const nock = require('nock');
  nock('https://api.example.com')
    .get('/users')
    .reply(200, [{ id: 1, name: 'John' }]);
  ```

---

### **4. How do you set up CI/CD for a Node.js application (e.g., GitHub Actions, Jenkins, Docker)?**

#### Common CI/CD tools:

* **GitHub Actions** (popular and integrated with GitHub)
* **Jenkins**, **GitLab CI**, **CircleCI**, **Bitbucket Pipelines**
* **Docker** for packaging and deploying

#### GitHub Actions Example:

```yaml
# .github/workflows/node.yml
name: Node.js CI

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - run: npm install
      - run: npm run test
      - run: npm run build
```

#### Deployment:

* Push Docker image to registry (e.g., Docker Hub, ECR).
* Deploy to platform (e.g., Heroku, ECS, Kubernetes).

#### Dockerfile (basic Node.js app):

```Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "start"]
```

---

Let me know if you’d like:

* A **hands-on CI/CD pipeline example** using Docker + GitHub Actions.
* A **testing template** structure for a Node.js app.
* A mock interview on this topic.
