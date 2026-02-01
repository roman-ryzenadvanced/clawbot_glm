# OpenClaw x Z.AI Integration Guide [ [Credit: cobrax91310 on Discord | Z.AI Community]](https://discord.com/channels/1346756824233148527/1442045587460722768/1467513064713621678)

This guide provides a structured walkthrough for setting up OpenClaw with Z.AI (GLM 4.7). Please note that this installation involves executing a remote script, which presents security considerations that you should evaluate before proceeding.

## ⚠️ Security Warning

**Important Security Notice:** The installation method requires executing a remote script directly from a URL. This is a known security risk ("curl to bash/cmd"). Only proceed if you explicitly trust the source.

## Installation & Setup

### Phase 1: Core Installation

#### 1. Open Command Line
On Windows, press `Win + R`, type `cmd`, and hit Enter.

#### 2. Execute the Bootstrap Script
Copy and paste the following command into your command prompt:

```cmd
curl -fsSL https://openclaw.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

> **Note:** This command downloads and runs a script immediately.

#### 3. Accept the Installation
The system will warn you that this is "powerful and inherently risky."
- Type **Yes** to continue.

#### 4. Network Configuration
- **Port:** 18789
- **Bind:** Loopback (127.0.0.1)
- **Tailscale:** Off

### Phase 2: Model Configuration (The Brain)

#### 1. Select Provider
When prompted for the Model/Auth provider, select **Z.AI (GLM 4.7)** from the list.

#### 2. Authenticate
- Select **API Key** as the auth method
- Enter your **Z.AI API Key** when prompted

#### 3. Confirmation
The system will confirm "Model configured" and set the default to `zai/glm-4.7`.

### Phase 3: Discord Bot Setup (The Body)

#### 1. Create the Application
- Go to the [Discord Developer Portal](https://discord.com/developers/applications)
- Click **New Application** and give it a name (e.g., OpenClaw)

#### 2. Optional Styling
- **Icon:** 1024x1024 pixels
- **Banner:** 680x240 pixels

#### 3. Generate Token
- Navigate to the **Bot** tab
- Click **Reset Token** to generate your bot token
- **CRITICAL:** Copy this token immediately. You cannot see it again. Paste this into your OpenClaw terminal when requested

### Phase 4: Configure Permissions (The Nervous System)

OpenClaw requires specific "Intents" to read chat and see users.

#### 1. Enable Privileged Gateway Intents
In the **Bot** tab, scroll down and toggle **ON** the following:
- **Presence Intent**
- **Server Members Intent**
- **Message Content Intent** (Crucial for the bot to read your questions)

#### 2. OAuth2 URL Generator
Navigate to **OAuth2 > URL Generator**:
- **Scopes:** Check `bot` and `applications.commands`
- **Bot Permissions:** Ensure you check permissions like `Read Messages/View Channels`, `Send Messages`, and `Read Message History`

### Phase 5: Activation & Testing

#### 1. Invite the Bot
- Copy the generated URL from the OAuth2 page
- Paste it into your browser, select your server, and click **Authorize**

#### 2. Channel Setup
- Create a text channel named `#openclaw`
- **Allowlist:** You may need to specify the allowed channels in the console using the format: `*/openclaw, [ChannelID]`
- *Tip:* Right-click the channel to "Copy Channel ID"

#### 3. Test the Connection
- Go to the channel and mention the bot: `@OpenClaw who r u`
- **Expected Response:** The bot should reply, acknowledging it just came online and asking for a name and personality

## Next Steps

After successful installation, you can customize your bot's personality and configure additional features as needed.

## Troubleshooting

If you encounter issues:
- Verify your API key is correctly entered
- Check that all required Discord permissions are granted
- Ensure the port 18789 is accessible and not blocked by firewall
- Confirm that Message Content Intent is enabled in your Discord application

## Contributing

Feel free to submit issues or pull requests to improve this guide.

## License

See the LICENSE file for licensing information.


⚠️ SPECIAL COMMENT: SECURITY CRITICAL
Do NOT use the default port (18789).

You noted that many hosts deploy OpenClaw on a VPS with the default port and zero additional security. You are right to be skeptical of the default config. Scrapers and script kiddies scan known default ports constantly.

The Risk: If you leave port 18789 open on a public VPS, you are effectively inviting hackers to hijack your bot interface.


The Fix: Change the port during the "Gateway port" setup step  to something random (e.g., 45912) and ensure your firewall only allows traffic from trusted IPs (or use a VPN/Tailscale).
