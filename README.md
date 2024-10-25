
# 🚀 Rule Engine with AST 🌳

## Overview
This project implements a **Rule Engine** using **Abstract Syntax Tree (AST)** to dynamically create, combine, and modify rules. The system evaluates user eligibility based on attributes such as age, department, income, and experience. Rules are stored in a **MySQL** database and processed using **Spring Boot**. The UI allows users to interact with the system easily.

## 🎯 Objective
The aim of this project is to create a 3-tier application (UI, API, Backend Data) that allows dynamic rule creation and evaluation using AST. The rules help in determining user eligibility based on specified conditions like age, department, income, and experience.

### ✨ Features
- 🛠️ **Dynamic Rule Creation**: Create rules using string input, which are converted to an AST.
- ⚙️ **Rule Combination**: Combine multiple rules into one.
- ✔️ **Rule Evaluation**: Evaluate a set of attributes against the rule's AST.
- 🔄 **Rule Modification**: Modify existing rules dynamically.

## 🗂️ Project Structure
```
src
├── main
│   ├── java
│   │   └── com.example.demo
│   │       ├── controller
│   │       ├── model
│   │       ├── repository
│   │       └── service
│   ├── resources
│   │   ├── static
│   │   │   └── index.html
│   │   └── application.properties
├── test
└── pom.xml
```

### 📄 Key Classes

- **Node.java**: Represents a node in the AST, either as an operator (AND/OR) or operand (e.g., `age > 30`).
- **Rule.java**: Represents a rule, composed of AST nodes.
- **RuleService.java**: Handles business logic for rule creation, combination, and evaluation.
- **RuleController.java**: Exposes API endpoints to create and evaluate rules.

## 🛠️ Data Structure
The AST is implemented using the `Node` class, with fields like:
- **type**: Determines if the node is an operator or operand.
- **left**: Reference to the left child node.
- **right**: Reference to the right child node.
- **value**: Stores the value for operand nodes.

### Example Rule
```plaintext
((age > 30 AND department = 'Sales') OR (age < 25 AND department = 'Marketing')) AND (salary > 50000 OR experience > 5)
```

## 📦 API Design
1. **create_rule**: Create an AST from a rule string.
   - **Endpoint**: `POST /create-rule`
   - **Input**: Rule string (e.g., `"age > 30 AND department = 'Sales'"`)
   - **Output**: JSON representation of the AST.

2. **combine_rules**: Combine multiple rules into one AST.
   - **Endpoint**: `POST /combine-rules`
   - **Input**: List of rule strings.
   - **Output**: Combined AST.

3. **evaluate_rule**: Evaluate a rule against user data.
   - **Endpoint**: `POST /evaluate-rule`
   - **Input**: JSON with user attributes (e.g., `{ "age": 35, "department": "Sales", "salary": 60000 }`)
   - **Output**: `true` if the rule matches, otherwise `false`.

## 🗄️ Database Design
The MySQL database stores rules and nodes with the following schema:

### Tables:
1. **rules**
   - `id`, `name`, `rule_string`, `ast_json`.

2. **nodes**
   - `id`, `type`, `left_node_id`, `right_node_id`, `value`.

## 🧪 Test Cases
1. **Create Rule**: Verify correct AST generation.
2. **Combine Rules**: Ensure correct AST logic when combining multiple rules.
3. **Evaluate Rule**: Test with different user data and ensure rules are correctly applied.

## 💻 Live Demo (UI)
You can access a simple user interface to interact with the Rule Engine. To access the live demo:
- Start the application using the instructions below.
- Open a browser and go to `http://localhost:8080`.
  
![UI Screenshot](path-to-your-screenshot.png)

### 🎨 UI Features
- A form to create and combine rules.
- A field to input JSON data and evaluate rules against it.
  
### 📸 Screenshot Example
![UI Rule Engine Example](path-to-your-second-screenshot.png)

## 📦 Getting Started
1. **Clone the repository**:
   ```bash
   git clone https://github.com/babureddynr/-Rule-Engine-with-AST.git
   cd -Rule-Engine-with-AST
   ```

2. **Configure MySQL**:
   Modify `application.properties` with your MySQL credentials:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/rule_engine
   spring.datasource.username=root
   spring.datasource.password=yourpassword
   ```

3. **Run the application**:
   ```bash
   mvn spring-boot:run
   ```

## 🧑‍💻 Author
**Babu Reddy NR**  
Connect with me on [GitHub](https://github.com/babureddynr).

## 🛠️ Commands to Push Code

To push your code to the GitHub repository, follow these steps:

```bash
git init
git add .
git commit -m "Initial commit with Rule Engine"
git branch -M main
git remote add origin https://github.com/babureddynr/-Rule-Engine-with-AST.git
git push -u origin main
```

## 🚀 Future Enhancements
- 🔄 **Dynamic Rule Modification**: Extend rule modification to support adding/removing nodes.
- 📈 **Advanced Conditions**: Support for more complex rule logic, including user-defined functions.

```

This updated `README.md` includes:
- Emojis 🎉 for enhanced readability.
- Screenshot placeholders to visually explain UI and features.
- A live demo section for easier access to the application.
