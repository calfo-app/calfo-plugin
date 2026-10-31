---
name: plan-from-pantry
description: Plan upcoming meals in Calfo around food that is about to expire. Reads the pantry and the week's plan, finds Calfo recipes that use the soonest-expiring items, proposes which recipe goes in which empty slot, and adds them to the plan once the user agrees. Use when the user asks to plan meals, plan dinners for the next few days, or use up what is in the pantry.
---

# Plan meals from the pantry

Goal: fill the user's empty meal slots with Calfo recipes that use up what is about to expire, without overwriting anything and without changing the pantry.

## Steps

1. **See what needs using.** Call `calfo_pantry_get` with `expiring_within_days: 5`. Note the soonest-expiring items. When `is_estimated` is true, call the date an estimate.
2. **See what is already planned.** Call `calfo_plan_get` for the current week, and again with `week_start` set to next week if the days the user asked about cross into it. Note which slots are empty. A slot in state `cooked` is a past meal, not a free slot.
3. **Find recipes.** Call `calfo_recipes_search` with `pantry_match: true` and the meal type the user asked for (`dinner` if they did not say). Add `max_time_min`, `max_calories` or `min_protein_g` only if the user asked for them. Prefer recipes that use the soonest-expiring items. If you need ingredient detail, search by the item's name with `query`.
4. **Propose, then wait.** Show a short plan: day, slot, recipe title, total time, per-serving calories and protein, and which expiring item it uses. Ask the user to confirm or swap before writing anything.
5. **Write the plan.** After the user agrees, call `calfo_plan_add_meal` once per slot with the recipe `id` from the search. Never pass `replace: true` unless the user explicitly agreed to replace that specific meal.
6. **Report.** List what was added. Say clearly that planning does not change the pantry: ingredients are deducted only when the user cooks the meal in the Calfo app.

## Rules

- If no catalog recipe fits, say so. Offer `calfo_recipe_generate` only as a choice for the user, and mention that it uses one of their daily generations.
- If `calfo_plan_get` or `calfo_plan_add_meal` reports a household plan, tell the user the change is visible to everyone in their household.
- Do not invent recipe ids or titles. Use only ids returned by `calfo_recipes_search` or `calfo_recipe_save`.
