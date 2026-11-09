# Gary insurance quotes

An [agent skill](https://agentskills.io) that lets an AI agent get real Australian insurance quotes from [Gary](https://gogary.com.au), an online insurance broker, through its MCP server.

It covers car, home and contents, landlord, professional indemnity and cyber insurance. It can also search the insurers' PDS and policy wordings, and existing customers can sign in to see their policies, claims and payments.

## Install

As a Claude Code plugin, which includes both the skill and the connector:

```bash
claude plugin install gary-insurance-quotes --marketplace shouldntregister/gary-insurance-quotes
```

As a skill only, for other agents:

```bash
npx skills add shouldntregister/gary-insurance-quotes
```

The skill tells your agent how to use the connector, but doesn't add it. To add the connector in Claude Code:

```bash
claude mcp add --transport http gary https://api.gogary.com.au/v1/mcp
```

For Claude, ChatGPT and other apps, see [gogary.com.au/ai](https://gogary.com.au/ai).

## What it runs and sends

This plugin contains one skill (instructions) and one remote MCP server, `https://api.gogary.com.au/v1/mcp`, which Gary runs. It has no hooks or scripts and installs no packages. The only command in it is an optional `curl` example, which calls the same server.

- **Sent to Gary:** the answers you give for a quote, and your searches of the policy wordings.
- **Sent on to insurers:** your answers go to the insurers on Gary's panel when your agent asks for a price. Some insurers keep a quote record.
- **Your account:** if you use the account tools, you sign in and approve access in your own browser. Your agent then gets a token that lasts up to 30 days, and it can see your quotes, policies, documents, claims and payments due. With your OK, it can also lodge a claim, send a change request or record a lender.

## What your agent will and won't do

- It asks you the insurers' questions and never answers them for you.
- It shows you prices, cover and the insurers' own documents, as general information.
- It never buys for you. You check your answers and pay on Gary's website.
- It never asks for a password, a sign-in code or card details in the chat.

Getting a price sends your answers to real insurers, so only use real details. See Gary's [privacy policy](https://gogary.com.au/privacy).

## Licence

The skill text is MIT licensed. The Gary name and brand are not covered by that licence.

Gary is a trading name of Lang Broking Co Pty Ltd (ABN 61 702 374 972), a Corporate Authorised Representative (No. 1323797) of Australian Broker Network Pty Ltd (AFSL 253131). Information provided is general only and does not take your objectives, financial situation or needs into account. Read the PDS and TMD before you decide.
