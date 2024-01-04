# Loan-duration
This Python project was created as part of my studies in financial engineering to automate the calculation of loan durations from a CSV file. The application utilizes the Tkinter graphical interface to streamline user interaction.

Usage Instructions:
The graphical interface prompts the user to place the CSV file in the same directory as the Python script and enter its name with the extension. 
The script uses the chardet library to automatically detect the encoding of the CSV file, then creates a Dataset class to store the file's data. 
The Calculation class performs the loan duration calculations based on the CSV file information. It also checks eligibility based on the duration. 
The results are saved in a new CSV file named 'loan_results.csv' with columns 'Loan', 'Duration in years', and 'Eligibility'.

