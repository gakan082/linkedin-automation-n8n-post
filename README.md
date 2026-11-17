# LinkedIn Content Approval Automation (n8n)

An n8n workflow template that turns an idea sent through Telegram into a LinkedIn post draft, asks for approval in Telegram, and publishes the post to LinkedIn only when it is approved.

> **Template status:** This is a sanitized, reusable workflow template. It has not been tested in a fresh n8n instance after import. You must connect your own accounts, configure the placeholders, and test it before using it. It is not a one-click installation.

## What the workflow does

1. **Telegram Trigger** receives a message containing a content idea.
2. **AI Agent** evaluates the idea and selects one.
3. **AI Agent1** drafts a LinkedIn post and returns structured output.
4. **Send message and wait for response** sends the draft to Telegram and waits for your approval or rejection.
5. **If** checks the approval result.
6. **Create a post** publishes the drafted text to LinkedIn only on the approved path.

## Requirements

- An n8n instance with the nodes used by this workflow available.
- A Telegram account and a Telegram bot created using [BotFather](https://t.me/BotFather).
- A Google Gemini API key and access to the Gemini model configured in your n8n Google Gemini credentials.
- A LinkedIn account and LinkedIn API/app access with the permissions required by the n8n LinkedIn integration to create posts.

**LinkedIn access note:** A LinkedIn account alone does not guarantee API posting access. LinkedIn app setup, product access, permissions, and the available authentication options can change. Follow the current requirements shown by LinkedIn and n8n. Do not assume every LinkedIn account can immediately authorize automated posting.

## Import the workflow

1. Download `linkedin-automation-public.json` from this repository.
2. Open your n8n instance.
3. Import the downloaded JSON as a workflow (the menu wording may vary by n8n version).
4. Open the imported workflow and configure the credentials and placeholders described below.
5. Save the workflow. Do not activate it until the credentials and Telegram trigger are configured and tested.

## Connect credentials

Create or select credentials in n8n and assign them to the corresponding nodes:

- **Google Gemini:** Connect your own Google Gemini API credential to both `Google Gemini Chat Model` and `Google Gemini Chat Model1`.
- **Telegram:** Connect your own Telegram bot credential to `Telegram Trigger` and `Send message and wait for response`.
- **LinkedIn:** Connect your own LinkedIn credential to `Create a post`. Complete any required LinkedIn authorization and permission steps.

Never paste API keys, bot tokens, OAuth client secrets, or access tokens into this repository or into screenshots. Store credentials in n8n's credential manager.

## Replace the placeholders

Search the imported workflow for these placeholder values and replace them with values belonging to your own setup:

| Placeholder | What to configure |
|---|---|
| `YOUR_TELEGRAM_CHAT_ID` | Your Telegram chat ID for the approval message. Use your own chat ID; do not publish it. |
| `YOUR_LINKEDIN_PERSON_ID` | The LinkedIn person/member identifier expected by the `Create a post` node for your authorized account. Select or enter the correct value supported by your n8n node version. |
| `11111111-1111-4111-8111-111111111111` and `22222222-2222-4222-8222-222222222222` | Sanitized placeholder webhook IDs in the exported template. Do not replace them with someone else's values. Let n8n configure/register the trigger webhook for your own instance when you configure and activate the Telegram Trigger. |

The placeholder webhook IDs are not Telegram bot tokens or complete webhook URLs. Each user must configure the trigger in their own n8n instance. Your n8n instance must be reachable by Telegram over the internet for webhook-based triggering to work. Avoid using the same Telegram bot for multiple active Telegram Trigger workflows because Telegram supports one webhook URL per bot at a time.

## Test before activating for regular use

1. Save the workflow after configuring credentials and placeholders.
2. Test the Telegram Trigger by sending a message to your bot.
3. Confirm the AI nodes produce the selected idea and LinkedIn draft.
4. Confirm the approval message arrives in Telegram.
5. Test the rejection path first and verify that it does **not** publish to LinkedIn.
6. Approve a test draft only when you are ready to publish it, then verify the post on LinkedIn.

The workflow's approval step is intended to prevent publishing unless the approval condition is true. Always test both approval and rejection paths in your own n8n environment before relying on it.

## Troubleshooting

- **Telegram Trigger does not receive messages:** Check the bot credential, webhook registration, n8n public HTTPS reachability, and whether another workflow is using the same bot webhook.
- **Telegram approval message fails:** Check the Telegram credential and the configured chat ID. Make sure the bot can message the chat.
- **Gemini node fails:** Check the API key, model availability, quota, and credential assignment on both Gemini model nodes.
- **LinkedIn publishing fails:** Check LinkedIn authorization, app/API access, required permissions, the person/member identifier, and the n8n LinkedIn node configuration.

## Privacy and security

This repository is intended to contain only a sanitized workflow template. Before making any changes or publishing updates, check that you have not added personal chat IDs, account identifiers that should remain private, API keys, bot tokens, OAuth secrets, access tokens, private webhook URLs, or execution data. Never commit your private working export with live credentials or personal configuration.

## Limitations

- This public template is not connected to the author's accounts.
- Each user must supply and configure their own credentials and IDs.
- Setup screens and API permissions may differ by n8n version, account type, and provider policy.
- The corrected JSON syntax has been checked, but this exact public template has not been imported and end-to-end tested in a fresh n8n instance.

## License

Add a license file if you want to specify the terms under which others may reuse, modify, or distribute this workflow. Without a license, do not assume others have permission to reuse it beyond rights granted by applicable law.
