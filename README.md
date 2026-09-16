# Assignment-Group-1

Programming Languages Lab – Names, Bindings and Scopes
Group 1: University Examination Eligibility and Result Processing System

This program implements a prototype that checks examination eligibility and, for eligible students, computes CAT, practical, and exam marks, total marks, grade, and summary statistics. The code is structured using named constants and modular functions as required.

Variable attributes and named constants
Named constants such as MIN_UNITS, MAX_UNITS, MAX_CAT, MAX_PRACTICAL, MAX_EXAM, and PASS_MARK replace magic numbers. The Student structure stores identity, eligibility details, marks, totals, and results.
The Student struct models identity (id, name), eligibility fields (unitsRegistered, feeBalance, hasExamCard, hasDisciplinaryCase), marks (catMark, practicalMark, examMark), total (totalMark), and result fields (isEligible, passed, grade). Each instance has its own values but a common type and layout.

L‑value / R‑value and aliases
In calculateTotal, the expression
totalMark = catMark + practicalMark + examMark;
illustrates l‑value and r‑value usage. totalMark on the left of = is an l‑value that denotes the memory location where the sum is stored. On the right, catMark, practicalMark, and examMark are used as r‑values: their current contents are read and combined.

The function moderateMark(double &mark, double adjustmentValue) demonstrates aliasing. The reference parameter mark refers directly to the caller’s variable, such as students[i].examMark. Therefore, changes made through mark also modify the original variable.
The statement examMark = examMark + 5; shows examMark in two roles: on the left as an l‑value (target location) and on the right as an r‑value (current value). The new value is computed from the old value and written back to the same location.

Scope, shadowing, and lifetime
Eligibility, total calculation, grade determination, and reporting are implemented in separate functions (checkEligibility, calculateTotal, determineGrade, printReport), satisfying modularity. In checkEligibility, the block‑local variable reason exists only within the if/else block. Attempting to access reason outside the block would cause an error, so the function copies reason into the output parameter failureReason before returning.

A global variable named adjustment is declared near the beginning of the program. In demonstrateShadowing, a local variable with the same name hides the global variable within that function. This illustrates shadowing and lexical scope.

processStudent contains a static int studentCount which counts how many students have been processed. The static variable is allocated once and retains its value across calls, illustrating static lifetime. The local variable tempTotal is automatic; it is allocated on each call and destroyed when the function returns.
The function lifetimeExperiment dynamically allocates a Student object using new and releases it with delete, demonstrating dynamic storage and proper memory management.

Storage binding and referencing environments
Each Student object associates its members with specific storage locations. Global constants and variables have static storage duration, while local variables and parameters are generally stored within function stack frames. Reference parameters bind directly to the caller’s storage, creating aliases that allow functions to modify the original data.

Output and analysis
The main function creates at least five student records, checks their eligibility, processes their marks, and produces a report. The report displays each student’s identification, name, registered units, eligibility status, pass or fail result, total marks, and grade. It also provides summary statistics, including the number of eligible students, number of students who passed, highest and lowest totals, and average total mark.
Overall, the program demonstrates constants, structures, modular functions, l-values and r-values, references, scope, shadowing, variable lifetime, dynamic memory, and summary-based reporting.

