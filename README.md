# Loan-duration
import tkinter as tk
import tkinter.messagebox as messagebox
import chardet
import math 
import csv

class Application:
    def __init__(self, root):
        self.root = root
        self.csv_filename = tk.StringVar() 
        tk.Label(self.root, text="Put the csv file in the same place as the python script and enter its name here with the extention.").pack()
        tk.Entry(self.root, textvariable=self.csv_filename).pack()
        tk.Button(self.root, text="Submit", command=self.submit).pack()

    def submit(self):
        self.csv_filename = self.csv_filename.get()
        self.root.destroy()
        messagebox.showinfo("CSV File Created", "The result CSV file was created in the same location as the Python file.")

root = tk.Tk()
csv_prompt = Application(root)
root.mainloop()



with open(csv_prompt.csv_filename, 'rb') as csv_file:
  encoding = chardet.detect(csv_file.read())['encoding']


class Dataset():
  def __init__(self, name, amount_borrowed, rate, monthly):
    self.name = name
    self.amount_borrowed = amount_borrowed
    self.rate = rate
    self.monthly = monthly

with open(csv_prompt.csv_filename, encoding=encoding) as csv_file:
  reader = csv.reader(csv_file,delimiter=';')
  next(reader)
  data_list = []
  for row in reader:
    data = Dataset(row[0], row[1], row[2], row[3])
    data_list.append(data)
 
  
class Calculation : 
    def __init__(self, data_list):
      self.data_list = data_list
      
    
    def calculate_duration(self, amount, rate, payment):
        monthly_rate = rate / 12
        duration = math.log(payment / (payment - monthly_rate * amount)) / math.log(1 + monthly_rate)
        return duration / 12
    def is_eligible_for_loan(self, duration):
        if duration > 30:
            return False
        return True
    
    def calculate_all_durations(self):
        results = []
        for data in self.data_list:
            amount = float(data.amount_borrowed.replace(' ', '').replace(',','.'))
            payment = float(data.monthly.replace('-','').replace(' ', '').replace('€','').replace(',','.'))
            rate = float(data.rate.replace(' ', '').replace('%','').replace(',','.')) / 100
            duration = self.calculate_duration(amount, rate, payment)
            eligibility = self.is_eligible_for_loan(duration)
            results.append((data.name, duration, eligibility))
        return results


class Save:
    def __init__(self, calculation):
        self.calculation = calculation
        
    def write_csv(self, filename):
        with open(filename, 'w', newline='') as csvfile:
            writer = csv.writer(csvfile)
            writer.writerow(['Loan', 'Duration in years', 'Eligibility'])
            for result in self.calculation.calculate_all_durations():
                loan_name, duration, eligibility = result
                duration = int(round(duration))
                writer.writerow([loan_name, duration, eligibility])
                

calcul = Calculation(data_list)
csv_writer = Save(calcul)
csv_writer.write_csv('loan_results.csv')
