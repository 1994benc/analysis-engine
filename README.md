# Analysis Engine

This program has 2 main parts.
1. It converts a human readable research question or analysis instruction into a structured set of instructions for the analysis engine. It takes into account the data schema provided by the user.

- For example:
```javascript

// Example input:
schema = [
    {
        "name": "name",
        "type": "string",
        "null_action": "drop_row"
    },
    {
        "name": "age",
        "type": "number",
        "null_action": "fill_zero"
    },
    {
        "name":"city"
        "type": "string",
        "null_action":"drop_row"
    },
    {
        "name": "interests",
        "type": "array",
        "null_action": "ignore"
    }
]

research_question_1 = "What is the {average} {age} of people in each {city}?"


// Example output:
result_1 = {
    "type":"descriptive",
    "target_variable":"age",
    "target_variable_type":"numeric",
    "target_variable_unit":"years",
    "stat_action":"mean",
    "group_by":"city",
}

research_question_2 = "Are there any {significant differences} between the {average} {age} of people in each {city}?"

result_2  = {
    "type":"comparative",
    "comparison_variable":"age",
    "comparison_variable_type":"numeric",
    "comparison_variable_unit":"years",
    "comparison_stat_action":"compare_mean",
    "between":"city"
}
```



2. It runs the instructions on a data input and produces an analysis result.