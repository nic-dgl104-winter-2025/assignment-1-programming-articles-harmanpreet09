# Programming Practice Article (Code Review)
# Introduction
Code reviews are a fundamental part of software development, ensuring higher code quality, early detection of issues, and collective learning within a team. For DGL 104 students, developing strong code review habits will sharpen their programming skills and prepare them for collaborative projects. In this article, we explore the significance of code reviews, best practices, and practical examples to help you build confidence in reviewing and receiving feedback on code.
# Why Code Review Matters
1. Improved Code Quality: They help detect issues early, ensuring consistent standards and leading to robust software.
2. Knowledge Sharing: Developers learn reliable techniques and best practices through collaborative reviews.
3. Better Documentation: Reviews assist teams in creating better documentation, facilitating future feature additions and upgrades.
4. Easier QA Testing: Consistent code standards make it simpler for specialists and testers to understand and assess the code.
# Best Practices for Effective Code Reviews
To make your code reviews effective:
1. Review Small Chunks of Code: It’s easier to understand and catch issues in smaller pieces.
2. Give Clear, Helpful Feedback: Be polite and offer solutions.
3. Focus on Clarity: Check if the code is easy to read and maintain.
4. Check for Security Risks: Look for issues like unsafe user inputs
5. Use Tools to Help: Linters and analyzers can catch simple errors automatically.
6. Think About Edge Cases: Test how the code performs under unexpected conditions.
# Code Examples and Reviews
## Refactoring for Efficiency (Source: Google Engineering Practices)
The original code uses a for loop to sum an array, which works but is longer and less elegant. The improved version uses the reduce method, which is built into JavaScript and designed for exactly this kind of operation. It's more concise and typically easier to read, especially for developers familiar with modern JavaScript
```
// Original
function sumArray(arr) {
  let sum = 0;
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
  return sum;
}

// Improved Version
function sumArray(arr) {
  return arr.reduce((acc, num) => acc + num, 0);
}
```
## Example 2: Catching a Logical Bug (Source: Stack Overflow Blog)
The original code checks if a number is greater than 0, but this causes 0 to be treated as a negative number. The improved version checks if the number is greater than or equal to 0, which includes zero as a positive value, making the function more accurate and logically correct.
```
// Original
function isPositive(num) {
  return num > 0;
}
console.log(isPositive(0)); // Returns false, but may be unexpected

// Improved Version
function isPositive(num) {
  return num >= 0;
}
```
## Example 3: Improving Security with Input Validation (Source: Atlassian Blog)
The original code uses eval(), which is considered dangerous because it can execute arbitrary code, leading to security risks. The improved version validates the input type before processing, ensuring that only strings are handled, which is a safer practice.
```
// Original
function processInput(input) {
  eval(input); // Dangerous!
}

// Secure Version
function processInput(input) {
  if (typeof input === 'string') {
    console.log(input);
  }
}
```
## Example 4: Consistent Style with Linters (Source: GitHub Docs)
The original code has inconsistent spacing and uses var instead of let. The improved version corrects the formatting, making the code cleaner and easier to read, and uses let for block-scoped variables, which is recommended in modern JavaScript.
```
// Original (Inconsistent Style)
let sum=0;
for(let i=0;i<10;i++){sum+=i;}

// Corrected Version
let sum = 0;
for (let i = 0; i < 10; i++) {
  sum += i;
}
```
# Code Review Checklist
1. Functionality :- The code should meet all requirements and handle errors gracefully. It should cover different scenarios, including edge cases. For example, the code below reads from a file, processes it, and handles errors if the file is missing:
  ```
try:
    with open("inputfile.txt", "r") as f:
        lines = f.readlines()

    with open("outputfile.txt", "w") as f:
        for line in lines:
            f.write(line.strip().upper())

except FileNotFoundError:
    print("Input file not found")
except Exception as e:
    print(f"An error occurred: {e}")
  ```
2. Clarity :- Good code is easy to read and self-explanatory. Use descriptive variable names, proper comments, and consistent formatting. Here’s an example with clear naming and a simple structure:
     ```
    def calculate_total_price(price, quantity, tax_rate):
    """Calculate the total price, including tax."""
    total_price = (price * quantity) * (1 + tax_rate)
    return total_price
   ``` 
3. Organization :- Organized code is easy to maintain and extend. Each function should perform one clear task. This example shows how breaking tasks into functions improves structure:
    ```
    def process_data(data):
    """Process data through filtering, transformation, and analysis."""
    filtered_data = filter_data(data)
    transformed_data = transform_data(filtered_data)
    results = analyze_data(transformed_data)
    return results
    ```
4. Maintainability :- Well-maintained code is easy to test, modify, and debug. Follow consistent naming conventions and keep functions reusable. Here’s a simple calculator class with clear methods:
 ```
    class Calculator:
    def __init__(self):
        self.result = 0

    def add(self, num):
        """Add a number to the result."""
        self.result += num
        return self.result

    def subtract(self, num):
        """Subtract a number from the result."""
        self.result -= num
        return self.result
   ```
5. Performance :- Efficient code runs quickly and uses resources effectively. Measure execution time to identify slow operations. For example:
 ```
import time
start = time.time()
# Code to be tested for performance
end = time.time()
print(f"Time elapsed: {end - start:.5f} seconds")
 ```
     
