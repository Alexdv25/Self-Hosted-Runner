# 🔰 Part 1 — Build Your First Self Hosted Runner on AWS

---

# 🎯 Mission

Create a fully working GitHub Actions Self Hosted Runner on AWS EC2 and use it to execute a Node.js CI pipeline.

---

# 🔹 Stage 0 — Create an AWS EC2 Instance

## Requirements

Create an EC2 instance that will act as a GitHub Actions Runner.

---

## Instance Requirements

### OS

Use:

```text
Ubuntu Server 24.04 LTS
```

---

### Instance Type

Use:

```text
t3.small
```

---

### Storage

Minimum:

```text
20GB
```

---

## Security Group Requirements

Allow:

| Type | Port |
| ---- | ---- |
| SSH  | 22   |

---

# 🔹 Stage 1 — Connect to the Machine

## Instructions

SSH into the EC2 instance.

---

## Validation

Run:

```bash
whoami
hostname
pwd
```

---

# 🔹 Stage 2 — Prepare the Runner Machine

## Requirements

Install:

```bash
git
curl
tar
unzip
```

---

## Validation

Verify:

```bash
git --version
curl --version
```

---

# 🔹 Stage 3 — Create a GitHub Repository

## Instructions

1. Open GitHub.

2. Click the `+` icon in the top-right corner.

3. Select:

   ```text
   New repository
   ```

4. Repository name:

   ```text
   aws-self-hosted-runner
   ```

5. Set visibility to:

   ```text
   Private
   ```

6. Enable:

   ```text
   Add a README file
   ```

7. Click:

   ```text
   Create repository
   ```

---

# 🔹 Stage 4 — Configure the Self Hosted Runner

## Instructions

Inside the repository:

```text
Settings → Actions → Runners
```

Click:

```text
New self-hosted runner
```

---

## Requirements

Choose:

```text
Linux
x64
```

GitHub will generate setup commands.

Run the commands on the EC2 instance.

---

# 🔹 Stage 5 — Start the Runner

## Instructions

Start the runner manually.

---

## Validation

Verify GitHub shows:

```text
Idle
```

---

# 🔹 Stage 6 — Create the First Workflow

## Requirements

Create:

```text
.github/workflows/main.yml
```

---

## Workflow Requirements

### Trigger

Run on every push to:

```text
main
```

---

## Job Requirements

Create one job named:

```yaml
runner-test
```

Run it on:

```yaml
runs-on: self-hosted
```

---

## Steps

### Step 1 — Print Machine Information

Print:

* hostname
* current user
* machine uptime

---

### Step 2 — Print Custom Message

```text
Hello from AWS self-hosted runner!
```

---

# 🔹 Stage 7 — Commit and Run the Workflow

## Instructions

1. Commit the workflow.

2. Push the changes to:

   ```text
   main
   ```

3. Open the:

   ```text
   Actions
   ```

   tab.

4. Open the workflow execution logs.

---

## Validation

Verify the workflow:

* runs successfully
* executes on the self-hosted runner
* prints the EC2 machine information

---

# 🔹 Stage 8 — Prove Runner Persistence

## Instructions

Inside the workflow:

Create a file:

```bash
touch proof.txt
```

---

## Validation

SSH back into the EC2 instance and verify:

```bash
ls
```

shows:

```text
proof.txt
```

---

# 🔹 Stage 9 — Install Node.js

## Requirements

Install:

```text
Node.js 20
```

on the EC2 instance.

---

## Validation

Add workflow steps that print:

```bash
node --version
npm --version
```

---

# 🔹 Stage 10 — Run the Node.js CI Pipeline

## Requirements

The repository contains:

* package.json
* tests
* build script

---

## Workflow Requirements

Add steps for:

### Install dependencies

```bash
npm ci
```

---

### Run tests

```bash
npm test
```

---

### Run build

```bash
npm run build
```

---

# 🔹 Stage 11 — Configure the Runner as a Linux Service

## Instructions

Configure the runner to:

* start automatically after reboot
* continue running after SSH disconnects

---

## Validation

1. Reboot the EC2 instance.
2. Verify the runner reconnects automatically.
3. Trigger a new workflow execution.
4. Verify the pipeline still works.
