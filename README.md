# linearalgebra
# 🧮 Gaussian Elimination Method (Python)

This project demonstrates how to solve a **system of linear equations** using the **Gaussian elimination method** in Python.  
It was created for study purposes (Linear Algebra class, AI major at Kookmin University 🇰🇷).

---

## 📘 Description

The Gaussian elimination algorithm transforms an augmented matrix into a reduced row-echelon form to find the values of unknown variables (x, y, z).

Example system:
x + y + 2z = 9
2x + 4y - 3z = 1
3x + 6y - 5z = 0


---

## 💻 Python Code

```python
import math 
 
def gauss_elimination(matrix): 
    # Apply Gaussian elimination 
    for i in range(min(len(matrix), len(matrix[0]) - 1)): 
        # Exclude when dividing by 0 
        max_row = max(range(i, len(matrix)), key=lambda k: abs(matrix[k][i])) 
        matrix[i], matrix[max_row] = matrix[max_row], matrix[i] 
 
        # Make pivot element 1 
        pivot = matrix[i][i] 
        for j in range(len(matrix[0])): 
            matrix[i][j] /= pivot 
 
        # Remove other rows 
        for k in range(len(matrix)): 
            if k != i: 
                factor = matrix[k][i] 
                for j in range(len(matrix[0])): 
                    matrix[k][j] -= factor * matrix[i][j] 
 
    # Extract solutions 
    solutions = [row[-1] for row in matrix] 
    return solutions 
 
# Row to apply / Last element is a constant value 
augmented_matrix = [ 
    [1, 1, 2, 9], 
    [2, 4, -3, 1], 
    [3, 6, -5, 0] 
] 
 
result = gauss_elimination(augmented_matrix) 
 
# Check for NaN or Inf in the result 
if any(math.isnan(val) or math.isinf(val) for val in result): 
    print("The system of equations has no solution or infinite solutions.") 
else: 
    formatted_result = [round(val, 2) for val in result] 
print("Simultaneous equations solution:", formatted_result)

Simultaneous equations solution: [2.0, 1.0, 3.0]
