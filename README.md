README:
This project automates the extraction of entities and relationships from text files using the OpenAI API. The code processes text files stored in different folders and outputs structured JSON data containing the identified entities and their relationships.

Table of Contents:
Introduction
Project Structure
Setup and Configuration
Usage
Examples
Conclusion
Introduction
The goal of this project is to extract specific information (entities) and their relationships from unstructured text files. The process involves:

Loading environment variables:
Configuring the OpenAI API.
Processing individual files to extract information.
Aggregating the extracted information into a structured JSON format.

Project Structure:
.
├── data/
│   ├── people_profiles/
│   │   └── example_profile.txt
│   ├── project_briefs/
│   │   └── example_project.txt
│   └── slack_messages/
│       └── example_message.txt
├── .env
├── main.py
└── README.md
data/: Directory containing subdirectories for different types of text files (people profiles, project briefs, slack messages).
.env: Environment variables file containing OpenAI API credentials and configurations.
main.py: Main Python script containing the code to run the pipeline.
README.md: This README file.


Setup and Configuration
Prerequisites
Python 3.x
OpenAI API account

Installation
Clone the repository:
git clone https://github.com/yourusername/information-extraction-pipeline.git
cd information-extraction-pipeline

Create and activate a virtual environment:
python3 -m venv venv
source venv/bin/activate   # On Windows, use `venv\Scripts\activate`

Install the required packages:

pip install -r requirements.txt

Set up your .env file with the following variables:
OPENAI_API_KEY=your_openai_api_key
OPENAI_API_BASE=your_openai_api_base
OPENAI_API_VERSION=your_openai_api_version

Usage
To run the information extraction pipeline, execute the following command:
python main.py
This script will process the text files in the specified folders and output the extracted entities and relationships.

Script Details
process_gpt: Calls the OpenAI API with a given prompt and system message to get the processed result.
extract_entities_relationships: Processes all files in a given folder, extracts entities and relationships using a prompt template, and collects the results.
ingestion_pipeline: Orchestrates the entire process for multiple folders and aggregates the results into a single list.
Configuration
The script uses predefined templates for each type of text file. You can customize these templates as needed.

Examples
Project Briefs
Input (File Content):
Project Name: Graph Generation Using LLM
Summary: Developing an AI solution for the finance industry.
Technologies: Python, TensorFlow
Client: FinCorp, Finance

Output:
{
  "entities": [
    {"label":"Project","id":"aidevelopment","name":"AI Development","summary":"Developing an AI solution for the finance industry."},
    {"label":"Technology","id":"python","name":"Python"},
    {"label":"Technology","id":"tensorflow","name":"TensorFlow"},
    {"label":"Client","id":"fincorp","name":"FinCorp","industry":"Finance"}
  ],
  "relationships": [
    "aidevelopment|USES_TECH|python",
    "aidevelopment|USES_TECH|tensorflow",
    "aidevelopment|HAS_CLIENT|fincorp"
  ]
}


People Profiles
Input (File Content):
Name: John Doe
Skills: Python, Machine Learning
Projects: AI Development
Output:

json
{
  "entities": [
    {"label":"Person","id":"johndoe","name":"John Doe"},
    {"label":"Technology","id":"python","name":"Python"},
    {"label":"Technology","id":"machinelearning","name":"Machine Learning"},
    {"label":"Project","id":"aidevelopment","name":"AI Development","summary":""}
  ],
  "relationships": [
    "johndoe|HAS_SKILLS|python",
    "johndoe|HAS_SKILLS|machinelearning",
    "aidevelopment|HAS_PEOPLE|johndoe"
  ]
}


Slack Messages
Input (File Content):
Message ID: 12345
Sender: John Doe
Message: Working on the AI project today.

Output:
{
  "entities": [
    {"label":"SlackMessage","id":"12345","text":"Working on the AI project today."},
    {"label":"Person","id":"johndoe","name":"John Doe"}
  ],
  "relationships": [
    "johndoe|SENT|12345"
  ]
}

F
Conclusion
This project provides an automated way to extract structured information from unstructured text files using the OpenAI API. The extracted entities and relationships can be used for various purposes, such as project management, HR analytics, and communication analysis.