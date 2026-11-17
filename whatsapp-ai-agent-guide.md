# How to Build a WhatsApp AI Agent with Claude

A simple step by step guide to set up a WhatsApp AI agent that answers customers, qualifies leads, answers FAQs and books appointments.

**Tools you will use**

- Claude (Claude Code)
- WhatsApp Business Cloud API (Meta for Developers)
- n8n (automation)
- Google Calendar (for bookings)

---

## Step 1: Open Claude and start your project

1. **Open Claude Code.** Open Claude and go to Claude Code.
2. **Create a project folder.** In your terminal, run:

   ```bash
   mkdir whatsapp-ai-agent
   cd whatsapp-ai-agent
   code .
   ```

   The last line opens the folder in VS Code. You can skip it if you do not use VS Code.

3. **Give Claude this prompt and run it:**

   ```text
   Build me a beginner-friendly WhatsApp AI agent.

   Use:
   - WhatsApp Business Cloud
   - n8n
   - Claude

   The agent must answer customers, qualify leads, answer FAQs and book appointments.

   Explain everything step by step and do as much setup as possible for me.
   ```

4. **Let Claude guide you.** Claude should help you create:
   - WhatsApp Business Cloud setup
   - n8n workflow (ready to import)
   - Claude AI integration
   - Lead qualification flow
   - FAQ auto responses
   - Appointment booking (Google Calendar)
   - All configuration steps
   - Test messages

---

## Step 2: Tell Claude about your business

The agent can only give good answers if it knows your business well.

### 1. Prepare your information

| Detail | Example |
| --- | --- |
| Business name | Hercules Detailing |
| Website | herculesdetailing.com |
| Services | Car wash, detailing, ceramic coating |
| Prices | Basic wash $50, Full detail $150 |
| Opening hours | Mon to Sat, 9AM to 7PM |
| Location | Los Angeles, CA |
| FAQs | How long does it take? |
| Booking link | cal.com/hercules |
| Contact details | +1 323 555 0123, info@hercules.com |

### 2. Give this prompt to Claude

Fill in the brackets with your own details:

```text
Study my business and create the knowledge base for my WhatsApp AI agent.

Business name: [Your Business Name]
Website: [Your Website]
Services: [List your services]
Prices: [List your prices]
Opening hours: [Your hours]
Location: [Your location]
FAQs: [Common questions and answers]
Booking link: [Your booking link]
Contact details: [Phone, email, etc.]

The agent should answer like a professional employee.
Never invent information.
If it does not know something, ask the customer for clarification or hand the conversation to a human.
```

### 3. Claude creates your knowledge base

Claude will organize everything into a clear knowledge base file, for example `business-knowledge-base.md`, split into sections:

1. Business Info
2. Services and Prices
3. FAQs
4. Policies
5. Booking
6. Contact Details

### 4. Result

Your agent now knows your services, prices and FAQs. It can share your booking link and knows when to ask for clarification or pass the chat to a human.

---

## Step 3: Create your WhatsApp Business API

1. **Go to Meta for Developers.** Open [developers.facebook.com](https://developers.facebook.com) and log in with your Facebook account.
2. **Create a new app.** Click **My Apps**, then **Create App**, and choose **Business** as the app type.
3. **Add WhatsApp.** In your app dashboard, click **Add Product** and select **WhatsApp Business Platform**.
4. **Get a test WhatsApp number.** After you add WhatsApp, set it up. Meta gives you a free test number so you can build and test before you use your real number.
5. **Copy your API details.** From the WhatsApp **API Setup** page, copy these 3 details:
   - **Access Token**: used to send and receive messages
   - **WhatsApp Business Account ID**: your business account on Meta
   - **Phone Number ID**: for your test number (or your real number later)
6. **Keep them safe.** You will need all 3 to connect WhatsApp with n8n and Claude. Do not share them publicly.

---

## Step 4: Connect WhatsApp to n8n

1. **Open n8n.** Go to your n8n workspace and open **Workflows**.
2. **Ask Claude for the workflow.** Use this prompt:

   ```text
   Create the WhatsApp AI agent JSON workflow for n8n that handles customer support.
   ```

3. **Import the workflow.** Save Claude's output as `workflow.json`, then in n8n click **Import Workflow** (or paste the JSON straight onto the canvas). You should see nodes like **Webhook**, **WhatsApp Trigger** and **AI Agent**.
4. **Add your WhatsApp credentials.** In n8n, create a WhatsApp Business API credential and enter:
   - Access Token
   - WhatsApp Business Account ID
   - Phone Number ID

   Then click **Connect**.
5. **How the trigger works.**
   - A customer sends a WhatsApp message.
   - n8n receives the message right away.
   - Your workflow starts (for example the AI agent or support flow) and sends a reply.

---

## Step 5: Test your WhatsApp AI agent

Send these messages to your WhatsApp number and check each reply:

1. `Hi`
2. `What services do you offer?`
3. `How much does it cost?`
4. `Can I book tomorrow?`
5. `I want to speak with a human.`

**Make sure the agent:**

- understands the question
- gives the correct answer
- remembers the conversation
- books correctly
- never invents information
- knows when to call a human

If all of these pass, your WhatsApp AI agent is live and working.

---

## Helpful notes

These are not in the original images, but they will save you time:

- **The test access token expires quickly** (usually within 24 hours). For a live agent, create a permanent token with a System User in Meta Business Settings.
- **On the test number, you can only message numbers you add** to the allowed list on the API Setup page.
- **n8n needs a public URL** so Meta can send messages to it. n8n Cloud gives you one. If you host n8n yourself, you need a public https address.
- **You need a Claude API key** from the Anthropic Console for the AI Agent node in n8n.
- **Test on the test number first**, then move to your real business number once everything works.
