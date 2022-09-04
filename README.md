# Analysis Engine

This program has 2 main parts.
1. It converts a human readable research question or analysis instruction into a structured set of instructions for the analysis engine. It takes into account the data schema provided by the user.

- For example:
```javascript

// Example input:
schema = {
    "city": {
        "type": "string",
        "null_action": "drop_row"
    },
    "age": {
        "type": "number",
        "null_action": "fill_zero"
    },
    "pid" : {
        "type": "string",
        "null_action":"drop_row"
    },
    "interests": {
        "type": "array",
        "null_action": "ignore"
    }
}

research_question = "What is the average age of people in each city?"


// Example output:
result = {
    "type":"descriptive",
    "target_variable":"age",
    "target_variable_type":"numeric",
    "target_variable_unit":"years",
    "stat_action":"mean",
    "group_by":"city",
}
```



2. It runs the instructions on a data input and produces an analysis result.