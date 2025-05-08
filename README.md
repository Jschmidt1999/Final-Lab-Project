### 🎓 Lab 10 – Jackson Schmidt

# Final-Lab-Project

**Displaying short answer and algorithm responses dynamically with formatting.**

---

> *“Enjoy my heavily over-engineered Lab 10 Assignment that I'm pretty sure you can get a 100 on without writing any code, haha.”*

This project demonstrates:
- Class-based design (encapsulation, dynamic method calls)
- Dictionary-based storage and retrieval
- Clean terminal UI formatting (typing effect, line-by-line output)
- Separation of logic by header/question/answer display

---

### 📁 Files
- `main.py` — core script for timed question/answer display
- `README.md` — this file you're reading
- No external dependencies required (standard Python libraries)
### 🎬 Demo

![Demo of Lab 10 Script](demo.gif)

---

### 🔧 How to Run
```bash
python main.py

#  =======================================================
#  !!! BEST VIEWED IN FULL SCREEN FOR DISPLAY PURPOSES !!!
#  =======================================================

import time

class SillyDisplayTimer:
    # Initializes the timer with a default or custom delay
    def __init__(self, delay=0.75):
        self.delay = delay  # Delay between outputs in seconds

    # Pauses the program for the set delay time
    def pause(self):
        time.sleep(self.delay)

    # Prints a single line with an optional custom delay
    def print_line(self, text, delay=None):
        print(text)
        time.sleep(delay or self.delay)

    # Prints a block of lines, one by one, with optional delay between each
    def print_block(self, block_lines, delay=None):
        for line in block_lines:
            self.print_line(line, delay)

    # Simulates typing each character in a string for animated text output
    def type_line(self, text, speed=0.01):
        for char in text:
            print(char, end='', flush=True)  # Flush forces immediate display
            time.sleep(speed)
        print()  # Move to the next line after typing is done


            
# === Headers Class for Each Header per Section

class Headers:

    # Stores headers in a dictionary
    def __init__(self):
        
        self.headers = {
            
            1: [
                "\n\n" + "\t\t" + "="   * 77,
                "\t\t" + "Lab 10 - Object-Oriented Short Answers/Algorithm Workbench | Jackson Schmidt",
                "\t\t" + "="    * 77
            ],
            2: [
                "\n\n" + "\t" * 5 + "=" * 22,
                "\t" * 5 + "Short Answer Workbench",
                "\t" * 5 + "="    * 22
            ],
            3: [
                "\n\n" + "\t" * 5 + "=" * 20,
                "\t" * 5 + "Algorithm Workbench",
                "\t" * 5 + "="    * 20
            ]
        }

    def get_header(self, number):
        # Resturns a string; Joins multi-line headers if stored as a list
        header = self.headers.get(number, ["Header not found."])
        return "\n".join(header)
    
    def display_header(self, number):
        # Returns a particular header
        print(self.get_header(number))

    def all_header_numbers(self):
        # Returns all header numbers for iteration
        return self.headers.keys()



# === Question & Answer Classes for Short Answer ===


class ShortAnswerQuestions:

    # Stores short answer questions in a dictionary
    def __init__(self):
        
        self.questions = {
            
            1: "What is encapsulation?\n",
            2: "Why should an object's data attributes be hidden from code outside the class?\n",
            3: "What is the difference between a class and an instance of a class?\n",
            4: [
                "The following statement calls an object's method. What is the name of the method?",
                "   What is the name of the variable that references the object?",
                "",
                "   wallet.get_dollar()\n"
            ],
            5: "When the __init__ method executes, what does the self parameter reference?\n"
            
        }

    def get_question(self, number):
        # Returns a string; Joins multi-line questions if stored as list
        question = self.questions.get(number, "Question not found.")
        return "\n".join(question) if isinstance(question, list) else question

    def all_question_numbers(self):
        # Returns all question numbers for iteration
        return self.questions.keys()
    

class ShortAnswerAnswers:
    
    # Stores answers as methods for each short answer question
    def __init__(self):
        
        self.answers = {
            
            1: self.answer_encapsulation,
            2: self.answer_hidden_attributes,
            3: self.answer_class_vs_instance,
            4: self.answer_wallet_method,
            5: self.answer_self_reference,

        }

    def answer_encapsulation(self):
        return "Encapsulation is the bundling of data and methods within a class to restrict direct access to the object's components."

    def answer_hidden_attributes(self):
        return "To protect the integrity of the data and to control how it is accessed or modified."

    def answer_class_vs_instance(self):
        return "A class is a blueprint; an instance is a specific object created from that blueprint."

    def answer_wallet_method(self):
        return "Method: get_dollar; Object: wallet"

    def answer_self_reference(self):
        return "'self' refers to the current instance of the class."

    def get_answer(self, number):
        # Dynamically call the method associated with the question number
        func = self.answers.get(number)
        return func() if func else "Answer not found."



# === Question & Answer Classes for Algorithm Workbench ===


class AlgorithmWorkbenchQuestions:
    
    # Stores algorithm workbench prompt
    def __init__(self):

        self.question = {
            1: [
                "Suppose my_car is the name of a variable that references an object, and go, is the name of the method.",
                "   Write a statement that uses the my_car variable to call the go method.\n"
            ]
        }

    def get_question_WB(self, number):
        # Returns a formatted string
        question = self.question.get(number, "Question not found.")
        return "\n".join(question) if isinstance(question, list) else question

    def question_number(self):
        # Returns question numbers for iteration(only 1 for this section)
        return self.question.keys()


class AlgorithmWorkbenchAnswers:
    
    # Stores answer to algorithm workbench prompt
    def __init__(self):
        
        self.answers = {
            
            1: self.answer_my_car_go
        }

    def answer_my_car_go(self):
        return "my_car.go()"

    def get_answer(self, number):
        # Returns the corresponding answer
        func = self.answers.get(number)
        return func() if func else "Answer not found."


# === Display Class that Ties It All Together ===


class DisplayAllSections:
    
    # Combines and displays both Short Answer and Algorithm Workbench sections
    def __init__(self):
        self.short_q = ShortAnswerQuestions()
        self.short_a = ShortAnswerAnswers()
        self.wb_q = AlgorithmWorkbenchQuestions()
        self.wb_a = AlgorithmWorkbenchAnswers()

    def display_all(self):
        # Local varaiable for calling each header
        headers = Headers()
        timer = SillyDisplayTimer(.5)
        
        # Displays Script Header
        timer.print_block(headers.get_header(1).split('\n'))

        # Displays Short Answer Header
        timer.print_block(headers.get_header(2).split('\n'))
        for i in self.short_q.all_question_numbers():
            timer.type_line(f"\n{i}. {self.short_q.get_question(i)}", speed=0.01)
            timer.type_line(f"\tAnswer:", speed=0.015)
            timer.type_line(f"\t{self.short_a.get_answer(i)}", speed=0.015)
            timer.pause()


        # Displays Algorithm Workbench Header
        timer.print_block(headers.get_header(3).split('\n'))
        for i in self.wb_q.question_number():
            timer.type_line(f"\n{i}. {self.wb_q.get_question_WB(i)}", speed=0.01)
            timer.type_line(f"\tAnswer:", speed=0.015)
            timer.type_line(f"\t{self.wb_a.get_answer(i)}", speed=0.015)
            timer.pause()

            
    
# === Main Script Execution ===

if __name__ == "__main__":

    lab10 = DisplayAllSections()
    lab10.display_all()

