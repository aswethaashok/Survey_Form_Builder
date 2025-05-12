# Survey Form Builder (ReactJS)
## Date: 12-05-2025

## AIM
To create a Survey Form Builder using ReactJS..

## ALGORITHM
### STEP 1 Initialize States
mode ← 'build' (default mode)

questions ← [] (holds all survey questions)

currentQuestion ← { text: '', type: 'text', options: '' } (holds input while building)

editingIndex ← null (tracks which question is being edited)

responses ← {} (user responses to survey)

submitted ← false (indicates whether survey was submitted)

### STEP 2 Switch Modes
Toggle mode between 'build' and 'fill' when the toggle button is clicked.

Reset submitted to false when entering Fill Mode.

### STEP 3 Build Mode Logic
#### a. Add/Update Question
If currentQuestion.text is not empty:

If type is "radio" or "checkbox", split currentQuestion.options by commas → optionsArray.

Construct a questionObject:

If editingIndex is not null, replace question at that index.

Else, push questionObject into questions.

Reset currentQuestion and editingIndex.

#### b. Edit Question
Set currentQuestion to the selected question’s data.

Set editingIndex to the question’s index.

#### c. Delete Question
Remove the selected question from questions.

### STEP 4 Fill Mode Logic
#### a. Render Form
For each question in questions:

If type is "text", render a text input.

If type is "radio", render radio buttons for each option.

If type is "checkbox", render checkboxes.

#### b. Capture Responses
On input change:

For "text" and "radio", update responses[index] = value.

For "checkbox":

If option exists in responses[index], remove it.

Else, add it to the array.

### STEP 5 Submit Form
When user clicks "Submit":

Set submitted = true.

Display a summary using the questions and responses.

### STEP 6 Display Summary
Iterate over questions.

Display the response from responses[i] for each question:

If it's an array, join it with commas.

If empty, show "No response".


## PROGRAM

```
App.js

 import React, { useState } from "react";
import "./App.css";

const defaultCheckboxOptions = [
  "Performance",
  "Stability",
  "User Interface",
  "None",
  "Other feature"
];

function App() {
  const [mode, setMode] = useState("build");

  const [title, setTitle] = useState("Product Feedback Survey");
  const [checkboxQuestion, setCheckboxQuestion] = useState(
    "Which features do you value the most?"
  );
  const [checkboxOptions, setCheckboxOptions] = useState(defaultCheckboxOptions);
  const [selectedOptions, setSelectedOptions] = useState([]);

  const submitSurvey = () => {
    alert(`Submitted: ${selectedOptions.join(", ")}`);
    setSelectedOptions([]);
  };

  return (
    <div className="app">
      <button onClick={() => setMode(mode === "build" ? "fill" : "build")}>
        Switch to {mode === "build" ? "Fill" : "Build"} Mode
      </button>

      <h1>{title}</h1>

      {mode === "build" ? (
        <div className="build-mode">
          <label>Survey Title:</label>
          <input
            value={title}
            onChange={(e) => setTitle(e.target.value)}
            className="input"
          />

          <label>Question:</label>
          <input
            value={checkboxQuestion}
            onChange={(e) => setCheckboxQuestion(e.target.value)}
            className="input"
          />

          {checkboxOptions.map((opt, idx) => (
            <input
              key={idx}
              value={opt}
              onChange={(e) => {
                const newOptions = [...checkboxOptions];
                newOptions[idx] = e.target.value;
                setCheckboxOptions(newOptions);
              }}
              className="input"
            />
          ))}
          <button
            onClick={() =>
              setCheckboxOptions([...checkboxOptions, `item${checkboxOptions.length + 1}`])
            }
          >
            Add Option
          </button>
        </div>
      ) : (
        <div className="fill-mode">
          <p>{checkboxQuestion}</p>
          {checkboxOptions.map((opt, idx) => (
            <div key={idx}>
              <input
                type="checkbox"
                checked={selectedOptions.includes(opt)}
                onChange={() =>
                  setSelectedOptions((prev) =>
                    prev.includes(opt) ? prev.filter((o) => o !== opt) : [...prev, opt]
                  )
                }
              />
              <label>{opt}</label>
            </div>
          ))}
          <button onClick={submitSurvey}>Submit</button>
        </div>
      )}
    </div>
  );
}

export default App;
```
```
App.css

.app {
  font-family: Arial, sans-serif;
  padding: 20px;
  background: linear-gradient(to right, #f0f8ff, #e6e6fa); 
}

button {
  margin: 10px 0;
  color: blueviolet;
  padding: 8px 16px;
  background-color: #ffffff; 
}

.input {
  display: block;
  margin: 5px 0 10px;
  padding: 6px;
  width: 300px;
  background-color: #ebe6e6; 
}

.build-mode, .fill-mode {
  margin-top: 20px;
  border: 1px solid #d62c2c;
  padding: 20px;
  border-radius: 8px;
  background: linear-gradient(to bottom, #ffe4e1, #561b1b); 
}
```



## OUTPUT

![Screenshot 2025-05-12 111519](https://github.com/user-attachments/assets/c24f5c58-d034-4dc8-9422-bf039c465ea5)

![Screenshot 2025-05-12 111530](https://github.com/user-attachments/assets/fc13ee15-3302-47ce-887d-8a4cbdcc2f04)



## RESULT
The program for creating Survey Form Builder using ReactJS is executed successfully.
