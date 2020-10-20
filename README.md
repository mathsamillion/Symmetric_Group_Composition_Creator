# Symmetric_Group_Composition_Creator
Question and Answer creator for Symmetric Group Composition

This code creates questions and the respective answers in 2 word documents.

Questions asked to user:
  1) 'How many elements do you want to work with?'
      If a value of 6 is chosen, then the elements used are {1,2,3,4,5,6}.
     
  2) 'What is the maximum length of any given cycle?'
      If 4 is chosen, then we can have the cycle (1 4 2 3) but not (1 2 4 3 5)

  3) 'What is the maximum number of cycles you want to work with?'
      If a value of 3 is chosen, then we can have questions like:
        (1 2)(4 3 2)(3 1)    or    (1 3)(4 3 1)
      but we couldn't have questions like (1 2)(3 4)(3 2 1)(4 1) as they have too many cycles.
    
  4) 'How many questions would you like to have?'
      ...
  
  
Restrictions:

  1) The maximum number of elements that can be used is 9.
        To keep track of each cycle, they're converted into an integer and added to a list 'cycles_full_index' e.g. (1 4 3 2) becomes 1432. If we allow double digits, then this method wouldn't be useable. Similarly for the number 0, the code wouldn't be able to tell the difference between (0 3 2 1) and (3 2 1). The only useable numbers are {1,2,3,4,5,6,7,8,9}.
      
      
Question Rules:

   1) Any cycle in a question won't appear more times than its length.
      This is because cycles cancel out when they appear a multiple of its length.
      So for example we can have (1 2 3) appear in a cycle twice, but not three times.
  
   2) Although the cycles (1 2 3) and (2 3 1) are the same, this code treats them differently.
      This is to allow for more questions e.g. (1 2)(1 4 2)(2 1).
      If the previous rule was followed, we wouldn't be able to have this question.
      
   3) If a question is created that doesn't need solving, it's redone.
   
   4) If a question is created multiple times, it's redone.
      The variable 'question_attempts' is increased, and when it reaches total_attempts=10 the code stops.


Brief Explaination:

As each cycle is created, it's converted to an integer, i.e. (1 3 4 2) >> 1342. This value is added to the list 'cycles_full_index' so that we have a way to index these cycles.

The conversion from cycles to integers is so we can use 'cycle_dict_tally' to keep track of how many times each cycle has been used as each question is created. This is so the code follows Rule 1.

Each question is made up of cycles from 'cycles_full_index'. So the location of these cycles are used to convert questions into integer lists 'question_index_value'.
For example, (1 2)(3 2 1)(3 1). If these cycles were located in 'cycles_full_index' at positions 5, 13, 0 respectively, then question_index_value = [5, 13, 0].

All integer lists are added to 'questions_full_index', and if any duplicates are created then the question is redone.
