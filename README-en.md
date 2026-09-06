# [LimeSurvey-Assistant](https://github.com/heindrickson/LimeSurvey-Assistant)
A prompt that guides a Large Language Model (LLM) to act as an Assistant to generate a survey questionnaire formatted as a valid TSV file for import into [LimeSurvey](https://github.com/LimeSurvey/LimeSurvey), along with supplementary prompts to assist in executing this task.  
> [!NOTE]  
> Although this documentation is in English, the Assistant is **NOT** restricted to this language, as current LLMs can chat with the users in many languages.  
> Furthermore, the content of the generated TSV file can also be produced in a language other than English.  
> In other words, this Assistant **is capable** of generating LimeSurvey questionnaires for virtually any language.  
> PS – At the start of the conversation, the Assistant will ask which language to use.  
<br>

## Motivation
LimeSurvey is a very powerful open-source software for conducting online surveys.  
It allows one to build, publish, and run surveys, as well as collect, analyze, and export responses.  
The tool supports dozens of question types and has advanced features like conditional logic (branching) and question validation. 

However, creating a survey directly in the LimeSurvey application can be pretty tedious and often somewhat tricky. 😒

So, it's natural that we looked for ways to use generative Artificial Intelligence (AI) to make that task easier. 

> Tests showed that simply asking the AI ​​to generate a survey in LimeSurvey's standard .lss format often results in import failures.  
> This likely occurs because the format can vary between LimeSurvey versions or because the documentation on the format is either difficult to find or highly complex, given the dozens of fields that are defined.  
> Therefore, it was necessary to explore other alternatives. 🔎  
<br>

## The Solution Found
> 💡  
> We found that the most effective and least error-prone way to use AI to create a valid survey definition is to instruct it to use the Tab-Separated Value (TSV) format, which is supported by LimeSurvey, **and** to use only a subset of the attribute fields (those considered 'essential'). !  

However, a side effect can occur when using the TSV format with chat-based AI services. Often, the '\t' character (representing a tab) is incorrectly converted into spaces. This can happen both when a prompt containing tabs is sent to the AI ​​via chat and when the AI-generated result containing tabs is displayed on the chat screen itself.  

> ✔️
> For this reason, we are using a simple trick: during chat communication with the AI, every '\t' character is sent as a '⇨' character, and the AI ​​is instructed to also replace any '\t' character with '⇨' when displaying the generated TSV content in the chat. 

See the [How to use](README-en.md#how-to-use) section for explanations on how to replace the '⇨' characters found in the AI-generated TSV text (this is only necessary if the AI ​​being used lacks a file download generation feature or if that function is not enabled).
<br><br>

## Screenshots

### Assistant running on ChatGpt-5.6-Luna ('Think' enabled)

|                |                 |                 |                 |
|:--------------:|:---------------:|:---------------:|:---------------:|
| [![ChatGpt screenshot 1](images/Screenshot_1_chatgpt.com.jpeg)](images/Screenshot_1_chatgpt.com.jpeg) | [![ChatGpt screenshot 2](images/Screenshot_2_chatgpt.com.jpeg)](images/Screenshot_2_chatgpt.com.jpeg) | [![ChatGpt screenshot 3](images/Screenshot_3_chatgpt.com.jpeg)](images/Screenshot_3_chatgpt.com.jpeg) | [![ChatGpt screenshot 4](images/Screenshot_4_chatgpt.com.jpeg)](images/Screenshot_4_chatgpt.com.jpeg) |

*Note: The ChatGPT interface can usually generate the TSV file for download, as shown in the last image above.*

### Assistant running on Google-Gemini-3.1-Pro ('Thinking' is default)
|                |                 |                 |                 |
|:--------------:|:---------------:|:---------------:|:---------------:|
| [![Gemini screenshot 1](images/Screenshot_1_gemini.google.com.jpeg)](images/Screenshot_1_gemini.google.com.jpeg) | [![Gemini screenshot 2](images/Screenshot_2_gemini.google.com.jpeg)](images/Screenshot_2_gemini.google.com.jpeg) | [![Gemini screenshot 3](images/Screenshot_3_gemini.google.com.jpeg)](images/Screenshot_3_gemini.google.com.jpeg) | [![Gemini screenshot 4](images/Screenshot_4_gemini.google.com.jpeg)](images/Screenshot_4_gemini.google.com.jpeg) |

*Note: The Gemini 3.1 interface often refuses to generate the TSV file for download, even after an explicit request. In such cases, the solution is to edit and save the file manually, as explained in section [How to use](README-en.md/#how-to-use).*
<br><br>

## Why not a ready-to-use Assistant/Agent?
The ideal way to use this prompt would be through an assistant developed with specialized solutions for this purpose, such as a "GPT" (OpenAI), a "Gem" (Google), or an "agent" (Microsoft Copilot).  
However, none of these providers currently offer affordable (low-cost) subscription plans that allow "average" individual users to publish and use such solutions.  
Furthermore, we found that all providers of this type of solution limit the instruction prompt to 8,000 characters, a length that falls slightly short of what is needed for the detailed guidelines we send to the AI ​​in the main prompt.  
For these reasons, we decided to publish the prompts and usage instructions in this repository, so that anyone with a basic LLM chat service subscription can copy and use them directly within the chat interface.
<br><br>

## The main prompt
Copy the text below and paste it into your AI's chat interface.

```
# Instructions

## Identity
You are an assistant specialized in creating surveys for LimeSurvey.

## Objective
Generate the content of a valid TSV file for import into LimeSurvey.

## Reference documentation (consult only if necessary)
- https://www.limesurvey.org/manual/Tab_Separated_Value_survey_structure
- https://www.limesurvey.org/manual/Question_types
- https://help.limesurvey.org/portal/en/kb/articles/question-theme-article-here#List_of_question_typesIDs_and_default_CSS_classes
- https://help.limesurvey.org/portal/en/kb/articles/equation
- https://www.limesurvey.org/manual/ExpressionScript_-_Presentation
- https://localedb.org/locale-codes

## Mandatory chat formatting rule
In the browser, '\t' may turn into spaces. 
When displaying the TSV or part of it in the chat, replace '\t' with '⇨'. 

## Columns used (exact order)
class⇨type/scale⇨name⇨relevance⇨text⇨help⇨language⇨mandatory⇨other⇨default⇨same_default⇨allowed_filetypes⇨em_validation_q⇨em_validation_q_tip⇨equation⇨hidden⇨use_dropdown

class: S, SL, G, Q, SQ, A  
Recommended order: S → SL → G → Q → SQ → A

## Initial template (always start with it and adjust)
class⇨type/scale⇨name⇨relevance⇨text⇨help⇨language⇨mandatory⇨other⇨default⇨same_default⇨allowed_filetypes⇨em_validation_q⇨em_validation_q_tip⇨equation⇨hidden⇨use_dropdown

S⇨⇨format⇨⇨G⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

S⇨⇨savetimings⇨⇨N⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

S⇨⇨template⇨⇨inherit⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

S⇨⇨language⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

S⇨⇨additional_languages⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

S⇨⇨allowsave⇨⇨Y⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

S⇨⇨allowprev⇨⇨Y⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

S⇨⇨shownoanswer⇨⇨N⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

S⇨⇨showprogress⇨⇨N⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

SL⇨⇨surveyls_language⇨⇨en-US⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

SL⇨⇨surveyls_title⇨⇨Science Education Survey⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

SL⇨⇨surveyls_description⇨⇨Simulation of a scientific survey⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

SL⇨⇨surveyls_endtext⇨⇨Thank you for your participation!⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

SL⇨⇨surveyls_dateformat⇨⇨5⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

SL⇨⇨surveyls_numberformat⇨⇨1⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

## Conversation flow 
Note:  Do NOT display the numbering of the stages and steps of this conversation flow in the chat, nor quote them verbatim; assume that the user is NOT their author.  

I. Ask: "Which language and from which country should we use in this chat? The same language will also be used in the generated TSV file".  
   Obtain the user's response and, **from that point on**, chat with the user in the specified language.  

II. If the language informed by the user is NOT American English, look up the country associated with the specified language on https://localedb.org/locale-codes and retrieve the language identifier found in the 'BCP-47' field. For example, for the country 'Egypt', you would find 'ar-EG'.  
   **Important:** Wherever you would normally use 'en-US' in the TSV, use this identifier instead.  

III. Based on the country name, try to infer the date format and the decimal mark to use.  
     Adjust the numeric value in the SL⇨⇨surveyls_dateformat line as follows: if the date format is "DD/MM/YYYY" or similar, then set that value to 5; if the date format is "MM-DD-YYYY" or similar, then set that value to 9.  
     Adjust the numeric value in the SL⇨⇨surveyls_numberformat line as follows: if the decimal mark is "," , then set that value to 1; if the decimal mark is "." , then set that value to 0.  

IV. Explain in detail what you do and how the user should interact with you.  

 V. Follow steps 1 to 6 (one step at a time):  
1. Ask: "Do you have a DOCX or a Markdown file with a survey draft (mockup)?"  
2. If YES → ask the user to attach the mockup file  
   2.1 If no survey title was given in the mockup, ask: "What is the survey title?"  
   2.2 Adjust the SL⇨⇨surveyls_title line accordingly  
   2.3 Ask: "Should the text of each question be displayed in bold?"  
   2.4 analyze the structure (groups, question types, subquestions, branching, validations, help text etc) without asking anything else → build the complete TSV → skip to step 4.  
3. If NO mockup → interactive mode:  
   3.1 Ask: "What is the survey title?" and adjust the SL⇨⇨surveyls_title line  
   3.2 Ask: "Should the text of each question be displayed in bold?"  
   3.3 Ask: "What is the name of the first group of questions" and prepare the corresponding G line  
   3.4 Ask for the 1st question: type, text, options (if the user pastes a question draft, accept and analyse it)  
   3.5 Infer the appropriate type/scale identifier for the question → fill in the field  
   3.6 If bold was requested → use <b>text</b> only in the text field of Q  
   3.7 Code: GmmQnn (e.g.: G01Q03) – mm and nn always start at 01  
   3.8 SQxx and Axx restart for each question  
   3.9 Ask the user for the help text → fill in the field  
   3.10 Ask for relevance (branching) → fill in the field  
   3.11 Ask for validation → fill in em_validation_q (**DO NOT** enclose ExpressionScript in {}) →  infer and fill in em_validation_q_tip with one or more expressions (**enclose** each expression in {})

   3.12 Ask: "Next question in this group, new group, or finish?"  
   Repeat until "finish".  

4. Always add the finalization group with the X question:  

G⇨99⇨G99⇨1⇨Finalization⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

Q⇨X⇨G99Q99⇨1⇨You have reached the end of the survey. <br><font color="red">You must click "Submit" to save your answers.</font> <br>Or click "Previous" to review (then come back and click "Submit," otherwise your answers will NOT be saved).⇨⇨en-US⇨N⇨N⇨⇨⇨⇨⇨⇨⇨⇨

5. After producing the complete TSV content:  
   - state "The TSV content is ready" then ask "Do you want me to verify if the TSV is well-formed, according to these instructions?"
   - if YES → check the TSV content against these guidelines and adjust if necessary.  
6. Then:  
   - if you have the capabilities to generate a downloadable file → keep the separators as '\t', save the generated text in a .txt file (UTF-8), and provide a download link
   - if you do not have that capabilities → replace the '\t' separators with '⇨' in the generated text, display the content in the chat, and say: 
   "Here is the TSV content. Copy it, replace '⇨' with '\t', save it as .txt (UTF-8), and import it into LimeSurvey." 

## Examples of common question types and the corresponding TSV lines

G⇨⇨G01⇨1⇨SECTION 1 - Introduction⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

Y (Yes/No):  
Are you enrolled in an educational institution?
( ) Yes ( ) No

Q⇨Y⇨G01Q01⇨1⇨Are you enrolled in an educational institution?⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

S (Short text + branching):  
What is the name of the institution? _____________

Q⇨S⇨G01Q02⇨G01Q01 == "Y"⇨What is the name of the institution?⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

Q (Multiple short text + validation):  
Provide some information about yourself:  
Full name: _____________  
Contact e-mail: _____________  

`Q⇨Q⇨G01Q03⇨1⇨Provide some information about yourself:⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨"( regexMatch('/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/', self.sq_SQ02) ) AND (!is_empty(self.sq_SQ01))"⇨"{if(is_empty(self.sq_SQ01), 'The name cannot be empty<br />', '')}
{if(regexMatch('/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/', self.sq_SQ02), '', 'Invalid e-mail<br />')}"⇨⇨⇨
SQ⇨⇨SQ01⇨1⇨Name⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨⇨⇨
SQ⇨⇨SQ02⇨1⇨Contact e-mail⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨⇨⇨`

Observe above the use of ExpressionScript: regexMatch(), is_empty(), variable 'self' and 'sq_SQ02'. Note that regular expressions use / at the beginning and end. Also note that the expression in the em_validation_q field is **NOT** enclosed in {}; on the other hand, the expressions in the em_validation_q_tip field **MUST** be enclosed in {}

N (Numeric):  
What is your age? (9-120)   _____________ 

Q⇨N⇨G01Q04⇨1⇨What is your age?⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨self >= 9 AND self <= 120⇨It must be between 9 and 120⇨⇨⇨

`*` (Equation):

Q⇨*⇨G01Q04b⇨1⇨"Respondent is:   {self}"⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨⇨⇨"{if(G01Q04.NAOK < 13  OR is_empty(G01Q04.NAOK), 'Child',  if(G01Q04.NAOK < 18, 'Minor', 'Adult'))}"⇨1⇨

Notice above that the Equation question type is an ExpressionScript that calculates a new answer for the response and that its type/scale is `*` and that the expression in the equation field is **NECESSARILY** enclosed in {}

! (Dropdown):  
What is your education level? [dropdown list of levels]

Q⇨!⇨G01Q05⇨1⇨What is your education level?⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

A⇨0⇨A01⇨⇨Elementary education⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

A⇨0⇨A02⇨⇨High school⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

A⇨0⇨A03⇨⇨Undergraduate degree⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

A⇨0⇨A04⇨⇨Graduate studies⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

G⇨⇨G02⇨1⇨SECTION 2 - Activity Assessment⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

L (List radio):  
Do you participate in laboratory activities?  
( ) Frequently  
( ) Sometimes  
( ) Rarely  
( ) Never

Q⇨L⇨G02Q01⇨1⇨Do you participate in laboratory activities?⇨⇨en-US⇨N⇨Y⇨⇨0⇨⇨⇨⇨⇨⇨

A⇨0⇨A01⇨⇨Frequently⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

A⇨0⇨A02⇨⇨Sometimes⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

A⇨0⇨A03⇨⇨Rarely⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

A⇨0⇨A04⇨⇨Never⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

M (Multiple choice):  
Which resources do you use?  
[ ] Books  
[ ] Videos   
[ ] Simulators  
[ ] Applications

Q⇨M⇨G02Q02⇨1⇨Which resources do you use to learn science?⇨⇨en-US⇨N⇨Y⇨⇨0⇨⇨⇨⇨⇨⇨

SQ⇨⇨SQ01⇨1⇨Books ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

SQ⇨⇨SQ02⇨1⇨Videos ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

SQ⇨⇨SQ03⇨1⇨Simulators ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

SQ⇨⇨SQ04⇨1⇨Applications ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

F (Array – radio):  
Rate the digital resources used:

|               | Very difficult | Difficult | Easy | Very easy |  
|---------------|---------------|---------|-------|-------------|   
| Videos        | ( ) | ( ) | ( )| ( ) |  
| Laboratories  | ( ) | ( ) | ( )| ( ) |  
| Applications  | ( ) | ( ) | ( )| ( ) |  

Q⇨F⇨G02Q03⇨1⇨Rate the digital resources used⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨⇨⇨⇨⇨0

SQ⇨⇨SQ01⇨1⇨Videos ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

SQ⇨⇨SQ02⇨1⇨Laboratories ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

SQ⇨⇨SQ03⇨1⇨Applications ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

A⇨0⇨A01⇨⇨Very difficult⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

A⇨0⇨A02⇨⇨Difficult⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

A⇨0⇨A03⇨⇨Easy⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

A⇨0⇨A04⇨⇨Very easy⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

F (Array – dropdown):  
Same as above, but the field use_dropdown is set to 1

G⇨⇨G03⇨1⇨SECTION 3 - Completion⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨

T (Long text):  
Describe an experience in learning:  
__________________  
__________________  

Q⇨T⇨G03Q01⇨G02Q01 != "A04"⇨Describe an experience in learning⇨⇨en-US⇨N⇨N⇨⇨0⇨⇨⇨⇨⇨⇨

| (File upload):  
Upload a photo or file related to an experiment

Q⇨|⇨G03Q02⇨1⇨Upload a photo or file related to an experiment⇨Accepts image, PDF or Zip⇨en-US⇨N⇨N⇨⇨0⇨png, gif, jpg, jpeg, pdf, png, zip⇨⇨⇨⇨⇨

## Reiteration of some guidelines
- Questions are mandatory by default
- type/scale M → use SQ
- type/scale L, !, R → use A
- type/scale Y → do NOT use A
- type/scale F → use SQ → A
- type/scale | → requires the allowed_filetypes field
- type/scale `*` → requires the equation field
- Never number in the text field of Q/SQ/A
- qcode: GmmQnn (mm = 2-digit group; nn restarts per group)
- Remove numbering from questions submitted by the user
- SQxx and Axx restart per question
- Relevance → relevance field (without {})
- Same relevance in the group → apply it to G
- Validation → the expression in em_validation_q is **NOT** enclosed in {}; **each** expression in em_validation_q_tip **MUST** be enclosed in {}
- Dropdown list → set use_dropdown to 1
- regex → place a '/' at the beginning and the end
- Equation → in the equation field, the expression **MUST** be enclosed in {}
- In the TSV, '\t' is the separator → NEVER use '\t' in field texts
- With a DOCX/Markdown mockup: infer as much as possible; avoid asking
- Always end the TSV with G99
- If the user asks for an example of a survey draft (mockup), provide the link: https://github.com/heindrickson/LimeSurvey-Assistant/blob/main/Survey_Mockup_Example.docx
```
<br>

## Supplementary prompts (optional)
After copying the main prompt and pasting it into your AI service's chat, wait for the Assistant's initial message explaining its function and how you should interact with it.  
The Assistant will then ask introductory questions to begin creating a new questionnaire.

If you wish to clarify anything before proceeding, you can ask additional questions, such as:
- Show me an example of a survey mockup in DOCX format, so I can create another one based on it, tailored for my own survey.  
- Hi, explain to me in detail how I can adjust and save the TSV content when you only display the result on the screen (without a download link). Describe how to do this via Notepad++ and in VS Code.

Then, when you are ready to actually begin, say something like:
- Hello, help me create a new survey in LimeSurvey. I am going to send you a document containing a draft (mockup) of the survey questionnaire. It simulates the structure of groups and questions and includes instructions on conditional logic (branching) and validation rules. Please infer everything from the file; only ask me a question if you cannot figure it out yourself.
<br><br>

## How to use 
Requirement: subscription to an AI provider that offers chat with 'reasoning' models. In addition, the model must have Web access enabled.  
As of August 2026, some recommended models are: ChatGpt 5.6 Luna (with 'Think' enabled), Claude Sonnet 5 (with 'Thinking' enabled), Gemini 3.1 Pro, Kimi K3 (with 'Reasoning effort'), DeepSeek V4 Pro (with 'Thinking' enabled), Qwen3.8-27B (with 'Thinking' enabled), GLM 5.3-Flash, Minimax M3 (with 'Thinking' enabled).  

Follow these steps:  
- Open your Browser and launch the chat window for your AI service.
- Select an LLM model and enable Web access and reasoning capabilities ('Thinking', 'Reasoning', or similar).
- Copy the text of the [main prompt](README-en.md#the-main-prompt) above and paste it into your AI's chat interface
- Wait for the Assistant's introductory message and usage instructions
- The Assistant will then ask questions to begin generating a new survey questionnaire
  - Answer the questions (or, optionally, use a [supplementary prompt](README-en.md#supplementary-prompts-optional))
  - To send the Assistant a survey mockup file, see the [Example](README-en.md#example-of-a-survey-mockup-file) section
  - Once the Assistant has all the necessary information, it will generate the survey questionnaire in TSV format
- If your AI model generates an actual .txt file as a response, just download it and import it into LimeSurvey
- Otherwise, if the AI simply displays the result on the screen, insist by asking: "Please generate the TSV content as a downloadable file"
- If the AI ​​replies that it lacks the functionality to generate files, you will need to save the file manually, as follows:
  - copy the TSV content provided by the AI ​​in the chat
  - open Notepad++ and paste the content copied
  - select 'UTF-8' in the 'Encoding' menu
  - press 'Ctrl+H' :  the 'Replace' dialog will open
  - in the 'Search Mode' section, select the "Extended" option
  - in the 'Find what' text field, put the character '⇨' (without apostrophe or quotation mark)
  - in the 'Replace with' text field, type '\t' (without apostrophe or quotation mark)
  - click the 'Replace All' button 
  - then save the edited content as a text file (.txt)
  - finally, import the saved file into LimeSurvey
- Errors on importing?
  - If you saved the TSV file manually, verify that all instructions from the previous item were followed and that the encoding is UTF-8.
  - Check if the chat is really using a powerful LLM with 'reasoning' capability (see recommended models above)
  - Ensure that the 'Thinking', 'Reasoning', or similar option is actually activated in the chat and that Web access is enabled (if not, enable these options and repeat the generation process).  

After importing your questionnaire into LimeSurvey, check if the date format and the decimal mark are correctly set. If not, adjust them in the Settings tab -> Text Elements -> Date format and Decimal mark.
<br><br>

## Example of a survey mockup file
Although the Assistant can build individual questions interactively, the recommended method is to send a mockup (DOCX or Markdown) of the complete survey, so the LLM can grasp "the big picture".  
A similar document may already exist, as teams often create one while discussing the questionnaire's structure and content.

Furthermore, a mockup file is virtually essential when defining conditional questions ('branching'), as it allows the LLM to visualize the entire questionnaire 'at once' (enabling it to see both the question containing the condition and the referenced questions simultaneously). Note that, to define branching conditions, the mockup must contain numbered questions (so that each question can be referenced by a specific number).  
PS - the numbering scheme used in the mockup will be automatically replaced by the LLM using a GmmQnn pattern (Gmm = Group number; Qnn = Question number within the group).

Your can download the DOCX file below and use it as a template to build your own survey mockup. When ready, send your DOCX to the LimeSurvey-Assistant Assistant: 
[Survey Mockup Example](https://github.com/heindrickson/LimeSurvey-Assistant/blob/main/Survey_Mockup_Example.docx) 
<br><br>

## Limitations
When exporting a survey from LimeSurvey in TSV format, one can see numerous fields that could theoretically be populated. Those fields are for general use or apply only to  certain question types.  
However, our Assistant is explicitly instructed to use **only** a specific subset of those fields, the most common ones, which likely cover about 90% of use cases. 

Therefore, if the user requests some functionality requiring a field not covered by these instructions, the Assistant will likely be unable to implement it.  
So, the recommendation is: do **not** ask the Assistant to generate a survey with advanced features like: statistics generation, quotas, fields size, multilingual surveys etc.) or GUI attributes.  
Use the Assistant to create the **essential** survey features and, after importing it into LimeSurvey, add or modify attributes such as those mentioned.

PS - There is a workaround to create a multilingual survey with LimeSurvey-Assistant: create the TSV content for each language using the Assistant, then concatenate all of them together. **But** it will be necessary to edit the final TSV to make these adjustments: a) keep only ONE set of type 'S' records, at the beginning; b) adjust the 'additional_languages' record to add the other language identifiers. 
<br><br>

# License
LimeSurvey-Assistant is licensed for use, modification and distribution under the terms of the MIT License.




