# LimeSurvey LSS File Scraper
This Python script automates the process of logging into a LimeSurvey administration panel and downloading all survey structures as .lss files. It's designed to help you back up or migrate your survey designs efficiently.

Features
Automated login to LimeSurvey admin panel.
Sets the number of surveys displayed per page to 100 for bulk selection.
Selects all surveys on the page.
Initiates the export of all selected survey structures (.lss files).
Handles common modal pop-ups during the export process.
Downloads the .lss files to a specified local directory.

# Prerequisites
Before running this script, ensure you have the following installed on your system:

Python 3.11.10: The script is tested with this version.
Conda (Anaconda or Miniconda): Recommended for managing Python environments and dependencies.
Jupyter Lab: For running the .ipynb notebook file.
Google Chrome Browser: Selenium requires a Chrome browser installed on your system to automate it. The script uses selenium-manager to automatically handle the ChromeDriver setup, so you don't need to download it manually.

# Setup
Follow these steps to set up your environment and install the necessary packages:

Create a Conda Environment:
Open your terminal or command prompt and run:

conda create -n lss_download python=3.11.10 ipykernel

This creates a new Conda environment named lss_download with Python 3.11.10 and ipykernel (which allows Jupyter to recognize this environment).

Activate the Conda Environment:

conda activate lss_download

You'll see the environment name in your terminal prompt, indicating it's active (e.g., (lss_download)).

Install Required Python Packages:
With the environment activated, install selenium using pip:

pip install selenium

Install the Conda Environment as a Jupyter Kernel:
This step makes your new Conda environment available as a selectable kernel in Jupyter Lab.

python -m ipykernel install --user --name=lss_download --display-name "LimeSurvey LSS Downloader (Python 3.11.10)"

# Configuration
# Before running the script, you must update the placeholder values with your actual LimeSurvey credentials and domain.

Open the lssDownloader.ipynb file.

Locate the --- Configuration --- section and modify the following lines:

LIMEQUERY_DOMAIN = "https://XXX.limequery.com/admin/authentication/sa/login"    # <--- REPLACE THIS with the exact URL to your LimeSurvey login page.
LIMEQUERY_USERNAME = "XXX"  # <--- REPLACE THIS with your LimeSurvey administrator username.
LIMEQUERY_PASSWORD = "XXX"  # <--- REPLACE THIS with your LimeSurvey administrator password.

Security Note: For production environments or enhanced security, consider loading these credentials from environment variables or a secure configuration system instead of hardcoding them directly in the script.

# Usage
Once the environment is set up and the configuration is updated, you can run the script from Jupyter Lab:

Start Jupyter Lab:
From your terminal (you can be in your base environment or the lss_download environment), navigate to the directory containing your .ipynb file and run:

jupyter lab

This will open Jupyter Lab in your web browser.

Open the Notebook:
In Jupyter Lab, navigate to and open your lssDownloader.ipynb file.

Select the Correct Kernel:
In the Jupyter Lab interface, go to the "Kernel" menu at the top, then "Change Kernel," and select "LimeSurvey LSS Downloader (Python 3.11.10)". This ensures your notebook runs within the environment where you installed selenium.

Run the Cell:
Execute the cells in the notebook sequentially. The script will launch a Chrome browser (or run in headless mode if uncommented), navigate to the LimeSurvey login page, perform the actions, and initiate the download.

Downloaded Files
The script is configured to save the downloaded .lss files (which will be a single .zip archive containing all selected .lss files) into a directory named lss_downloads within the same directory where your Jupyter Notebook is located.

If the lss_downloads directory does not exist, the script will create it automatically.

Notes and Troubleshooting
Headless Mode: By default, the script will open a visible Chrome browser window. 

# Use it carefully and without abuse. Check the robots.txt file on the website in case you do not.

Page Load Times: The script uses WebDriverWait to wait for elements to appear. If your internet connection is slow or the LimeSurvey instance is under heavy load, you might need to increase the 30 second timeout in WebDriverWait(driver, 30).

Selector Changes: Web applications can change their HTML structure (CSS selectors, XPaths). If the script fails to find elements (e.g., "Page size dropdown not found"), it's possible that LimeSurvey's interface has been updated, and the selectors in the script might need to be adjusted.

Download Prompts: While the script attempts to configure Chrome to automatically download files, browser security settings or specific LimeSurvey configurations might still trigger a download prompt in some cases. You may need to manually confirm the download if this occurs.

Login Issues: If the script reports "Login failed: Invalid username or password," double-check your LIMEQUERY_USERNAME and LIMEQUERY_PASSWORD in the script.
