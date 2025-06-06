# Start Smart: Build Your First AI Using Azure AI Foundry

- [Start Smart: Build Your First AI Using Azure AI Foundry](#start-smart-build-your-first-ai-using-azure-ai-foundry)
  - [Exercise 1: Build Your First Agent in Azure AI Foundry](#exercise-1-build-your-first-agent-in-azure-ai-foundry)
    - [Task 1: Deploy an AI Hub](#task-1-deploy-an-ai-hub)
    - [Task 2: Create an Agent](#task-2-create-an-agent)
  - [Exercise 2: Powerful Agentic Workflows Using Power Automate](#exercise-2-powerful-agentic-workflows-using-power-automate)
    - [Task 1: Create an Instant Cloud Flow](#task-1-create-an-instant-cloud-flow)
    - [Task 2: Configure the HTTP action](#task-2-configure-the-http-action)
    - [Task 3: Configure the Parse JSON action](#task-3-configure-the-parse-json-action)
    - [Task 4: Add Send an Email action](#task-4-add-send-an-email-action)
    - [Task 5: Manually test the flow](#task-5-manually-test-the-flow)


In this lab, you will learn how to build your first AI agent using Azure AI Foundry and integrate it with Power Automate for workflow automation. The lab is divided into two main exercises:

1. **Exercise 1:** Guides you through deploying an AI Hub in Azure, creating a project, deploying an agent using the GPT-4o-mini model, and enriching it with knowledge from a PDF document. You will also test your agent's capabilities in the playground.

2. **Exercise 2:** Demonstrates how to create an automated workflow using Power Automate. You will set up an instant cloud flow that sends user queries to your Azure AI agent and delivers the AI-generated responses via email.

By completing this lab, you will gain hands-on experience in deploying AI solutions on Azure and automating interactions using Microsoft Power Platform.

## Exercise 1: Build Your First Agent in Azure AI Foundry

### Task 1: Deploy an AI Hub

1. Go to [https://portal.azure.com/](https://portal.azure.com/).

2. In the top search bar, type "AI Foundry" and select **Azure AI Foundry**.

    ![The AI Foundry search results are displayed.](media/search-ai-foundry.png)

3. In the left navigation, expand the **Use with AI Foundry** left menu item, select **AI Hubs**, select **Create**, then **Hub**.

    ![Create AI Hub option.](media/create-ai-hub.png)

4. Create a new Resource Group:
   - Use the format `<yourname>-rg`

   ![The resource group name entry form is displayed.](media/create-resource-group.png)

5. Add the Hub name:
   - Use the format `<yourname>-hub`
   - You can add a friendly name
   - Do not change any default values

   ![The completed AI Hub form is displayed.](media/new-ai-hub-form.png)

8. Select **Next: Storage** — leave all values as-is  
9. Select **Next: Inbound Access** — leave all values as-is  
10. Select **Next: Outbound Access** — leave all values as-is  
11. Select **Next: Encryption** — leave all values as-is  
12. Select **Next: Identity** — leave all values as-is  
13. Select **Next: Tags** — skip creating tags  
14. Select **Next: Review + Create**  
15. Select **Create**

    ![The AI Hub confirmation page is displayed.](media/new-ai-hub-create.png)

    ![The deployment in progress page is displayed.](media/deployment-in-progress.png)

16. Wait for deployment confirmation: "Your deployment is complete".

17. Select **Go to resource**.

    ![The deployment is completed and the Go to Resource button is highlighted.](media/deployment-completed.png)

18. Select **Launch Azure AI Foundry**.

    ![The Launch AI Foundry button is displayed.](media/launch-ai-foundry.png)

### Task 2: Create an Agent

1. In your AI Hub space, select **New Project**.

    ![The New Project button is highlighted.](media/ai-foundry-new-project.png)

2. In the popup:
   - Name your project `<yourname>-project`.
   - Select **Create**.

   ![The new project form is completed.](media/ai-foundry-new-project-form.png)

3. You will see your project dashboard.

    ![The AI Foundry project dashboard is displayed.](media/ai-foundry-project-dashboard.png)

4. Select **Agents** in the left navigation.

5. Select the Azure OpenAI resource:
   - Select **Let’s go**.

   ![The Azure OpenAI resource is selected and the Let's Go button is highlighted.](media/ai-foundry-agents-lets-go.png)

6. Pick a model for your agent:
   - Choose `gpt-4o-mini`.
   - Select **Confirm**.

   ![The gpt-4o-mini model is selected and the Confirm button is highlighted.](media/ai-foundry-select-model.png)

7. Deploy the model:
   - Select **Deploy**.

   ![The model deployment button is highlighted.](media/ai-foundry-deploy-model.png)

8. You'll be navigated to the **My agents** screen.

    ![The My Agents screen is displayed.](media/ai-foundry-my-agents.png)

9. Select your agent, then:
   - In the right navigation, go to **Knowledge**.
   - Select **Add**.

   ![The Add button in the agent's Knowledge section is highlighted.](media/agent-add-knowledge-button.png)

10. Select **Files** to upload the [cloth mask vs medical mask.pdf](cloth-mask-vs-medical-mask.pdf?raw=true) PDF.
    - Select **Upload and save**.
    - The file is now added to the vector store.

    ![The PDF is uploaded and the Upload and Save button is highlighted.](media/agent-upload-file.png)

11. Test your model:
    - Select **Try in Playground**.
    - Enter a query in the input box.

    ![The Try in Playground button is highlighted.](media/agent-try-in-playground-button.png)

> Examples:
> 
> - What documents do I have available?
> - Breakdown the differences in efficacy between cloth and medical masks, based on the provided data.
> - Can you create a diagram that shows these differences?

![The Agent playground is displayed with chat results.](media/agent-chat-in-playground.png)

## Exercise 2: Powerful Agentic Workflows Using Power Automate

> ⚠️ *Note: Only proceed after successfully creating your Agent in Azure AI Foundry.*

> [!IMPORTANT]
> You must have a [Power Automate Premium license](https://go.microsoft.com/fwlink/?linkid=2297915) or other license that includes premium connectors to run this flow since it uses the `Http` connection. You will be able to create the flow, but you will not be able to test it.
> When you save the flow, you will be presented with an option to sign up for a free 90-day Power Automate Premium License.

### Task 1: Create an Instant Cloud Flow

1. Go to your Microsoft365 Account:  
   [https://m365.cloud.microsoft/](https://m365.cloud.microsoft/)

2. Select **Power Automate** under **Apps**.

    ![The Power Automate app is selected.](media/power-automate-app-selection.png)

3. Select **Create** → **Instant Cloud Flow**.

    ![The Instant Cloud Flow option is selected within the Create pane.](media/create-instant-cloud-flow.png)

4. Use a **Manual Trigger** and select **Create**.

    ![The Manual Trigger option is selected and the Create button is highlighted.](media/instant-cloud-flow-manual-trigger.png)

5. Select **Manually Trigger a Flow**.
6. Select **Add an Input** → select **Text**.

    ![The manual trigger is selected and the Text input option is highlighted.](media/manual-trigger-add-input.png)

7. Enter the input name: `UserQuery`.
8. Select outside to save it.

    ![The input name is changed to UserQuery.](media/manual-trigger-add-input-name.png)

9. Select the `+` button below the `Manually trigger a flow` step and add a new **HTTP** action.
    - Enter "http" in the search bar to filter the list of actions.
    - Select the **HTTP** result that has a diamond.

    ![The plus button is highlighted, http is entered in the search box, and the HTTP result is highlighted.](media/flow-add-http-action.png)

### Task 2: Configure the HTTP action

Now, configure the HTTP action to establish a connection to the agent that you created in the previous exercise.

1. Return to Azure AI Foundry, then select **Models and Endpoints** in the left-hand menu, then select the **gpt-4o-mini** model you deployed in Exercise 1.

    ![The Models and Endpoints page is displayed with the model deployment.](media/ai-foundry-models-and-endpoints.png)

2. Copy the **URL** value for your model deployment and paste the value in the HTTP action's **URL** field.

    ![The model URL is highlight.](media/ai-foundry-model-url.png)

3. Select `POST` in the **Method** dropdown list.

    ![The Post method is selected.](media/flow-http-method.png)

4. In **Headers**, configure the following two values:
    
    1. Enter `Content-Type` for the **Key** and `application/json` for the **Value**.

    ![Add the Content-Type header value.](media/flow-http-header-content-type.png)

    2. Add another header value with `api-key` for the **Key** and paste the key value from the `gpt-4o-mini` model deployment pane in AI Foundry.

    ![The API key value in AI Foundry for the model deployment is highlighted.](media/ai-foundry-api-key.png)
    
    ![Add the API Key header value.](media/flow-http-header-api-key.png)

5. Select the **Body** field and paste the following JSON value:

     ```json
    {
      "messages": [
        {
          "role": "system",
          "content": "You are a helpful assistant that helps users find answers in PDF documents and provide concise, accurate answers."
        },
        {
          "role": "user",
          "content": "Input"
        }
      ],
      "temperature": 0.7,
      "max_tokens": 300
    }
    ```

    1. Delete the "Input" text next to the `content` property in the JSON text that you pasted, then select the **lightning icon** that appears on the right to enter data from a previous step.

    ![The lightning button is highlighted and the cursor is where "Input" used to be.](media/flow-http-body-dynamic-input-button.png)

    2. Search for `input`, then select the **UserQuery** input that you created at the end of Task 1 above:

    ![The Input item is highlighted in the search results.](media/flow-http-body-dynamic-input-result.png)

    3. The final Body value should include the dynamic **Input** value.

    ![The dynamic input value is inserted into the body.](media/flow-http-body-dynamic-input-complete.png)

### Task 3: Configure the Parse JSON action

1. After configuring the HTTP action, select the **+** button underneath the HTTP action. Search for `json` and select **Parse JSON** in the search results.

    ![The plus button, json search text, and Parse JSON action result are highlighted.](media/flow-search-parse-json.png)

2. Select the **Parse JSON** action to open its properties. Select the **Content** field, then select the **lightning icon** to choose dynamic content from a previous step.

    ![The content field and lightning icon are highlighted.](media/flow-parse-json-select-content.png)

3. Select **Body** underneath the HTTP category.

    ![The Body content option is highlighted.](media/flow-parse-json-content-body.png)

4. Paste the following JSON into the **Schema** field:
    
    ```json
    {
      "id": "chatcmpl-12345",
      "choices": [
        {
          "message": {
            "role": "assistant",
            "content": "Here is the AI response."
          }
        }
      ]
    }
    ```

    ![The JSON schema pasted within the schema field.](media/flow-parse-json-schema.png)

### Task 4: Add Send an Email action

1. After configuring the Parse JSON action, select the **+** button underneath the Parse JSON action. Search for `send email` and select **Send an Email (V2)** in the search results.

    ![The plus button, json search text, and Send an Email (V2) action result are highlighted.](media/flow-search-send-email.png)

2. Select **Sign in** to create a new connection to your Microsoft 365 email account.

    ![The sign in button is highlighted.](media/flow-send-email-sign-in.png)

3. In the email parameters, enter your email address in the **To** field, specify a **Subject**, then click in the **Body** field and select the *`fx`* button to enter dynamic content.

    ![The to, subject, and body fields are highlighted in this screenshot.](media/flow-send-email-dynamic-content.png)

4. Paste the following into the textbox, then select **Add**. This instructs PowerFlow to insert the parsed JSON output from your agent and insert it into the email body:

    ```text
    outputs('Parse_JSON')?['body']?['choices'][0]['message']['content']
    ```

    ![The dynamic content field and Add button are highlighted.](media/flow-send-email-dynamic-content-value.png)

5. The final email form should look similar to the following:

    ![The completed email form is displayed.](media/flow-send-email-configured.png)

6. Select **Save**.

    ![The save button is highlighted.](media/flow-save-button.png)

### Task 5: Manually test the flow

1. Select **Test** next to the Save button, then select **Test** inside the dialog to test the flow manually.

    ![The manual flow test dialog is displayed.](media/flow-test-manually.png)

2. Grant permission to Outlook when prompted, then select **Continue** to start the test.

    ![The run flow dialog is displayed with the granted Outlook connection.](media/flow-test-continue.png)

3. Enter your query related to the PDF uploaded to your Azure AI Foundry agent, such as `What are the three primary differences between cloth and surgical masks?`. Select **Continue** to submit the request.

    ![The test form shows the user query and the Continue button is highlighted.](media/flow-test-query.png)

4. You should receive an email with the agent's response.
    - If not, go to **Flow Runs** to troubleshoot.

5. If the manual test successfully ran, you should see the following:

    ![The flow successfully ran.](media/flow-test-success.png)

    The email you receive should look similar to the following:

    ![The email containing the agent's response is displayed.](media/flow-test-email.png)
