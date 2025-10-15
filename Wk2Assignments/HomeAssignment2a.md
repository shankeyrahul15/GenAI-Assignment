//Provide a user story from your project or sample userstory--> ask to convert into non-functional testcases
--Prompt for API(Postman)--

{
  "model": "llama-3.3-70b-versatile",
  "messages": [
    {
      "role": "user",
      "content": "-Generate Manual Test Cases\n-Generate non functional test cases\n- Make sure test case has Test Tile, Test Description in BDD format, Action Steps, Expected Result and appropriate Priority assigned\n\nUser Story:\n Scenario: Successful Transfer\nGiven I am logged into the mobile app\nAnd I have selected my checking account as the source and my savings account as the destination\nAnd I have entered a transfer amount less than or equal to my available checking balance\nWhen I confirm the transfer\nThen the amount is immediately deducted from my checking account\nAnd the amount is immediately added to my savings account\nAnd I receive a confirmation message on the screen and an email with a unique transaction ID\n\nMANDATORY: Provide me the total number of testcases in the response for me to count"
    },
    {
      "role": "system",
      "content": "You are a Senior Manual Tester"
    },
    {
      "role": "assistant",
      "content": "The testcase should be in BDD format"
    }
  ]
}
