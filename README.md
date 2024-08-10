# Customer Support AI

**Code adapted from Bill Zhang**

---

## Getting Started

Follow these steps to set up the project:

### 1. Obtain an OpenAI API Key
First, you need to obtain an API key from [OpenAI](https://platform.openai.com/).

### 2. Install Dependencies

#### Option 1: Create a New Next.js App
```bash
npx create-next-app@latest my-nextjs-app
```

#### Option 2: Install Node.js (If you don't have it already)
```bash
brew install node
```

### 3. Install Required Packages

- **OpenAI:**
  ```bash
  pip install openai
  ```

- **Material-UI (MUI):**
  ```bash
  npm install @mui/material @emotion/react @emotion/styled
  ```

### 4. Add the API Key

Create a `.env.local` file in the root directory of your project and add the following:

```env
OPENAI_API_KEY=replace-this-with-your-api-key
```

### 5. Run the Development Server

You can start the server using one of the following commands:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Then, open [http://localhost:3000](http://localhost:3000) in your browser to view the application.

---

## Setting up Virtual Machine using EC2
Follow this tutorial: [Easily Deploy Full Stack Node.js](https://www.youtube.com/watch?v=nQdyiK7-VlQ)

[Code Snippets](https://www.sammeechward.com/deploying-full-stack-js-to-aws-ec2)

## To connect (with MacOS)
Locate your private key in your local directory. 
This is the key used to launch this EC2 instance.
Then move it to the root .ssh directory file.
```bash
mv california-mac-1.pem ~/.ssh
cd ~/.ssh
```

Run this command, if necessary, to ensure your key is not publicly viewable.
```bash
chmod 400 "california-mac-1.pem"
```

Connect to your instance using its Public DNS:
```bash
ssh -i "california-mac-1.pem" ubuntu@ec2-3-89-21-49.compute-1.amazonaws.com
```

You can find your private key name and address on you EC2 dashboard instance. On your EC2 dashboard > instances, select the instance then click connect. Then click the SSH Client tab.

#### On your Virtual Machine
Once you successfully connect, first thing you need to do is update
packages on your VM
```bash
sudo apt update
sudo apt upgrade
```

Install Node.js to run your javascript application
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

## Transfer your app source code from local to the VM
#### On your Localhost
This rsync command will only sync up files when something changes.
Make sure that you use your private key and address to use the code below.
```bash
rsync -avz --exclude 'node_modules' --exclude '.git' --exclude '.env' \
-e "ssh -i ~/.ssh/california-mac-1.pem" \
. ubuntu@ec2-3-89-21-49.compute-1.amazonaws.com:~/app
```

## To run your app
1. First install all your dependencies
```bash
 npm install
 ```

2. Compile using:
```bash
npm run build
npm run start
```

....STUCK HERE......