# Playwright Test Automation Script

This script automates the process of testing a web frontend by reading test inputs from an Excel file, interacting with the web application via a browser (using Playwright), and writing the actual outputs and pass/fail statuses back to the Excel file.

## Prerequisites

Before running the script, you need to have Python installed along with a few dependencies. Open your terminal and run the following commands:

```powershell
pip install -U pip
pip install playwright openpyxl
playwright install
```

## Basic Usage

**Important:** You should navigate into the `test_automation` folder before running the script so it can automatically find the default Excel file.

```powershell
cd test_automation
```

To run the script specific parameters, such as pointing to the xlsx file and the deployed URL:

```powershell
python test_automation.py --excel "IT23701496.xlsx" --url "https://www.pixelssuite.com/chat-translator"
```

## Useful Command-Line Arguments

Here are the most common flags you might want to use:

- `--excel`: Path to your Excel file containing the test cases. (Default: looks for `Assignment 1 - Test cases.xlsx`).
- `--url`: The URL of the frontend application to test. (Default: `https://www.pixelssuite.com/chat-translator`).
- `--headless`: Run the browser in the background without opening a visible window (faster).
- `--keep-open`: Keep the browser window open after the tests finish (useful for debugging).
- `--save-every <N>`: Save the Excel file after every `N` rows processed, preventing data loss if the script is interrupted. (Example: `--save-every 1`).
- `--type-delay-ms <ms>`: Delay between keystrokes in milliseconds to simulate realistic typing (Example: `--type-delay-ms 80`).
- `--slow-mo-ms <ms>`: Slows down all Playwright operations by the specified amount of milliseconds.
- `--wait-ms <ms>`: The time to wait after clicking "Transliterate" before checking for the output. (Default: 5000).

## Excel File Formatting

The script is designed to automatically find the correct header row and columns by searching for common names:
- **Input Column:** Looks for `Input`, `Singlish`, `Test Input`, etc.
- **Expected Output:** Looks for `Expected_Output`, `Expected Sinhala`, `Sinhala`, etc.
- **Actual Output:** Looks for `Actual_Output`, `Actual`. If it doesn't exist, it will create one.
- **Status:** Looks for `Status`, `Result`, `Pass/Fail`. If it doesn't exist, it will create one.

If your columns have non-standard names, you can explicitly define them:
```powershell
python test_automation.py --input-col "My Source Data" --expected-col "My Target"
```

## Stopping the Script
If you are running the script and want to stop it early, press `CTRL + C` in your terminal. If you are using `--save-every 1`, all your progress up until you stopped will be safely saved in the Excel file!
