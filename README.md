
# Rule Engine with AST

## Overview
This project implements a Rule Engine using Abstract Syntax Tree (AST) to dynamically create, combine, and modify rules. The system evaluates user eligibility based on attributes such as age, department, income, experience, etc. The rules are stored in a MySQL database and processed using a Spring Boot-based backend with a simple UI for interaction.

## Objective
Develop a 3-tier application (UI, API, and Backend Data) that allows dynamic rule creation and evaluation using ASTs. The rules are applied to determine user eligibility based on conditions involving attributes like age, department, income, and experience.

### Features
1. **Dynamic Rule Creation**: Users can define rules using string inputs, which are converted to an AST.
2. **Rule Combination**: Multiple rules can be combined into a single AST.
3. **Rule Evaluation**: Given user data in JSON format, the system evaluates whether the data satisfies the rules.
4. **Rule Modification**: Existing rules can be dynamically updated.

## Project Structure
```
src
├── main
│   ├── java
│   │   └── com.example.demo
│   │       ├── controller
│   │       │   └── RuleController.java
│   │       ├── model
│   │       │   ├── Node.java
│   │       │   └── Rule.java
│   │       ├── repository
│   │       │   ├── NodeRepository.java
│   │       │   └── RuleRepository.java
│   │       └── service
│   │           └── RuleService.java
│   ├── resources
│   │   ├── static
│   │   │   └── index.html
│   │   └── application.properties
├── test
└── pom.xml
```

### Key Classes

- **Node.java**: Represents a node in the AST. Each node can be an operator (AND/OR) or an operand (conditions like age, department, etc.).
- **Rule.java**: Represents a rule, composed of multiple AST nodes.
- **RuleService.java**: Contains business logic for creating, combining, and evaluating rules.
- **RuleController.java**: Exposes API endpoints to create and evaluate rules.

## Data Structure
The AST is represented using the `Node` class:
- **type**: Specifies whether the node is an operator (`AND`, `OR`) or an operand (a condition like `age > 30`).
- **left**: Reference to the left child node.
- **right**: Reference to the right child node.
- **value**: Value for operand nodes (e.g., comparison values like `age > 30`).

### Example Rule
Rule 1: 
```
((age > 30 AND department = 'Sales') OR (age < 25 AND department = 'Marketing')) AND (salary > 50000 OR experience > 5)
```

## API Design
1. **create_rule(ruleString)**: Accepts a rule string and returns an AST representing the rule.
   - **Endpoint**: `POST /create-rule`
   - **Input**: Rule string (e.g., `"age > 30 AND department = 'Sales'"`)
   - **Output**: JSON representation of the AST.

2. **combine_rules(rules)**: Combines multiple rules into a single AST.
   - **Endpoint**: `POST /combine-rules`
   - **Input**: List of rule strings.
   - **Output**: Combined AST.

3. **evaluate_rule(data)**: Evaluates the AST against user data in JSON format.
   - **Endpoint**: `POST /evaluate-rule`
   - **Input**: JSON data with user attributes (e.g., `{ "age": 35, "department": "Sales", "salary": 60000, "experience": 3 }`)
   - **Output**: `true` if the data satisfies the rule, otherwise `false`.

## Database
The rules and application metadata are stored in a MySQL database. Here is a basic schema:

### Tables:
1. **rules**
   - `id` (Primary Key)
   - `name` (String)
   - `rule_string` (String): The original rule in string format.
   - `ast_json` (JSON): The AST stored as JSON.

2. **nodes**
   - `id` (Primary Key)
   - `type` (String): `operator` or `operand`.
   - `left_node_id` (Foreign Key to `nodes` table): Reference to the left child node.
   - `right_node_id` (Foreign Key to `nodes` table): Reference to the right child node.
   - `value` (String): Optional value for operand nodes (e.g., comparison values).

## Usage
1. **Create Rule**:
   ```bash
   curl -X POST http://localhost:8080/create-rule -d "ruleString=age > 30 AND department = 'Sales'"
   ```

2. **Combine Rules**:
   ```bash
   curl -X POST http://localhost:8080/combine-rules -d '{"rules": ["age > 30 AND department = 'Sales'", "salary > 50000"]}'
   ```

3. **Evaluate Rule**:
   ```bash
   curl -X POST http://localhost:8080/evaluate-rule -d '{"data": { "age": 35, "department": "Sales", "salary": 60000, "experience": 3 }}'
   ```

## Test Cases
1. **Create Individual Rules**: Verify the AST representation of the rules.
2. **Combine Rules**: Ensure that the combined AST represents the intended logic.
3. **Evaluate Rule**: Test various JSON inputs against the rules to ensure correct evaluation.
4. **Error Handling**: Ensure that invalid rules and malformed JSON inputs are handled gracefully.

## Future Enhancements
- **Rule Modification**: Implement functionality to modify existing rules by changing operators, operands, or adding/removing sub-expressions.
- **User-defined Functions**: Extend support for custom functions within the rule language for advanced use cases.

## Technologies Used
- **Spring Boot**: Backend framework.
- **MySQL**: Database for storing rules and metadata.
- **Thymeleaf**: For rendering dynamic HTML content.
- **Maven**: Build and dependency management.

## Getting Started
1. Clone the repository:
   ```bash
   git clone https://github.com/babureddynr/-Rule-Engine-with-AST.git
   cd -Rule-Engine-with-AST
   ```

2. Configure the database in `application.properties`:
   ```
   spring.datasource.url=jdbc:mysql://localhost:3306/rule_engine
   spring.datasource.username=root
   spring.datasource.password=yourpassword
   ```

3. Run the application:
   ```bash
   mvn spring-boot:run
   ```

## Author
Babu Reddy NR
