# Edx Grader Java Assessment Reference Repo

This document serves to show you how you need to organize your solutions repo so that our Grader
can use it for assessments.

## Prerequisites

- For Java assessments, always start out with a bare maven repository.
- Ideally, use the `mvn-archetype-quickstart` archetype to generate the project.

If you have the maven command-line utility installed, you can generate the project easily with the following command:

```bash
mvn -B archetype:generate \
-DgroupId=<YOUR NAMESPACE HERE> \
-DartifactId=<ASSESSMENT NAME>-grader-repo \
-DarchetypeArtifactId=maven-archetype-quickstart \
-DarchetypeVersion=1.4
```

## The Layout

The typical layout of the project will look as follows:

```
/
├── pom.xml
├── Questions
│   ├── Question1.xml
│   ├── Question2.xml
│   ├── Question3.xml
│   ├── Question4.xml
│   └── Question5.xml
├── README.md
└── src
    ├── main
    │   └── java
    │       └── assessment
    │           ├── Question1.java
    │           ├── Question2.java
    │           ├── Question3.java
    │           ├── Question4.java
    │           └── Question5.java
    └── test
        └── java
            └── assessment
                ├── TestQuestion1.java
                ├── TestQuestion2.java
                ├── TestQuestion3.java
                ├── TestQuestion4.java
                └── TestQuestion5.java
```

- The `pom.xml` file is your central project configuration file. If your project needs **ANY** external dependency, it **MUST** be listed in this file appropriately.
    - You **SHOULD** overwrite the default `dependencies` and `build` sections in your pom.xml with the values available in this repository.
    - Make sure you don't overwrite the entire file, **JUST** those 2 sections.
- The `Questions` directory must contain edx-compatible-xml versions of your Assessment Questions.
- The `src/main/java/assessment` directory should contain the actual java code for problem that students need to solve.
    - Each file here **MUST** follow the following naming scheme: `QuestionX.java`, where `X` is the question number.
- The `src/test/java/assessment` directory should contain the tests that will verify if the student's code works or not.
    - Each file here **MUST** follow the following naming scheme: `TestQuestionX.java`, where `X` is the question number.
    - We highly recommend a 1:1 relationship between a `QuestionX.java` file and a `TestQuestionX.java` file.
    - i.e., If you have a `Question1.java` file, then **ALL** it's tests should be written inside a `TestQuestion1.java` file.

## EDX Question XML

Here's a general template to follow for each `Question.xml` file:

```xml
<problem>
  <coderesponse queuename="openedx">
    <label>YOUR QUESTION PROMPT SHOULD BE WRITTEN HERE</label>
    <textbox rows="15" cols="80" mode="java" tabsize="4"/>
    <codeparam>
      <initial_display>
      THIS IS WHERE THE INITIAL BOILERPLATE CODE FOR THE QUESTION SHOULD BE WRITTEN
      </initial_display>
      <answer_display>
      THIS IS WHERE THE COMPLETE SOLUTION CODE SHOULD BE WRITTEN
      </answer_display>
      <grader_payload>
        {"program_name": "QuestionX", "program_output": "n/a", "program_language": "java", "solution_repo": "YOUR REPO'S SSH CLONE URL SHOULD GO HERE"}
      </grader_payload>
    </codeparam>
  </coderesponse>
</problem>
```

Please make a note of the values you'll need to modify to make use of this template.

For a more complete example, you can view the [Question1.xml](Questions/Question1.xml) we have in this repo.

### NOTE

- When you're pasting the code into the xml file, make sure you replace angle brackets with their xml escaped versions.
- i.e., every `<` should be replaced with `&lt;` and every `>` should be replaced with `&gt;` including the semi-colons.

## Writing Your Tests

- Please use TestNG to write your tests.
- Make sure you add TestNG as a dependency to your `pom.xml` file.
