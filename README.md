# Data-structure-partical-program-5
# Infix to Postfix and Evaluation
stack = []
def priority(op):
    if op == '+' or op == '-':
        return 1
    if op == '*' or op == '/':
        return 2
    if op == '^':
        return 3
    return 0

def infix_to_postfix(exp):
    output = ""
    for ch in exp:
        if ch.isdigit():
            output += ch
        elif ch == '(':
            stack.append(ch)
        elif ch == ')':
            while stack[-1] != '(':
                output += stack.pop()
            stack.pop()
        else:
            while stack and priority(ch) <= priority(stack[-1]):
                output += stack.pop()
            stack.append(ch)

    while stack:
        output += stack.pop()

    return output

def evaluate_postfix(exp):
    s = []
    for ch in exp:
        if ch.isdigit():
            s.append(int(ch))
        else:
            b = s.pop()
            a = s.pop()

            if ch == '+':
                s.append(a+b)
            elif ch == '-':
                s.append(a-b)
            elif ch == '*':
                s.append(a*b)
            elif ch == '/':
                s.append(a/b)
            elif ch == '^':
                s.append(a**b)

    return s.pop()

exp = raw_input("Enter Infix Expression: ")

post = infix_to_postfix(exp)
print "Postfix:", post

result = evaluate_postfix(post)
print "Result:", result
