1. Read the workspace to understand how I implemented the chrome extension
2. Now, I need to add an another checkbox for test data generation, here are few recommendations:
    1. Go to panel.html and add another checkbox for test data generation
    2. Go to prompts.js and perform this >> Add prompt specific for test data generation and add it to the CODE_GENERATOR_TYPES
    3. Use that reference in the chat.js 
    4. Go to chat.js at getPromptKeys function
    5. Add additional conditional logic for random test data generation for every input field based on number of records