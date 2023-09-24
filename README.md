# AA-DR Portal

A simple portal that allows vendors to sign up to apply, view application progress and status, as well as providing a central location for documents.

### **Pre-requisites**

AA-DR Portal requires AWS-CLI in order to get credentials needed to make AWS service related calls.

1. [Install AWS-CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) for your respective OS (using Windows will require a configuration change)
2. (**For Windows Users**) Go to `docker-compose.yml` and change this line in the backend container configuration:

```
    volumes:
      - ./backend:/app
      - ~/.aws:/root/.aws <- change to %UserProfile%\.aws:/root/.aws
```

3. Once installed run `aws configure sso` on your terminal / PowerShell
4. Follow the prompts as shown here exactly (if you don't things will break)

```
SSO session name (Recommended): aa-dr-developer
SSO start URL [None]: https://castlepointanime.awsapps.com/start
SSO region [None]: us-east-1
SSO registration scopes [sso:account:access]: (just hit enter here)
You will be prompted on your web browser to allow access, just follow the steps
There are X roles available to you.
 > PowerUserAccess
Use the role name "PowerUserAccess"
CLI default client Region [us-east-2]: us-east-1
CLI default output format [json]: json
CLI profile name [PowerUserAccess-971141433805]: cpac-webmaster
```

5. Once finished, login with `aws sso login --profile cpac-webmaster`
6. Follow the prompts and **make sure to sign in with your CPAC Google Account**
7. **Important**: You will need to re-run step 4 and restart your local / docker instance if you get a credential expiration
8. Follow the next steps below for local / container setup.

### **Local Setup**

---

To begin simply pull this repository and its submodules using the following command:

`git clone --recurse-submodules https://github.com/cpacdev/portal.git`

...or if you setup SSH already:

`git clone --recurse-submodules git@github.com:cpacdev/portal.git`

### **Running Locally With Docker**

---

_This method will build both front-end and back-end at once with minimal local installation!_

1. Make sure to install Docker for your system first!

2. After doing so simply run `docker compose up -d --build`

3. To shutdown both the front-end and backend run `docker compose down`

**You will now see the frontend on `localhost:3000` and the backend on `localhost:3001`**

### **Running VSCode Devcontainers**

---

Requirements:

- VSCode
- Docker
- VSCode Dev Containers plugin

**Running the backend**

1. In vscode click `File` and then click `Open Folder...`
2. Open the `backend` folder
3. Click `Ctrl + Shift + P` and then select `Dev Containers: Rebuild and Reopen in Container`
4. See steps **Running the backend** in **Running Locally without Docker** below to see how to start the backend

**Running the frontend**

1. In vscode click `File` and then click `Open Folder...`
2. Open the `frontend` folder
3. Click `Ctrl + Shift + P` and then select `Dev Containers: Rebuild and Reopen in Container`
4. See steps **Running the frontend** in **Running Locally without Docker** below to see how to start the frontend

### **Running Locally without Docker**

---

Make sure to have the following installed before proceeding:

- Node.js
- Yarn package manager
- Python 3.10+

**Running the backend**

1. `cd backend`
2. `pip install -r requirements.txt`
3. `python app.py`

**Running the frontend**

1. `cd frontend`
2. `yarn`
3. `yarn run dev`

### **Pushing your changes**

---

`git push --recurse-submodules=on-demand`
