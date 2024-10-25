# Application 1:

class Node: 
def __init__(self, node_type, value=None, left=None, right=None):
""" - node_type: "operator" (for AND/OR) or "operand" (for conditions) - value: The actual condition for operand nodes or the operator for operator nodes - left: Left child node - right: Right child node 
"""
self.type = node_type 
self.value = value 
self.left = left 
self.right = right 
def __repr__(self): 
return 
f"Node(type={self.type}, 
value={self.value}, 
left={self.left}, 
right={self.right})"



{ 
"rule_id": "unique_rule_id", 
"name": "Rule 1", 
"description": "Rule for user eligibility based on age and department", 
"ast": { 
"type": "operator",
"value": "AND", 
"left": { 
"type": "operator", 
"value": "OR", "left": { 
"type": "operand", 
"value": "age > 30" 
},
"right": { 
"type": "operand", 
"value": "department = 'Sales' " 
} 
},
"right": { 
"type": "operator", 
"value": "OR", 
"left": { 
"type": "operand", 
"value": "salary > 50000" 
}, 
"right": { 
"type": "operand", 
"value": "experience > 5" 
}
} 
}
}



import re 
def tokenize(rule_string): 
token_pattern = r'(\(|\)|AND|OR|>|<|=|!=|\w+|\d+)' 
return 
re.findall(token_pattern, rule_string) 
def create_rule(rule_string): 
tokens = tokenize(rule_string) 
return parse_expression(tokens) # Parse tokens into an AST


def combine_rules(rules): 
ast_list = [create_rule(rule) for rule in rules] # Combine ASTs with AND or OR logic 
if len(ast_list) > 1: 
root=Node('operator',value='AND',left=ast_list[0],right=ast_list[1]) 
for ast in ast_list[2:]: 
root = Node('operator', value='AND', left=root, right=ast) 
return root 
else: 
return ast_list[0]



def evaluate_rule(ast, data): 
if ast.type == 'operand': # Evaluate the condition against user data 
return eval_condition(ast.value, data) 
left_result = evaluate_rule(ast.left, data) 
right_result = evaluate_rule(ast.right, data) 
if ast.value == 'AND': 
return left_result and right_result 
elif ast.value == 'OR': 
return left_result or right_result
def eval_condition(condition, data): 
# Basic condition evaluation (you can improve this) attribute, operator, value = condition.split(' ') value = int(value) 
if value.isdigit() 
else value.strip("'") 
if operator == '>': 
return data.get(attribute) > value 
elif operator == '<':
return data.get(attribute) < value 
elif operator == '=': 
return data.get(attribute) == value 
elif operator == '!=': 
return data.get(attribute) != value 
return False




rule_ast = create_rule("age > 30 AND department = 'Sales'") 
user_data = {"age": 35, "department": "Sales", "salary": 60000, "experience": 3} 
print(evaluate_rule(rule_ast, user_data)) # True




rule1 = "((age > 30 AND department = 'Sales') OR (age < 25 AND department = 'Marketing')) AND (salary > 50000 OR experience > 5)" 
rule2 = "((age > 30 AND department = 'Marketing')) AND (salary > 20000 OR experience > 5)" 
ast1 = create_rule(rule1) 
ast2 = create_rule(rule2) 
combined_ast = combine_rules([rule1, rule2]) 
data = {"age": 35, "department": "Marketing", "salary": 60000, "experience": 3} 
result = evaluate_rule(combined_ast, data) 
print(result) # True/False based on rule logic



def modify_operator(ast, old_operator, new_operator): 
if ast.type == 'operator' and ast.value == old_operator: 
ast.value = new_operator 
if ast.left: 
modify_operator(ast.left, old_operator, new_operator) 
if ast.right: 
modify_operator(ast.right, old_operator, new_operator)





# Application 2:

All source codes are in pdf cannot attach due to the indentation
