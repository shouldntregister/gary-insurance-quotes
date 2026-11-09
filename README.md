# Gary insurance quotes

An [agent skill](https://agentskills.io) that lets an AI agent get real Australian insurance quotes from [Gary](https://gogary.com.au), an online insurance broker, through its MCP server.

It covers car, home and contents, landlord, professional indemnity and cyber insurance. It can also search the insurers' PDS and policy wordings, and existing customers can sign in to see their policies, claims and payments.

## Install

```bash
npx skills add shouldntregister/gary-insurance-quotes
```

The skill tells your agent how to use the connector. To add the connector itself in Claude Code:

```bash
claude mcp add --transport http gary https://api.gogary.com.au/v1/mcp
```

For Claude, ChatGPT and other apps, see [gogary.com.au/ai](https://gogary.com.au/ai).

## What your agent will and won't do

- It asks you the insurers' questions and never answers them for you.
- It shows you prices, cover and the insurers' own documents, as general information.
- It never buys for you. You check your answers and pay on Gary's website.
- It never asks for a password, a sign-in code or card details in the chat.

Getting a price sends your answers to real insurers, so only use real details. See Gary's [privacy policy](https://gogary.com.au/privacy).

## Licence

The skill text is MIT licensed. The Gary name and brand are not covered by that licence.

Gary is a trading name of Lang Broking Co Pty Ltd (ABN 61 702 374 972), a Corporate Authorised Representative (No. 1323797) of Australian Broker Network Pty Ltd (AFSL 253131). Information provided is general only and does not take your objectives, financial situation or needs into account. Read the PDS and TMD before you decide.
