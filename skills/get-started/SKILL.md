---
name: get-started
description: First run after connecting Calfo. Checks that the Calfo account is reachable, gives a short picture of the pantry (how much is in it and what expires in the next three days), and suggests a few things to try next. Use right after Calfo is installed or connected, or when the user asks how to start using Calfo.
---

# Get started with Calfo

Calfo is a kitchen app. It tracks a household's pantry, what is about to expire, the week's meal plan and the user's nutrition goals. This setup only reads; it changes nothing in the account.

## Steps

1. Call `calfo_pantry_get` with `expiring_within_days: 3`.
   - If it fails because the user is not signed in, ask them to connect Calfo again and sign in with the account they use in the Calfo iPhone app. Calfo accounts are created in that app; if they do not have one yet, point them to https://www.calfo.app.
   - Otherwise keep the items it returns for step 3.
2. Call `calfo_pantry_get` with no filter to learn roughly how many items are in the pantry. One page is enough; do not page through everything.
3. Tell the user, in two or three sentences:
   - how many items Calfo is tracking, and
   - what expires in the next three days, soonest first. When an item has `is_estimated: true`, say its date is Calfo's estimate, not a date from the package.
   - If nothing expires soon, say so plainly.
   - If the pantry is empty, say that and suggest adding the last grocery run in one sentence.
4. Offer three short next steps the user can say, for example:
   - "What can I cook tonight with what I have?"
   - "Add the groceries I just bought: …"
   - "Plan dinners for the next three nights."

## Rules

- Do not add, change or remove anything during setup.
- Do not call `calfo_recipe_generate` here. Each call uses one of the user's daily generations.
- Pantries can be shared with a household. If items look like someone else added them, describe them as the household's pantry, not the user's purchases.
