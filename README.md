# Fishy Phiisshing

![Placeholder Image for Project](https://i.imgur.com/linkToPlaceholderImage.png)

## Objective

The "Fishy Phiisshing" project is an ambitious endeavor aimed at unraveling the complexities of real-world phishing attacks. Our journey begins with a rich source of data: a GitHub repository filled with numerous samples of actual phishing emails. Leveraging this repository, our objective is twofold:

1. **Automate Collection**: We will develop a Python script to interact with the GitHub repository's API, automating the process of downloading these phishing email samples for analysis. This not only enhances efficiency but also ensures we have a diverse dataset for a comprehensive study.

2. **In-Depth Analysis**: With a suite of sophisticated tools within a Kali Linux VM, our goal is to dissect these emails meticulously. We'll explore various tactics and characteristics of phishing attempts, using tools like Thunderbird for email analysis, Talos Intelligence and VirusTotal for threat intelligence and link examination, and PhishTool for detailed phishing email investigations.

Our final product will be a detailed phishing report, akin to what a SOC analyst would compile, summarizing our analysis, insights, and recommendations. The aim is to gain a deeper understanding of phishing threats and to create educational content to enhance cybersecurity awareness.

## Components

- **VirtualBox**: For creating and managing a secure virtual environment.
- **Kali Linux VM**: A specialized Linux distribution for cybersecurity tasks.
- **GitHub**: Source for phishing email samples, accessed through Python scripting.
- **Python**: Scripting language for automating the fetching of email samples.
- **Thunderbird**: Email client to safely view and analyze phishing emails.
- **Talos Intelligence**: For additional threat intelligence and contextual analysis.
- **VirusTotal**: To analyze suspicious links and attachments for threats.
- **PhishTool**: Specialized tool for detailed phishing email analysis.


<details>
  <summary><h2><b>Section 1: Setting Up the Virtual Environment</b></h2></summary>
  This section outlines the initial setup of our Kali Linux virtual machine for the phishing analysis project. We'll begin by updating the system, followed by installing Thunderbird, and ensuring our Python environment is properly configured.

  - **Step 1: Update and Upgrade Kali Linux**:  
    Our first step is to update the Kali Linux system to ensure we have the latest security patches and functionalities.
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```
    ![Placeholder Image 1 for Update](https://i.imgur.com/linkToUpdateImage1.png)
    
  - **Step 2: Install Thunderbird**:  
    Then, we proceed to install Thunderbird, our chosen application for securely managing and viewing phishing emails.
    ```bash
    sudo apt install thunderbird -y
    ```
    ![Placeholder Image 1 for Thunderbird](https://i.imgur.com/linkToThunderbirdImage1.png)

  - **Step 3: Set Up Python Environment**:  
    Finally, we'll verify that Python is installed and ready, and then set up pip, Python's package manager. We'll also install the 'requests' library, which is crucial for our scripting tasks.
    - Confirm Python installation:
      ```bash
      python3 --version
      ```
    - Install Python if necessary:
      ```bash
      sudo apt install python3 -y
      ```
    - Check pip installation and install 'requests':
      ```bash
      pip3 --version
      pip3 install requests
      ```
    ![Placeholder Image 1 for Python Setup](https://i.imgur.com/linkToPythonSetupImage1.png)

  With these steps completed, our Kali Linux VM is fully prepared with the latest updates, Thunderbird is ready for email analysis, and our Python environment is equipped for scripting. This forms a robust foundation for our phishing email analysis endeavor.

</details>


<details>
  <summary><h2><b>Section 2: Script Development and Data Collection</b></h2></summary>
  In this section, we'll dive into the development of our Python script. This script will interact with the GitHub API to automate the downloading of phishing email samples.

  - **Python Script Creation**:  
    We'll code a script in Python that efficiently downloads email samples from the designated GitHub repository.
    - **API Interaction**: Script will use GitHub API for fetching emails.
    - **Data Organization**: Downloads will be organized for easy access and analysis.

    <details>
    <summary>download_emails.py <b>(CLICK HERE TO VIEW)</b></summary>
  
    ```python
    import requests  # Importing the requests library to handle HTTP requests
    import os  # Importing the os library for interacting with the operating system

    # Setting variables for GitHub repository details
    github_username = 'rf-peixoto'  # GitHub username
    repository_name = 'phishing_pot'  # Repository name
    branch_name = 'main'  # Branch name

    # Setting the folder in the GitHub repo and the local directory to save files
    github_folder = 'email'  # Folder name in the GitHub repository
    local_folder = '/home/thuynh808/Desktop/Phishing/samples/'  # Local folder path for saving files

    # Constructing the URL to access the contents of the specified folder in the GitHub repository
    url = f'https://api.github.com/repos/{github_username}/{repository_name}/contents/{github_folder}?ref={branch_name}'

    # Making an HTTP GET request to the GitHub API
    response = requests.get(url)
    # Checking if the request was successful
    if response.status_code == 200:
        files = response.json()  # Parsing the response to JSON to get a list of files
        # Iterating over each file in the folder
        for file in files:
            # Checking if the file is an email file (.eml)
            if file['name'].endswith('.eml'):
                # Making a GET request to download the file
                download_response = requests.get(file['download_url'])
                # Checking if the download was successful
                if download_response.status_code == 200:
                    # Opening/creating a file in write-binary mode in the specified local directory
                    with open(os.path.join(local_folder, file['name']), 'wb') as f:
                        f.write(download_response.content)  # Writing the content of the download to the file
                    print(f'Downloaded: {file["name"]}')  # Printing a confirmation message
                else:
                    print(f'Failed to download: {file["name"]}')  # Printing an error message if download fails
    else:
        print(f'Failed to access GitHub folder: {github_folder}')  # Printing an error message if GitHub folder access fails
    ```
    </details>

  ![Placeholder Image for Script Development](https://i.imgur.com/linkToScriptDevImage.png)
  
</details>

<details>
  <summary><h2><b>Section 3: Analyzing Phishing Emails</b></h2></summary>
  Here, we focus on the detailed analysis of the phishing emails using our chosen tools.

  - **Email Examination with Thunderbird**:  
    We'll utilize Thunderbird to inspect the contents and structure of each email.
  - **Threat Assessment**:  
    Using Talos Intelligence and VirusTotal, we'll evaluate any links or attachments for threats.
  - **Using PhishTool**:  
    This tool will help us in deeper analysis, including header examination and pattern identification.

  ![Placeholder Image for Email Analysis](https://i.imgur.com/linkToEmailAnalysisImage.png)
</details>

<details>
  <summary><h2><b>Section 4: Compiling the Phishing Report</b></h2></summary>
  Our final task is to compile a comprehensive phishing report that encapsulates our findings and insights.

  - **Report Structure**:  
    Outline of the report, including types of attacks, common traits, and notable patterns.
  - **Key Findings**:  
    Summarization of the most significant insights from our analysis.
  - **Recommendations**:  
    Practical advice and strategies based on our findings.

  ![Placeholder Image for Report Compilation](https://i.imgur.com/linkToReportCompilationImage.png)
</details>

<details>
  <summary><h2><b>Section 5: Reflection and SOC Analyst Insights</b></h2></summary>
  In this concluding section, we reflect on the entire project and its implications in the real world of cybersecurity.

  - **Project Reflection**:  
    Discuss the skills and knowledge gained throughout the project.
  - **SOC Analyst Role Simulation**:  
    How this project simulates the role of a SOC analyst and its relevance to actual cybersecurity scenarios.

  ![Placeholder Image for Reflection](https://i.imgur.com/linkToReflectionImage.png)
</details>
