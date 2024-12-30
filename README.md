# quizapp2


from flask import Flask, render_template, request

app = Flask(__name__)

class Questions:
    q_id = -1
    question = ""
    option1 = ""
    option2 = ""
    option3 = ""
    correctOption = -1

    def __init__(self, q_id, question, option1, option2, option3, correctOption):
        self.q_id = q_id
        self.question = question  # Corrected this line to use 'question'
        self.option1 = option1
        self.option2 = option2
        self.option3 = option3
        self.correctOption = correctOption

    def get_correct_option(self):
        if self.correctOption == 1:
            return self.option1
        elif self.correctOption == 2:
            return self.option2
        elif self.correctOption == 3:
            return self.option3

# Create instances of Questions class with correct data
q1 = Questions(1, "What is the result of 3 + 2 * 2 in Python?", "10", "7", "8", 2)
q2 = Questions(2, "Which of the following is the correct syntax to create a list in Python?", "list = 1, 2, 3", "list = (1, 2, 3)", "list = [1, 2, 3]", 3)
q3 = Questions(3, "Which keyword is used to define a function in Python?", "def", "function", "define", 1)
q4 = Questions(4, "What is the purpose of the range() function in Python?", "To iterate over a range of values", "To check the size of a list", "To create a range object", 1)
q5 = Questions(5, "What is the difference between == and = in Python?", "== is used for assignment, = is used for comparison", "== is used for comparison, = is used for assignment", "Both are used for comparison", 2)
q6 = Questions(6, "What is the result of 10 / 3 in Python?", "3.5", "3.0", "3", 2)
q7 = Questions(7, "How do you get the length of a list in Python?", "length(list)", "len(list)", "list.length()", 2)
q8 = Questions(8, "What is the difference between a list and a tuple in Python?", "Lists are mutable, tuples are immutable", "Tuples are mutable, lists are immutable", "Both are mutable", 1)
q9 = Questions(9, "What is Python?", "A database", "An operating system", "A programming language", 3)
q10 = Questions(10, "How do you declare a variable in Python?", "int x = 5", "x: int = 5", "x = 5", 3)
q11 = Questions(11, "How do you write a comment in Python?", "# This is a comment", "/* This is a comment */", "<!-- This is a comment -->", 1)
q12 = Questions(12, "How do you add an item to a list in Python?", "list.add(item)", "list.insert(item)", "list.append(item)", 3)
q13 = Questions(13, "What is the output of len('Hello World')?", "10", "11", "12", 2)
q14 = Questions(14, "How do you access the first element of a list in Python?", "list[0]", "list[1]", "both of above", 1)
q15 = Questions(15, "What is the purpose of import in Python?", "To declare a variable", "To import a library or module", "To create a function", 2)
q16 = Questions(16, "What is the purpose of the break statement in Python?", "To exit the loop completely", "To pause the loop for a while", "To continue with the next iteration of the loop", 1)
q17 = Questions(17, "What does the continue statement do in Python?", "It stops the program", "It pauses the loop for a specified time", "It skips the current iteration and moves to the next iteration of the loop", 3)
q18 = Questions(18, "How do you define a tuple in Python?", "tuple = [1, 2, 3]", "tuple = {1, 2, 3}", "tuple = (1, 2, 3)", 3)
q19 = Questions(19, "How do you concatenate two strings in Python?", "str1.concat(str2)", "str1 + str2", "str1.append(str2)", 2)
q20 = Questions(20, "What is the purpose of the input() function in Python?", "To read data from a file", "To display output on the screen", "To accept user input", 3)

questions_list = [q1, q2, q3, q4, q5, q6, q7, q8, q9, q10, q11, q12, q13, q14, q15, q16, q17, q18, q19, q20]

@app.route("/quiz")
def quiz():
    return render_template("quiz.html", questions_list=questions_list)

@app.route("/submitquiz", methods=["POST", "GET"])
def submit():
    correct_count = 0
    for question in questions_list:
        # Accessing question.q_id for the radio button group
        question_id = str(question.q_id)
        selected_option = request.form.get(f"option_{question_id}")  # Use 'get' instead of direct access
        correct_option = question.get_correct_option()
        
        # Compare selected option with the correct one
        if selected_option == correct_option:
            correct_count += 1  # Correct the logic to increment the count
            
    return str(correct_count)  # Return the count as a string to be displayed

if __name__ == "__main__":
    app.run(debug=True)
