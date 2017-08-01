---
layout: post
title: A Hackers Expense Tracking (wip)
permalink: "/hackers-expense-tracking.html"
redirect_from: "/2015/06/07/a-hackers-expense-tracking-wip.html"
---

A quick and hacky way of tracking expenses.

**tl;dr**

- Buy something
- Send an email to your Gmail with a specific subject, and the transaction details in the body
- Those emails are automatically forwarded to Zapier Email Parser
- Transactions get extracted from the emails, and appended to a “transaction log” Google Sheet
- Use that transaction log in other worksheets (e.g. income vs expenses)

First of all, why have I done this?! Because this is what hackers do! There are a lot of ready-made solutions for this stuff out there, with various strengths/weaknesses. The strength of this setup is that I can control those strengths and weaknesses.

Besides, I don’t really know what I want from this…yet. I think I want [YNAB][1]-like budgeting, but not exactly what they’ve done. The easiest way for me to figure out what I actually want is to start with something simple, and grow it around experience.

There are other systems I’d like to try too (like [ledger][2]), but I’m sharing this with somebody uncomfortable with the command line.

And the final reason for hacking something together using various tools: *it’s fun!*

## How it works

Once I complete a purchase, I send emails to myself with a specific subject. A Gmail filter picks these up, hides them from my inbox, and forwards it to my Zapier Email Parser account. The Zapier Email Parser Mailbox is set up to parse `amount`, `reason`, and `tags` from the email. That parsed result gets appended to a “Transaction Log” Google Sheet, with some extra information (`timestamp`, `from email`, `from name`, etc).

## Reporting

I’ve setup a spreadsheet that has per-month breakdowns of income, estimated expenses (on things like rent, bills, groceries etc), and actual expenses. This spreadsheet uses formula and scripts to categorise expenses (per-person, per-tag, etc) from the transaction log.

With that information available, I can make smarter financial decisions, and I can feel more comfortable about making them. Based on data, I can see when I need to change my behaviour. I can project finances into the future, and then simulate changes in financial situation.

This gives me lots more power than most personal finance software, as nearly all of the solutions only look at past results, and do not help you plan for the future. I’ve now got the ability to add “features” to help me budget for the future (as I said, I want something *similar* to YNAB, but I’m not sure exactly what yet).

## Improvements

The email parsing needs improvement. It’s not always accurate, which results in me checking up on it (extra end-user work, not good). To fix this I could:

- Use an email format that simpler for the parser to understand *(That’s not good! Making the user do repetitive work that a computer should be doing.)*
- Look at different services for parsing the emails *(Not sure I’ll find a good-enough one though)*
- Write less information in the email to make the parsing simpler *(That’s not good! I want more data, not less.)*
- Use a more structured form of recording expenses *(This is the most likely solution. Perhaps throwing together a simple iOS app that has fields/inputs for each field. This will definitely solve the parsing issue–no parsing required–but feels like more work. Could be easier to extend though.)*

## Next

I’m going to try and make improvements to the expense-recording aspect of this. I’m very happy with Google Sheets as a backend for now. It’s really flexible, I love having programmatic (through formulas and scripting) access to the raw data, and it’s great for collaboration (very important, as I’m sharing this with my girlfriend).

When I make some substantial changes I’ll write about it again. I’ll also write about if it’s a complete failure.

## Notes

### Alternative input

I really like that it doesn’t involve installing an App (just use my standard email client), but I might need something with a more structured input.

I did consider SMS an input method, however, it’s got roughly the same qualities/problems as email for this.

### Zapier Email Parser Format

In case anybody else want’s to try a setup similar to mine, here’s email format I’m experimenting with:

<div class="island">
<pre>
<strong>Subject:</strong> _money

<strong>Body:</strong>

£5.60

Lunch - sandwich, fruit, popcorn

#lunch
</pre>
</div>

### The pains of UK online-banking

An article from two years ago that is (unfortunately) still pretty accurate: [http://www.thinkui.co.uk/2013/01/lloyds-tsb-a-bad-ux/][3]

[1]:	https://www.youneedabudget.com/
[2]:	http://www.ledger-cli.org/
[3]:	http://www.thinkui.co.uk/2013/01/lloyds-tsb-a-bad-ux/