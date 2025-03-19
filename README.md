# PYTHON PROJECT
# STUDENT COMPASS

* AIM: Making life of ever-caring staff esier.

# CODE USED:
1. FOR NORMAL OPERATION:
```import pandas as pd
import os
import sys  



file_path = r"C:\Users\LENOVO\Documents\SEC 404\Project\student_2a.csv"


'''if not os.path.exists(file_path):
    print(f" Error: File '{file_path}' not found! Check the path and try again.")
    sys.exit() ''' 


df = pd.read_csv(file_path, dtype=str)  
print("HEY, CSV file loaded successfully!\n")


def search_student(query):
    query = query.strip().lower()
    result = df[df.apply(lambda row: query in row.astype(str).str.lower().values, axis=1)]
    return result if not result.empty else None


while True:
    query_input = input("SAIRAM BANGARU, Enter a student detail (Name, Reg No, Email, etc.) or type 'leave' to quit: ").strip()
    
    if query_input.lower() == 'leave':
        print("Exiting... Have a great day sairam to you all ! ")
        break

    result = search_student(query_input)

    if result is not None:
        print("\n WOW !Matching Student(s) Found:\n", result.to_string(index=False))
    else:
        print("OOPS! No match found. Try again.")
   ```
2.FOR DOING THE SAME USING GUI:
```
import sys
import pandas as pd
from PyQt5.QtWidgets import QApplication, QWidget, QVBoxLayout, QLineEdit, QPushButton, QTableWidget, QTableWidgetItem, QLabel

file_path = r"C:\Users\LENOVO\Documents\SEC 404\Project\student_2a.csv"

try:
    df = pd.read_csv(file_path, dtype=str)
except FileNotFoundError:
    print(f"Error: CSV file not found at {file_path}. Check the path and try again.")
    sys.exit()

class StudentSearchApp(QWidget):
    def __init__(self):
        super().__init__()

        self.initUI()

    def initUI(self):
        self.setWindowTitle("Student Search")
        self.setGeometry(100, 100, 1100, 500)

        layout = QVBoxLayout()

        self.label = QLabel("Enter student detail (Name, Reg No, Email, Hobby, etc.):")
        layout.addWidget(self.label)

        self.input_field = QLineEdit(self)
        layout.addWidget(self.input_field)

        self.search_button = QPushButton("Search", self)
        self.search_button.clicked.connect(self.search_student)
        layout.addWidget(self.search_button)

        self.table = QTableWidget(self)
        layout.addWidget(self.table)

        self.setLayout(layout)

    def search_student(self):
        query = self.input_field.text().strip().lower()
        result = df[df.apply(lambda row: any(query in str(value).lower() for value in row.values), axis=1)]

        if not result.empty:
            self.display_results(result)
        else:
            self.table.setRowCount(0)
            self.table.setColumnCount(0)
            self.label.setText("No match found. Try again.")

    def display_results(self, result):
        self.table.setRowCount(len(result))
        self.table.setColumnCount(len(result.columns))
        self.table.setHorizontalHeaderLabels(result.columns)

        for row_idx, (_, row) in enumerate(result.iterrows()):
            for col_idx, value in enumerate(row):
                self.table.setItem(row_idx, col_idx, QTableWidgetItem(str(value)))  # Convert values to string properly

        self.label.setText(f"Found {len(result)} matching student(s).")  # Show result count

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = StudentSearchApp()
    window.show()
    sys.exit(app.exec_())
```
# OUTPUT:
AS AN OUTPUT ONE CAN SEE THE DETAILS OF THE STUDENT BY GIVING JUST ONE ATTRIBUTE OF THE PARTICULAR STUDENT.

