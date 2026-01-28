# SIMPLE CALCULATOR (CONSOLE BASED)


# Operator precedence dictionary (data structure)

precedence = {
    '+': 1,
    '-': 1,
    '*': 2,
    '/': 2
}

# Function to perform calculation
def apply_operator(a, b, operator):
    if operator == '+':
        return a + b
    elif operator == '-':
        return a - b
    elif operator == '*':
        return a * b
    elif operator == '/':
        if b == 0:
            raise ZeroDivisionError("Division by zero is not allowed.")
        return a / b

# We asked AI for this Function
# Function to convert infix to postfix (Shunting Yard Algorithm)
def infix_to_postfix(expression):
    stack = []      # operator stack
    postfix = []    # output list

    tokens = expression.split()

    for token in tokens:
        if token.isdigit():
            postfix.append(token)

        elif token == '(':
            stack.append(token)

        elif token == ')':
            while stack and stack[-1] != '(':
                postfix.append(stack.pop())
            stack.pop()  # remove '('

        else:  # operator
            while (stack and stack[-1] != '(' and
                   precedence[token] <= precedence[stack[-1]]):
                postfix.append(stack.pop())
            stack.append(token)

    while stack:
        postfix.append(stack.pop())

    return postfix

# We asked AI for this Function
# Function to evaluate postfix expression
def evaluate_postfix(postfix):
    stack = []

    for token in postfix:
        if token.isdigit():
            stack.append(int(token))
        else:
            b = stack.pop()
            a = stack.pop()
            result = apply_operator(a, b, token)
            stack.append(result)

    return stack[0]

# Main calculator function
def calculator():
    while True:
        print("\nSIMPLE CALCULATOR")
        print("1. Calculate Expression")
        print("2. Exit")

        choice = input("Choose an option: ")

        if choice == '1':
            print("\nEnter expression with spaces between numbers and operators")
            print("Example: ( 3 + 5 ) * 2 ")
            print("\n")
            expression = input("Expression: ")

            try:
                postfix = infix_to_postfix(expression)
                result = evaluate_postfix(postfix)
                print(f"Result: {result}")

            except ZeroDivisionError as e:
                print("Error:", e)
            except Exception:
                print("Invalid input. Please check your expression.")

        elif choice == '2':
            print("Calculator exited.")
            break

        else:
            print("Invalid menu choice.")

# Run program
calculator()
