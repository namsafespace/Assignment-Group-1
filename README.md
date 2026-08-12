# Assignment-Group-1

Programming Languages Lab – Names, Bindings and Scopes
Group 1: University Examination Eligibility and Result Processing System

This program implements a prototype that checks examination eligibility and, for eligible students, computes CAT, practical, and exam marks, total marks, grade, and summary statistics. The code is structured using named constants and modular functions as required.

Variable attributes and named constants
Named constants MIN_UNITS, MAX_UNITS, MAX_CAT, MAX_PRACTICAL, MAX_EXAM, and PASS_MARK are declared at the top of the file as const int. They replace magic numbers and define the registered units range, mark maxima, and pass mark used throughout the program (e.g., calculateTotal, determineGrade, and eligibility checks).

The Student struct models identity (id, name), eligibility fields (unitsRegistered, feeBalance, hasExamCard, hasDisciplinaryCase), marks (catMark, practicalMark, examMark), total (totalMark), and result fields (isEligible, passed, grade). Each instance has its own values but a common type and layout.

L‑value / R‑value and aliases
In calculateTotal, the expression
totalMark = catMark + practicalMark + examMark;
illustrates l‑value and r‑value usage. totalMark on the left of = is an l‑value that denotes the memory location where the sum is stored. On the right, catMark, practicalMark, and examMark are used as r‑values: their current contents are read and combined.

The function moderateMark(double &mark, double adjustmentValue) demonstrates aliases. The parameter mark is a reference bound directly to the caller’s variable, e.g. moderateMark(students[i].examMark, 3.0);. Inside the function, assignments to mark affect the same memory location as students[i].examMark, so both names are aliases for one l‑value.

The statement examMark = examMark + 5; shows examMark in two roles: on the left as an l‑value (target location) and on the right as an r‑value (current value). The new value is computed from the old value and written back to the same location.

Scope, shadowing, and lifetime
Eligibility, total calculation, grade determination, and reporting are implemented in separate functions (checkEligibility, calculateTotal, determineGrade, printReport), satisfying modularity. In checkEligibility, the block‑local variable reason exists only within the if/else block. Attempting to access reason outside the block would cause an error, so the function copies reason into the output parameter failureReason before returning.

A global variable adjustment is declared near the top of the file. In demonstrateShadowing, a local variable named adjustment is declared inside the function. Within this function, the local variable shadows the global; all uses of adjustment refer to the local value, while outside the function the global value is used. This demonstrates how name resolution chooses the nearest declaration in scope.

processStudent contains a static int studentCount which counts how many students have been processed. The static variable is allocated once and retains its value across calls, illustrating static lifetime. The local variable tempTotal is automatic; it is allocated on each call and destroyed when the function returns.

The function lifetimeExperiment creates one dynamically allocated Student object with new Student and later releases it with delete heapStudent. The object’s lifetime begins at allocation and ends at deletion, demonstrating dynamic storage and correct release of heap memory.

Storage binding and referencing environments
Each Student instance binds a set of names (id, name, totalMark, etc.) to specific storage locations within the struct. Global constants and variables are bound to static storage, while local variables and parameters are bound to stack frames of their respective functions. Reference parameters such as double &mark bind directly to the caller’s storage, forming aliases. These bindings form the environment in which expressions are evaluated and assignments update memory.

Output and analysis
The main function constructs an array of at least five Student records, applies eligibility checks and mark processing, and then calls printReport. The report lists each student’s ID, name, units, eligibility status, pass/fail result, total, and grade, followed by summary statistics (eligible count, pass count, highest, lowest, and average total mark). Conceptually, the program also shows that two variables with the same name in different scopes (global and local adjustment) do not share a location, while two different names (mark and students[i].examMark) can share one location via aliasing.

