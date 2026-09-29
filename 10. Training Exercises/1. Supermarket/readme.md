#### C# Programming Exercises – Summary Table

| # | Exercise | Max Score | Key Concepts | Required C# Features | Input | Output |
|---|----------|-----------|--------------|----------------------|-------|--------|
| 1.1 | **Supermarket** | 1 | Product array, loop, sum, change calculation | `int[]`, `while`, `ReadLine`, `Write`, `WriteLine` | Product number (1–10), 0 to quit; payment amount | Product number & price per item; Total; Change |
| 1.2 | **My own split and join** | 1 | Custom string splitting/joining without built‑in methods | Custom `MySplit`, `MyJoin` functions; no `Split`/`Join` | A sentence | Comma‑joined string; each word on its own line |
| 1.3 | **Employee** | 1 | Class with `Id` and `Name`; list of objects | `class Employee`, `List<Employee>`, loop until "0" | Employee names (0 to quit) | `Id: X Name: Y` for each employee |
| 1.4 | **PayrollSystem** | 1 | Inheritance (`SalaryEmployee : Employee`), payroll calculation | `PayrollSystem` class, `CalculatePayroll`, `SalaryEmployee` subclass | Employee name + monthly salary (0 to quit) | Payroll block per employee: header, name, check amount |
| 1.5 | **SalaryEmployee to CSV‑file** | 1 | File I/O, CSV format, reuse `MyJoin`/`MySplit` | Menu loop, `StreamWriter`/`StreamReader`, custom join/split | Menu choices; employee names & salaries | Menu; confirmation messages; employee list; file read/write counts |
| 1.6 | **Extend PayrollSystem with HourlyEmployee and CommissionEmployee** | 1 | Multiple inheritance levels, polymorphic salary calculation | `HourlyEmployee : Employee`, `CommissionEmployee : SalaryEmployee`, `AskSalary`, `CalculateSalary` | Salary type (1–3, 0 to quit), name, rate/hours/commission | Payroll blocks with correct check amounts |
| 1.7 | **Complete Payroll with File handling** | 1 | Full system: multiple salary types, file I/O, duplicate prevention, original values saved | Menu, salary type menu, CSV read/write, polymorphism, `List<Employee>` | Menu choices; salary type; employee details | Menu; payroll blocks; file write/read confirmations; updated payroll after read |

---
#### 1.1 Supermarket
- **Data**: `int[] prices = {10,14,22,33,44,13,22,55,66,77}`
- **Logic**: Ask product number; if 0 → quit; if invalid → error message; else add price to total, print `Product: X Price: Y`.
- **Final**: Print `Total:`, ask `Payment:`, print `Change:`.

#### 1.2 My own split and join
- **MySplit(sentence, separator)** → returns `List<string>` of items.
- **MyJoin(list, separator)** → returns single string.
- **Output**: First line = joined with commas; then each item on separate line.

#### 1.3 Employee
- **Class**: `Employee { int Id; string Name; }`
- **Loop**: Ask name; if "0" stop; else create Employee with auto‑increment Id, add to list.
- **Print**: `Id: 1 Name: Jane Doe` etc.

#### 1.4 PayrollSystem
- **Classes**:
  - `Employee` (base)
  - `SalaryEmployee : Employee` with `MonthlySalary`, `CalculateSalary()`
  - `PayrollSystem` with `CalculatePayroll(List<Employee>)`
- **Input**: Name + salary; 0 name to quit.
- **Output**: For each employee:
  ```
  Employee Payroll
  ================
  Payroll for: 1 - Jane Doe
  - Check amount: 5500
  ```

#### 1.5 SalaryEmployee to CSV‑file
- **Menu**:
  ```
  Payroll Menu
  ============
  (1) Add employees
  (2) Write employees to file
  (3) Read employees from file
  (4) Print employees
  (0) Quit
  ```
- **Option 2**: Write CSV using `MyJoin`; print `X employee(s) added to file salary_employee.csv`
- **Option 3**: Read CSV using `MySplit`; print `X employee(s) read from file salary_employee.csv`
- **Option 4**: Print `Id: X Name: Y Salary: Z`

#### 1.6 Extend PayrollSystem
- **New classes**:
  - `HourlyEmployee : Employee` → `HourRate`, `HoursWorked`, `CalculateSalary() = HourRate * HoursWorked`
  - `CommissionEmployee : SalaryEmployee` → `Commission`, `CalculateSalary() = MonthlySalary + Commission`
- **Menu**:
  ```
  Salary type
  -----------
  (1) Monthly
  (2) Hourly
  (3) Commission
  (0) Quit
  ```
- **Output**: Payroll blocks with correct amounts (e.g., Hourly 60×45=2700; Commission 2500+777=3277).

#### 1.7 Complete Payroll with File handling
- **Combines** 1.5 and 1.6.
- **Menu**:
  ```
  Payroll Menu
  ============
  (1) Add employees
  (2) Write employees to file
  (3) Read employees from file
  (4) Print payroll
  (0) Quit
  ```
- **File**: `employees.csv` (not `salary_employee.csv`).
- **Requirements**:
  - Identify salary type when reading from file.
  - No duplicate employees.
  - Save original values (HourRate, not calculated salary).
- **Output**: Payroll blocks; file write/read confirmations; updated payroll after reading.
