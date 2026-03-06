# Data-structure-partical-program-5
def postfix(exp):
    stack = []
    output = ""
    for ch in exp:
        if ch.isdigit():
            output += ch
        else:
            stack.append(ch)
    while stack:
        output += stack.pop()
    return output

print postfix("23+")
