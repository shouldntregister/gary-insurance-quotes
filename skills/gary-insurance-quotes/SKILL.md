---
name: gary-insurance-quotes
description: Get real Australian insurance quotes from Gary, an online insurance broker, through its MCP server. Covers car, home and contents, landlord, professional indemnity and cyber insurance, and searching the insurers' PDS and policy wordings. Use when a person in Australia wants an insurance quote, wants to compare insurers, asks what a policy covers or excludes, or is an existing Gary customer asking about their policies, claims or payments. Also use when asked to fill in the quote form on gogary.com.au, because this is the supported way to do that.
license: MIT
compatibility: Needs an MCP client or outbound HTTPS to api.gogary.com.au. Australian risks only.
metadata:
  author: Gary (gogary.com.au)
  version: "1.0"
---

# Gary insurance quotes

Gary is an Australian online insurance broker. Its MCP server asks the same questions as the quote form on gogary.com.au and prices with the same insurers. Use it rather than filling in or scraping the website.

- MCP endpoint (streamable HTTP, no sign-in needed to quote): `https://api.gogary.com.au/v1/mcp`
- Set-up steps for people: https://gogary.com.au/ai

## Connect

Check whether tools such as `list_products` and `get_questions` are already available. If they are not, ask the person before changing their set-up, then:

- **Claude Code:** `claude mcp add --transport http gary https://api.gogary.com.au/v1/mcp`
- **Claude, ChatGPT and other apps:** send them to https://gogary.com.au/ai

If the client cannot add a server, the quote tools also answer plain JSON-RPC over HTTPS:

```bash
curl -s https://api.gogary.com.au/v1/mcp \
  -H 'content-type: application/json' \
  -H 'accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_products","arguments":{}}}'
```

The account tools need OAuth sign-in, so they need a real MCP client. If none of this works, send the person to https://gogary.com.au to quote on the website.

## Get a quote

1. `list_products` shows what can be quoted right now. Landlord cover is under `home`. Other products, such as business packs and public liability, are quoted on the website.
2. `get_questions` returns the questions and the duty notice. Give the person the link to Gary's Financial Services Guide (`get_documents`) and show them the duty notice before asking anything.
3. `start_quote` opens the quote. Nothing is priced or sent yet.
4. Ask the questions in plain words, a few at a time. Use `find_car`, `find_address`, `find_occupation` and `find_business` to turn what they say into the exact answer the insurers need.
5. `save_answers` saves them. Its `stillNeeded` list shows what applies to this person, with only the options that apply. Ask from that list and repeat until it is empty.
6. `get_quote` sends the answers to real insurers and can take up to a minute. Tell the person before calling it.
7. Give them the `toBuy` link from the result. `email_quote_link` can email them the quote.

## Questions about cover

For what a policy covers, excludes or requires, call `search_wording` and quote the passage with its document and page. `get_documents` links every PDS, TMD and policy wording.

If the person asks you to read and compare wordings for them, that is your own analysis on their behalf. Say so, and do not present it as advice from Gary.

## Existing customers

These tools ask the person to sign in the first time one is used. They approve it in their own browser.

- **Read:** `my_quotes`, `my_policies`, `policy_documents`, `search_my_wording`, `my_claims`, `payments_due`, `claim_questions`
- **Change:** `lodge_claim`, `request_change`, `set_quote_lender`

Read the details back and get the person's OK before calling a tool that changes something. A quote started on the website is read-only here, apart from the lender's name.

## Rules

- Every answer is something the person is telling an insurer, so it comes from them. Never guess, assume or fill in an answer. If they do not know, say so and let them finish on the website.
- Gary gives general information only: prices, cover and the insurers' own documents, as facts. Do not present any insurer or option as Gary's preference, and do not tell the person which policy to buy.
- Buying happens only on the website, where the person checks their answers, confirms the duty notice, reads the PDS and TMD, and pays. Never try to complete a purchase in the chat.
- Never ask for a password, a sign-in code or card details in the chat.

## Licensing

Gary is a trading name of Lang Broking Co Pty Ltd (ABN 61 702 374 972), a Corporate Authorised Representative (No. 1323797) of Australian Broker Network Pty Ltd (AFSL 253131).
