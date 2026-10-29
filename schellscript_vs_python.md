
# Shell Scripting vs Python in DevOps

## Introduction

In DevOps, Shell Scripting and Python are used to automate tasks, reduce manual work, and improve efficiency.

Both are useful, but the choice depends on the task you want to automate.

- **Shell Scripting (Bash):** Best for running Linux commands and automating system administration tasks.
- **Python:** Best for complex automation, API integration, data processing, and building reusable scripts.

## 1. What Is Shell Scripting?

Shell scripting means writing a series of commands in a file and executing them automatically using a shell such as Bash.

Instead of running commands one by one, we can write them in a script and execute them together.

### Example

```bash
#!/bin/bash

echo "Checking disk usage..."

df -h

echo "Disk check completed!"
```

### Explanation

- `#!/bin/bash` specifies the Bash interpreter.
- `echo` displays a message.
- `df -h` displays disk usage in a human-readable format.

### When to Use Shell Scripting

1. **System Administration:** Manage files, directories, users, permissions, and processes.
2. **Linux Commands:** Automate commands such as `cp`, `mv`, `grep`, `find`, and `systemctl`.
3. **Application Deployment:** Pull code, install dependencies, and restart services.
4. **Text Processing:** Search logs and extract information using tools such as `grep`, `awk`, and `sed`.
5. **Quick Automation:** Automate simple, repetitive tasks on Linux servers.

### Common DevOps Use Cases

- Checking disk space on an EC2 instance.
- Starting and stopping Linux services.
- Creating backups of important files.
- Deploying applications on servers.
- Automating Docker commands.

## 2. What Is Python?

Python is a general-purpose programming language used to develop applications and automate complex tasks.

It provides built-in features and external libraries that make it easier to work with files, APIs, databases, cloud services, and structured data.

### Example

```python
import shutil

print("Checking disk usage...")

usage = shutil.disk_usage("/")

percentage = (usage.used / usage.total) * 100

print(f"Disk usage: {percentage:.2f}%")

if percentage >= 80:
    print("WARNING: Disk usage is high!")
else:
    print("Disk usage is normal.")
```

### Explanation

- `import shutil` imports a Python module for file and disk operations.
- `shutil.disk_usage("/")` retrieves disk usage information for the root filesystem.
- The percentage calculation determines how much space is used.
- The `if` statement checks whether usage has reached the 80% threshold.

### When to Use Python

1. **Complex Automation:** Automate tasks involving multiple conditions and operations.
2. **API Integration:** Communicate with AWS services and other applications through APIs.
3. **Data Processing:** Read, filter, transform, and analyze JSON, CSV, and log files.
4. **Reusable Code:** Create functions and modules that can be reused across projects.
5. **Error Handling:** Handle failures and exceptions in a structured way.
6. **Monitoring:** Collect system metrics and generate reports or alerts.

### Common DevOps Use Cases

- Listing EC2 instances using Boto3.
- Generating AWS resource inventory reports.
- Monitoring CPU, memory, and disk usage.
- Checking application health through HTTP APIs.
- Automating CI/CD pipeline checks.
- Processing application and server logs.

## 3. Difference Between Shell Scripting and Python

| Feature | Shell Scripting | Python |
|---|---|---|
| Main purpose | Automating shell commands | General-purpose automation |
| Syntax | Linux commands and shell syntax | Python programming syntax |
| Learning | Easier for basic command automation | Requires learning programming concepts |
| Linux administration | Excellent | Also useful |
| File operations | Excellent for command-line tasks | Excellent for structured and complex operations |
| API integration | Possible, but often less convenient | Supported by many libraries |
| AWS automation | Commonly uses AWS CLI | Can use Boto3 and AWS CLI |
| Error handling | Basic to moderate | Structured exception handling |
| Large projects | Can become difficult to maintain | Easier to organize into modules |
| File extension | `.sh` | `.py` |

## 4. Same Task Using Shell Scripting and Python

Consider a task where we need to check disk usage and display a warning if it reaches 80%.

### Shell Script: `disk_check.sh`

```bash
#!/bin/bash

THRESHOLD=80

USAGE=$(df -P / | awk 'NR==2 {gsub(/%/, "", $5); print $5}')

echo "Disk usage: ${USAGE}%"

if [ "$USAGE" -ge "$THRESHOLD" ]; then
    echo "WARNING: Disk usage is high!"
else
    echo "Disk usage is normal."
fi
```

Run it using:

```bash
chmod +x disk_check.sh
./disk_check.sh
```

### Python Script: `disk_check.py`

```python
import shutil

THRESHOLD = 80

usage = shutil.disk_usage("/")
percentage = (usage.used / usage.total) * 100

print(f"Disk usage: {percentage:.2f}%")

if percentage >= THRESHOLD:
    print("WARNING: Disk usage is high!")
else:
    print("Disk usage is normal.")
```

Run it using:

```bash
python3 disk_check.py
```

**Key takeaway:** Both scripts perform the same basic task, but they use different approaches. Bash executes Linux commands, while Python uses a programming library to retrieve and process disk information.

## 5. Shell Scripting and Python in a CI/CD Pipeline

Both languages can work together in tools such as Jenkins and GitHub Actions.

### Example Workflow

1. A developer pushes code to GitHub.
2. GitHub Actions or Jenkins starts the pipeline.
3. A Bash script installs dependencies and runs build commands.
4. Python scripts validate configurations, call APIs, or generate reports.
5. Automated tests run.
6. The application is deployed.
7. Monitoring scripts check application health.

### Architecture

```text
Developer
    |
    v
GitHub Repository
    |
    v
Jenkins / GitHub Actions
    |
    +----> Bash Scripts
    |         |
    |         +--> Build and deployment commands
    |
    +----> Python Scripts
              |
              +--> API checks and automation
    |
    v
Application Deployment
    |
    v
Monitoring and Reporting
```

## 6. Which One Should a DevOps Engineer Learn First?

A beginner should learn both languages in the following order:

1. **Linux Commands:** Learn `ls`, `cd`, `grep`, `find`, `chmod`, `chown`, and `systemctl`.
2. **Shell Scripting:** Learn variables, conditions, loops, functions, and exit codes.
3. **Python Basics:** Learn variables, data types, lists, dictionaries, loops, and functions.
4. **Python Automation:** Learn file handling, JSON, exception handling, and subprocess execution.
5. **AWS Automation:** Learn Boto3 to interact with AWS services.
6. **CI/CD Integration:** Use Bash and Python scripts in Jenkins or GitHub Actions.

## Conclusion

Shell scripting and Python are both important skills in DevOps.

- Choose **Shell Scripting** when the task mainly involves Linux commands, files, services, or straightforward deployment operations.
- Choose **Python** when the task requires complex logic, API integration, structured data processing, or reusable automation.
- Use **both together** when building practical DevOps workflows.

### Recommendation

Learn Bash first for Linux automation, then learn Python to build more advanced automation for AWS, Docker, Terraform, monitoring, and CI/CD pipelines.
