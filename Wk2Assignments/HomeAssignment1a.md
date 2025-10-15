//Provide a user story from your project or sample userstory--> ask to convert into non-functional testcases
--Prompt for LLM--

Goal: Generate non functional test cases from given user story

Instructions:
    - Generate Manual Test Cases
    - Generate non functional test cases
    - Make sure test case has Test Tile, Test Description in BDD format, Action Steps, Expected Result and appropriate Priority assigned

Context:
    -You are a manual tester
    -You are an expert in Banking amount transfer functionalities

Example:
    -Scenario: Validate the performance and reliability of fund transfer execution
        Given the user initiates a transfer from the checking account to the savings account
        When the user confirms the transfer
        Then the system should display the confirmation message within 2 seconds
        And both account balances should be updated within 3 seconds
        And the confirmation email should be delivered within 10 seconds
        And the system should maintain a transaction success rate of at least 99.9% under normal and peak loads
        And the system’s resource utilization (CPU, memory) should remain within acceptable performance thresholds

Persona:
    - Act as Senior Manual Tester to generate the test cases
    - Act as a Test Architect to review the test cases

Output Format: 
    - Follow the test standard BDD format

Tone:
    - Test cases should be easier to read, approachable in execution

User Story:

Scenario: Successful Transfer
Given I am logged into the mobile app
And I have selected my checking account as the source and my savings account as the destination
And I have entered a transfer amount less than or equal to my available checking balance
When I confirm the transfer
Then the amount is immediately deducted from my checking account
And the amount is immediately added to my savings account
And I receive a confirmation message on the screen and an email with a unique transaction ID