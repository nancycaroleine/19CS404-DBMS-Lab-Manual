# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers


    DECLARE

      num1 NUMBER := 45;
    
      num2 NUMBER := 80;
    
    BEGIN

      IF num1 > num2 THEN
    
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num1);
        
      ELSE
    
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num2);
        
      END IF;
    
    END;

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Greater number is: 80

![Screenshot (264)](https://github.com/user-attachments/assets/6bda92a0-5e68-4146-90af-5a01ab3f9a24)

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

    DECLARE
   
      n   NUMBER := 10;
      
      i   NUMBER := 1;
      
      sum NUMBER := 0;
      
    BEGIN
   
      WHILE i <= n LOOP
      
         sum := sum + i;
         
         i := i + 1;
         
      END LOOP;

      DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
      
    END;


### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

![Screenshot (265)](https://github.com/user-attachments/assets/043912f4-b623-48c3-a4f6-55098eeb9c22)

---

## 3. Write a PL/SQL program to generate Fibonacci series

    DECLARE

      n   NUMBER := 7;
    
      a   NUMBER := 0;
    
      b   NUMBER := 1;
    
      c   NUMBER;
    
      i   NUMBER := 3; 
    
      result VARCHAR2(1000);
    
     BEGIN

      result := a || ', ' || b;

      WHILE i <= n LOOP
    
         c := a + b;
        
         result := result || ', ' || c;
        
         a := b;
        
         b := c;
        
         i := i + 1;
        
       END LOOP;

       DBMS_OUTPUT.PUT_LINE('Fibonacci sequence: ' || result);
      
     END;

    
### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

![Screenshot (267)](https://github.com/user-attachments/assets/c0631f42-a87d-4f65-96db-e857b8936bd2)


---

## 4. Write a PL/SQL Program to display the number in Reverse Order

     DECLARE
     
       n         NUMBER := 1535;
       
       reversed  NUMBER := 0;
       
       digit     NUMBER;
       
       original  NUMBER := 1535; 
      
     BEGIN
     
       WHILE n > 0 LOOP
       
         digit := MOD(n, 10);  
         
         reversed := reversed * 10 + digit;  
         
         n := TRUNC(n / 10);    
         
       END LOOP;

         DBMS_OUTPUT.PUT_LINE('n = ' || original);
         
         DBMS_OUTPUT.PUT_LINE('Reversed number is ' || reversed);
         
     END;

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351

![Screenshot (268)](https://github.com/user-attachments/assets/ac53b470-c66d-4fa2-b40e-114951d7fa9f)

---

## 5. Write a PL/SQL program to find the largest of three numbers

    DECLARE
    
        a NUMBER := 10;
        
        b NUMBER := 9;
        
        c NUMBER := 15;
        
        largest NUMBER;
        
     BEGIN
     
        IF a >= b AND a >= c THEN
        
           largest := a;
           
        ELSIF b >= a AND b >= c THEN
        
           largest := b;
           
        ELSE
        
           largest := c;
           
        END IF;

          DBMS_OUTPUT.PUT_LINE('a = ' || a || ', b = ' || b || ', c = ' || c);
          
          DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || largest);
          
        END;

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

![Screenshot (269)](https://github.com/user-attachments/assets/9c27ac8e-26f2-439c-af76-c5566429ff0a)


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
