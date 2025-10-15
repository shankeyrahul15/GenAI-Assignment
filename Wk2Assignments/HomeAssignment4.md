//Generate test data for credit card applications for different types of cards and conditions
--Prompt for API(Postman)--

{
  "model": "llama-3.3-70b-versatile",
  "messages": [
    {
      "role": "user",
      "content": "- Generate test data for credit card application\n - Make sure to cover different types of cards (e.g., Visa, MasterCard, Amex)\n - Make sure to cover different conditions (e.g., approved, declined, pending)\n - Provide data in tabular format with columns: Card Type, Applicant Name, Credit Score, Income, Application Status, Reason (if declined or pending)\nExample:|Platinum Rewards|Sarah Johnson|780|95,000|Declined|Credit score below minimum threshold|\nMANDATORY: Provide me the total number of testcases in the response for me to count"
    },
    {
      "role": "system",
      "content": "You are a Test Data Generator for Credit Card Applications"
    },
    {
      "role": "assistant",
      "content": "he generated test data should be in tabular format as shown in the example"
    }
  ],
  "temperature": 0.1
}
