# Working-with-functions-arrays-in-shell-scripting
Repo on functions and arrays in shell scripting
🐚 Shell Scripting with Functions & AWS CLI - Complete Tutorial 📋
Introduction Welcome! This comprehensive tutorial will guide you through
shell scripting functions and AWS CLI integration. Let's dive in! 🚀

## Step 1: 📝 Basic Function Syntax

``` bash
#!/bin/bash
# Syntax for function
function_name() {
    # Function body
    # Commands or logic
}
```

### 🎯 What We're Learning:

-   🔤 **Function Declaration:** Basic structure of shell functions
-   🏗️ **Code Organization:** How to encapsulate logic
-   📂 **Scope:** Understanding function boundaries

💡 **Key Points:** - Functions help organize code into reusable blocks -
Use descriptive names for better readability - Always include comments
for complex logic

------------------------------------------------------------------------

## Step 2: ⚠️ Script Without Functions (Before)

``` bash
# Checking the number of arguments
if [ "$#" -eq 0 ]; then  
    echo "Usage: $0 <environment>"  
    exit 1  
fi

# Accessing the first argument  
ENVIRONMENT=$1  

# Acting based on the argument value  
if [ "$ENVIRONMENT" == "local" ]; then  
    echo "Running script for local Environment..."  
elif [ "$ENVIRONMENT" == "testing" ]; then  
    echo "Running script for Testing Environment..."  
elif [ "$ENVIRONMENT" == "production" ]; then  
    echo "Running script for Production Environment..."  
else  
    echo "Invalid environment specified. Please use 'local', 'testing', or 'production'."  
    exit 2  
fi
```

### 🎯 What We're Learning:

-   🔍 **Argument Checking:** Validating input parameters\
-   🎚️ **Conditional Logic:** Using if-elif-else statements\
-   🚦 **Exit Codes:** Proper error handling with exit codes

⚠️ **Issues with This Approach:** - ❌ Code is not reusable\
- ❌ Hard to maintain\
- ❌ No separation of concerns

------------------------------------------------------------------------

## Step 3: 🔧 Script With Functions

``` bash
#!/bin/bash

# Function to check the number of arguments
check_num_of_args() {
    if [ "$#" -eq 0 ]; then
        echo "Usage: $0 <environment>"
        exit 1
    fi
}

# Function to run based on environment
run_environment() {
    ENVIRONMENT=$1

    if [ "$ENVIRONMENT" = "local" ]; then
        echo "Running script for Local Environment..." 
    elif [ "$ENVIRONMENT" = "testing" ]; then
        echo "Running script for Testing Environment..." 
    elif [ "$ENVIRONMENT" = "production" ]; then
        echo "Running script for Production Environment..." 
    else
        echo "Invalid environment specified. Please use 'local', 'testing', or 'production'." 
        exit 2
    fi
}
```

### 🎯 What We're Learning:

-   🎪 **Function Creation:** Breaking down logic into functions\
-   🔄 **Parameter Passing:** How functions receive arguments\
-   🏗️ **Modular Design:** Creating maintainable code structure

✅ **Benefits:** - ✔️ Reusable code components\
- ✔️ Easier testing and debugging\
- ✔️ Better organization

------------------------------------------------------------------------

## Step 4: 📞 Calling Functions in Action

``` bash
#!/bin/bash

# Checking the number of arguments
if [ "$#" -eq 0 ]; then
    echo "Usage: $0 <environment>"
    exit 1
fi

# Accessing the first argument
ENVIRONMENT=$1

# Acting based on the argument value
if [ "$ENVIRONMENT" == "local" ]; then
    echo "Running script for local Environment..." 
elif [ "$ENVIRONMENT" == "testing" ]; then
    echo "Running script for Testing Environment..." 
elif [ "$ENVIRONMENT" == "production" ]; then
    echo "Running script for Production Environment..." 
else
    echo "Invalid environment specified. Please use 'local', 'testing', or 'production'."
    exit 2
fi
```

### 🎯 Execution Examples:

``` bash
# 🚫 No arguments provided
[stiv@devops shell_scripting]$ sh functions.sh
Usage: functions.sh <environment>

# ✅ With valid argument
[stiv@devops shell_scripting]$ sh functions.sh local
Running script for local Environment...
```

### 🎯 What We're Learning:

-   🖥️ **Script Execution:** How to run shell scripts\
-   📥 **Argument Passing:** Providing input to scripts\
-   🔍 **Error Handling:** Seeing validation in action

------------------------------------------------------------------------

## Step 5: 🔍 AWS CLI Dependency Check

``` bash
# Function to check if AWS CLI is installed
check_aws_cli() {
    if ! command -v aws &> /dev/null; then
        echo "AWS CLI is not installed. Please install it before proceeding."
        return 1
    fi
}

# --- Main script starts here ---

# Call the function
if ! check_aws_cli; then
    # If the function returned 1 (failed), stop the script
    exit 1
fi

echo "AWS CLI is installed. Continuing with the script..." 
```

### 🎯 Execution Result:

``` bash
[stiv@devops shell_scripting]$ sh aws_cli.sh
AWS CLI is not installed. Please install it before proceeding.
```

### 🎯 What We're Learning:

-   🔧 **Dependency Checking:** Ensuring required tools are available\
-   🔄 **Return Values:** Using return codes for function status\
-   🛑 **Graceful Failure:** Stopping execution when requirements aren't
    met

💡 **Pro Tip:**\
Use `command -v` instead of `which` for better portability across
different shells.

------------------------------------------------------------------------

## Step 6: 🌍 AWS Environment Variables

``` bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_DEFAULT_REGION="us-east-1"
export AWS_PROFILE="default"
```

### 🎯 What We're Learning:

-   🔑 **Authentication:** Setting up AWS credentials\
-   🌐 **Region Configuration:** Specifying AWS regions\
-   👤 **Profile Management:** Working with multiple AWS accounts

⚠️ **Security Note:**\
Never commit actual credentials to version control! Use environment
variables or AWS profiles.

------------------------------------------------------------------------

## Step 7: 👥 AWS Profile Configuration

``` bash
[default]
aws_access_key_id = AKIAxxxxxxxx
aws_secret_access_key = abcdxxxxxxx

[dev-account]
aws_access_key_id = DEVKEYxxxxxxx
aws_secret_access_key = DEVSECRETxxxxxxx

[default]
region = us-east-1
output = json

[profile dev-account]
region = eu-west-1
output = text
```

### 🎯 What We're Learning:

-   🗂️ **Profile Setup:** Configuring multiple AWS profiles\
-   🎛️ **Output Formatting:** Setting default output formats (JSON,
    text, table)\
-   🌍 **Regional Settings:** Different regions for different profiles

📍 **File Location:**\
`~/.aws/credentials` and `~/.aws/config`

------------------------------------------------------------------------

## Step 8: 🎯 Complete Integrated Script

``` bash
# Function to check number of arguments
check_num_of_args() {
    if [ "$#" -eq 0 ]; then
        echo "Usage: $0 <environment>"
        exit 1
    fi
}

# Function to activate infra environment
activate_infra_environment() {
    ENVIRONMENT=$1
    if [ "$ENVIRONMENT" == "local" ]; then
        echo "Running script for Local Environment..." 
    elif [ "$ENVIRONMENT" == "testing" ]; then
        echo "Running script for Testing Environment..." 
    elif [ "$ENVIRONMENT" == "production" ]; then
        echo "Running script for Production Environment..." 
    else
        echo "Invalid environment specified. Please use 'local', 'testing', or 'production'."
        exit 2
    fi
}

# Function to check if AWS CLI is installed
check_aws_cli() {
    if ! command -v aws &> /dev/null; then
        echo "AWS CLI is not installed. Please install it before proceeding."
        return 1
    fi
}

# Function to check if AWS profile is set (fallback to default)
check_aws_profile() {
    if [ -z "$AWS_PROFILE" ]; then
        echo "AWS_PROFILE not set. Falling back to default profile."
        export AWS_PROFILE=default
    fi
}

# --- Run checks ---
check_num_of_args "$@"
activate_infra_environment "$1"
check_aws_cli
check_aws_profile
```

### 🎯 What We're Learning:

-   🔗 **Function Integration:** Combining multiple functions\
-   🚀 **Script Flow:** Proper execution sequence\
-   🛡️ **Robustness:** Comprehensive error checking\
-   🔄 **Dependency Management:** Ensuring all requirements are met

------------------------------------------------------------------------

## 🏁 Conclusion

### ✅ What We've Accomplished:

-   📚 **Function Fundamentals:** Learned shell function syntax and
    structure\
-   🔄 **Code Organization:** Transformed monolithic scripts into
    modular functions\
-   🔒 **Error Handling:** Implemented proper validation and error
    checking\
-   ☁️ **AWS Integration:** Added AWS CLI dependency checks and profile
    management

### 🎯 Key Takeaways:

-   🏗️ **Modular Design:** Break code into small, focused functions\
-   🔒 **Validation First:** Always validate inputs and dependencies\
-   📝 **Clear Naming:** Use descriptive function and variable names\
-   🛡️ **Error Handling:** Plan for failure scenarios\
-   🔧 **Reusability:** Write functions that can be reused across
    scripts

### 🚀 Next Steps:

-   Practice creating more complex functions\
-   Explore advanced AWS CLI commands\
-   Learn about shell script testing frameworks\
-   Study best practices for secure credential management

💡 **Final Pro Tip:**\
Always test your scripts in a safe environment before deploying to
production! 🧪

**Happy Scripting! 🎉🐚**
