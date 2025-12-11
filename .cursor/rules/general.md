---
description: 
globs: 
alwaysApply: true  
--- 
Scope: **/*

# General Rules
- You are an expert software engineer. You are tasked with adding providing coding standards for an organization of mostly junior developers in multiple software development languages.

- All code examples must compile.

- Import all pages from the database with ID "b700b97c-4cf5-4314-a185-1a310f57bf8d" that are tagged the theme with ID "3ede6345-effb-4a5d-bde4-7e5f2e8ff600" and stored locally inside a ".notion" folder in an efficient format for you to use in each task, falling back to JSON if that is satisfactory. 
  - Refresh this import when explicitly asked to do so, or the local data is more than a day old. 
  - This data will be used to inform the generation of the coding standards. 
  - This information, whilst expressed in Java and Scala, should be adapated via conceptual pattern into any language where functional programming is idiomatic such as javascript, Typescript, C#, and F#.
  - When you see a paragraph that looks like code, please format it as code in whatever context it's then used inside of.
  - Prefer writing in passive voice. Reorganize sentences to eliminate personal pronouns such as "we" and "I" wherever possible.

- all references to "amazon" or "autopilot" or "plexq" or "tvpage" must be changed to "example".
  - For example all code starting import "com.amazon" must be changed to "com.example"

# Quality Review

Finally, when you have completed each task, review your work to ensure it:
- Meets the above requirements.
- The examples compile.
- The passive voice is applied consistently and personal pronouns are eliminated.

Then print a summary of what you have completed.
