# Survey Definition Language (SDL)

## Table of Contents
1. [Introduction](#1-introduction)
2. [Overview of Survey Definition Language](#2-overview-of-survey-definition-language)
    - [Structure](#structure)
    - [Syntax](#syntax)
3. [SDL Components](#3-sdl-components)
    - [Survey](#survey)
    - [Section](#section)
    - [Page](#page)
    - [Question](#question)
4. [Question Types](#4-question-types)
    - [Text](#text)
    - [Single Choice](#single-choice)
    - [Checkbox](#checkbox)
    - [Rating](#rating)
    - [Binary](#binary)
    - [Slider](#slider)
    - [Dropdown](#dropdown)
    - [Likert Scale](#likert-scale)
    - [Date Picker](#date-picker)
5. [Survey Variants](#5-survey-variants)
    - [Single-Page Surveys](#single-page-surveys)
    - [Multi-Page Surveys](#multi-page-surveys)
6. [SDL Syntax Specifications](#6-sdl-syntax-specifications)
    - [JSON-LD Format](#json-ld-format)
    - [Semantic Annotations](#semantic-annotations)
7. [Creating a Survey](#7-creating-a-survey)
    - [Without Sections](#without-sections)
    - [With Sections](#with-sections)
8. [Advanced Topics](#8-advanced-topics)
9. [Best Practices](#9-best-practices)
10. [Versioning and Updates](#10-versioning-and-updates)
11. [Example Surveys](#11-example-surveys)
12. [Language Extensions](#12-language-extensions)
13. [SDL Schema Reference](#13-sdl-schema-reference)
14. [Appendix](#14-appendix)






---

## 1. Introduction

The Survey Definition Language (SDL) is a language designed for defining and structuring surveys. It provides a flexible and robust way to create surveys that can range from simple questionnaires to complex forms with multiple pages and dynamic content. This document serves as a comprehensive guide to SDL, detailing its structure, components, syntax, and use cases.

---

## 2. Overview of Survey Definition Language

SDL is a JSON-based language that allows for the easy creation and interpretation of survey forms. It is designed to be both human-readable and machine-processable, ensuring ease of use for survey creators and seamless integration with survey platforms.

### Structure
SDL documents are structured as JSON objects, facilitating their integration with web technologies and data handling methods. The core components of an SDL document include:

- **Survey:** The root element representing the entire survey.
- **Section:** Optional subdivision of a survey, representing a page or a logical grouping of questions.
- **Question:** The fundamental unit of a survey, representing an individual query or prompt.

### Syntax
SDL uses a JSON syntax with specific keywords and structures. Essential elements include:

- `@context`: Specifies the version and context of SDL being used.
- `@type`: Defines the type of element (e.g., "Survey", "Section", "Question").

---

## 3. SDL Components

### Survey
The survey object is the root element of an SDL document. It encapsulates all other elements and provides global properties for the survey.

#### Properties
- `@context`: (Required) The SDL context version.
- `@id`: (Required) A unique identifier for the survey.
- `title`: (Optional) The title of the survey.
- `description`: (Optional) A brief description of the survey.
- `sections`: (Optional) An array of section objects.

### Section
A section represents a subdivision of a survey, often corresponding to a page.

#### Properties
- `title`: (Optional) The title of the section.
- `questions`: (Required) An array of question objects.

### Page
A page is similar to a section but is specifically used in multi-page surveys to group questions.

#### Properties
- Inherits all properties from the Section component.

---

## 4. Question Types

Each question type is designed to capture specific types of responses. Below are examples of how each question type should be written in the SDL.

### Text
- **Description:** Allows respondents to input freeform text.
- **Sample Usage:**
  ```json
  {
    "@type": "Question",
    "questionText": "Please describe your experience with our service:",
    "questionType": "Text",
    "isRequired": true
  }
  ```

### Single Choice
- **Description:** Lets respondents select one option from a predefined set of choices.
- **Sample Usage:**
  ```json
  {
    "@type": "Question",
    "questionText": "What is your favorite color?",
    "questionType": "Single Choice",
    "options": ["Red", "Blue", "Green", "Yellow"],
    "isRequired": true
  }
  ```

### Checkbox
- **Description:** Allows multiple selections from a set of options.
- **Sample Usage:**
  ```json
  {
    "@type": "Question",
    "questionText": "Select the fruits you like:",
    "questionType": "Checkbox",
    "options": ["Apple", "Banana", "Orange", "Grapes"],
    "isRequired": false
  }
  ```

### Rating
- **Description:** Enables rating using a numerical scale. The scale property defines the range, e.g., a scale of 5 allows ratings from 1 to 5.
- **Usage Notes:** This type is ideal for feedback, satisfaction, or preference surveys.
- **Sample Usage:**
  ```json
  {
    "@type": "Question",
    "questionText": "Rate our customer service (1: Poor, 5: Excellent):",
    "questionType": "Rating",
    "scale": 5,
    "isRequired": true
  }
  ```

### Binary
- **Description:** A simple 'True' or 'False' question.
- **Sample Usage:**
  ```json
  {
    "@type": "Question",
    "questionText": "Do you agree with our terms and conditions?",
    "questionType": "Binary",
    "isRequired": true
  }
  ```
### Slider
- **Description:** Allows respondents to select a value from a sliding scale.
- **Sample Usage:**
  ```json
  {
    "@type": "Question",
    "questionText": "On a scale of 1 to 10, how would you rate your level of satisfaction with our product?",
    "questionType": "Slider",
    "minValue": 1,
    "maxValue": 10,
    "isRequired": true
  }
  ```

### Dropdown
- **Description:** Presents a list of options in a dropdown menu for selection.
- **Sample Usage:**
  ```json
  {
    "@type": "Question",
    "questionText": "Select your country of residence:",
    "questionType": "Dropdown",
    "options": ["United States", "Canada", "United Kingdom", "Australia", "Other"],
    "isRequired": true
  }
  ```

### Likert Scale
- **Description:** Measures attitudes or feelings on a multi-point scale.
- **Sample Usage:**
  ```json
  {
    "@type": "Question",
    "questionText": "How much do you agree with the following statement: 'The customer service was satisfactory'",
    "questionType": "Likert Scale",
    "options": ["Strongly Disagree", "Disagree", "Neutral", "Agree", "Strongly Agree"],
    "isRequired": true
  }
  ```
### Date Picker
- **Description:** Allows respondents to select a date from a calendar.
- **Sample Usage:**
  ```json
  {
    "@type": "Question",
    "questionText": "Select your date of birth:",
    "questionType": "Date Picker",
    "isRequired": true,
    "dateFormat": "YYYY-MM-DD" // Default format if not specified by the  user
  }
  ```


---

### 5. Survey Variants

SDL supports both single-page and multi-page surveys, accommodating various survey lengths and complexities.

#### Single-Page Surveys
- **Structure:** Consists of a series of questions without section divisions.
- **Use Case:** Ideal for short surveys or forms.

#### Multi-Page Surveys
- **Structure:** Organized into multiple sections, each representing a page.
- **Use Case:** Suited for longer surveys, allowing logical grouping and progression.

---

### 6. SDL Syntax Specifications

SDL adopts the JSON-LD format for ease of integration with web technologies and semantic annotations.

#### JSON-LD Format
- **Advantages:** Compatible with standard web technologies and facilitates semantic tagging.
- **Syntax:** Uses standard JSON syntax with additional `@context` and `@type` properties.

#### Semantic Annotations
- **Purpose:** Enhances the meaning of survey elements, aiding in automated processing and analysis.
- **Implementation:** Utilizes JSON-LD's ability to define context and type for each element.

---

## 7. Creating a Survey

### Without Sections
- **Structure:** A flat list of questions for single-page surveys.
- **Complete Example:**

```json
{
  "@context": "cgi:itc:sdl:context;1",
  "@id": "survey123",
  "title": "General Feedback Survey",
  "questions": [
    {
      "@type": "Question",
      "questionText": "Please describe your experience with our service:",
      "questionType": "Text",
      "isRequired": true
    },
    {
      "@type": "Question",
      "questionText": "What is your favorite color?",
      "questionType": "Single Choice",
      "options": ["Red", "Blue", "Green", "Yellow"],
      "isRequired": true
    },
    {
      "@type": "Question",
      "questionText": "Select the fruits you like:",
      "questionType": "Checkbox",
      "options": ["Apple", "Banana", "Orange", "Grapes"],
      "isRequired": false
    },
    {
      "@type": "Question",
      "questionText": "Rate our customer service (1: Poor, 5: Excellent):",
      "questionType": "Rating",
      "scale": 5,
      "isRequired": true
    },
    {
      "@type": "Question",
      "questionText": "Do you agree with our terms and conditions?",
      "questionType": "Binary",
      "isRequired": true
    },
    {
      "@type": "Question",
      "questionText": "On a scale of 1 to 10, how would you rate your level of satisfaction with our product?",
      "questionType": "Slider",
      "minValue": 1,
      "maxValue": 10,
      "isRequired": true
    },
    {
      "@type": "Question",
      "questionText": "Select your country of residence:",
      "questionType": "Dropdown",
      "options": ["United States", "Canada", "United Kingdom", "Australia", "Other"],
      "isRequired": true
    },
    {
      "@type": "Question",
      "questionText": "How much do you agree with the following statement: 'The customer service was satisfactory'",
      "questionType": "Likert Scale",
      "options": ["Strongly Disagree", "Disagree", "Neutral", "Agree", "Strongly Agree"],
      "isRequired": true
    },
    {
      "@type": "Question",
      "questionText": "Select your date of birth:",
      "questionType": "Date Picker",
      "isRequired": true,
      "dateFormat": "YYYY-MM-DD"
    }
  ]
}
```

### With Sections
- **Structure:** Used for multi-page surveys, where each section represents a separate page.
- **Complete Example:**

```json
{
  "@context": "cgi:itc:sdl:context;1",
  "@id": "survey456",
  "title": "Employee Engagement Survey",
  "sections": [
    {
      "title": "Section 1: Work Environment",
      "questions": [
        {
          "@type": "Question",
          "questionText": "Is your workplace comfortable?",
          "questionType": "Binary",
          "isRequired": true
        },
        {
          "@type": "Question",
          "questionText": "Describe your ideal work environment:",
          "questionType": "Text",
          "isRequired": false
        },
        {
          "@type": "Question",
          "questionText": "Select the facilities available at your workplace:",
          "questionType": "Checkbox",
          "options": ["Cafeteria", "Gym", "Recreation Area", "Parking"],
          "isRequired": false
        }
      ]
    },
    {
      "title": "Section 2: Job Satisfaction",
      "questions": [
        {
          "@type": "Question",
          "questionText": "Rate the level of your job satisfaction:",
          "questionType": "Rating",
          "scale": 5,
          "isRequired": true
        },
        {
          "@type": "Question",
          "questionText": "Choose your preferred work schedule:",
          "questionType": "Single Choice",
          "options": ["Regular 9-5", "Flexible", "Remote", "Shift-based"],
          "isRequired": true
        },
        {
          "@type": "Question",
          "questionText": "On a scale from 1 to 10, how likely are you to recommend our company to a friend?",
          "questionType": "Slider",
          "minValue": 1,
          "maxValue": 10,
          "isRequired": true
        }
      ]
    },
    {
      "title": "Section 3: Professional Development",
      "

questions": [
        {
          "@type": "Question",
          "questionText": "How often do you seek professional development opportunities?",
          "questionType": "Dropdown",
          "options": ["Regularly", "Occasionally", "Rarely", "Never"],
          "isRequired": true
        },
        {
          "@type": "Question",
          "questionText": "How much do you agree with the statement: 'My job role aligns with my career goals'?",
          "questionType": "Likert Scale",
          "options": ["Strongly Disagree", "Disagree", "Neutral", "Agree", "Strongly Agree"],
          "isRequired": true
        },
        {
          "@type": "Question",
          "questionText": "Select your date of joining the company:",
          "questionType": "Date Picker",
          "isRequired": true,
          "dateFormat": "YYYY-MM-DD"
        }
      ]
    }
  ]
}
```

These examples provide clear, complete illustrations of both single-page and multi-page surveys using the SDL format, with each question type and section usage accurately represented.

---

### 8. Advanced Topics (coming in later version)

#### Conditional Logic
- **Description:** Allows the survey to adapt based on responses to previous questions.
- **Implementation:** Utilizes `if-then-else` structures within questions to trigger conditional paths.

#### Dynamic Content
- **Description:** Content changes based on user input or external data.
- **Implementation:** Supports dynamic variables and real-time data integration.

#### More Question Types
- **Matrix Question:** Allows respondents to evaluate multiple items using the same set of response options.
- **File Upload** Enables respondents to upload a file.

---

### 9. Best Practices

#### Survey Design
- **Clarity:** Ensure questions are clear and concise.
- **Relevance:** Only include questions that serve the survey's objective.
- **Engagement:** Use a variety of question types to maintain respondent interest.

#### Technical Considerations
- **Validation:** Implement input validation for data quality.
- **Accessibility:** Ensure the survey is accessible to all users, including those with disabilities.
- **Security:** Protect respondent data and adhere to privacy standards.

---

### 10. Versioning and Updates

- **Version Control:** Use version numbers in `@context` to manage updates.
- **Backward Compatibility:** Strive for backward compatibility with previous versions.

---

### 11. Language Extensions

- **Localization:** Support for multiple languages in surveys.
- **Advanced Validation:** Complex validation rules for inputs.

---

### 12. SDL Schema Reference

- **Survey Object:** Root element schema.
- **Section Object:** Schema for survey sections.
- **Question Object:** Schema for different question types.
