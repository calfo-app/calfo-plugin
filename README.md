# Calfo for Claude, Cursor and Grok Bot

The official plugin for [Calfo](https://www.calfo.app), the kitchen app that tracks what is in your pantry, what is about to expire, what you plan to cook this week and what you are trying to eat. With this plugin, your assistant can read and update your Calfo pantry, search Calfo recipes, plan meals and check your nutrition goals while you chat.

Calfo is made by Acosta Tech LLC.

## What you need

- A Calfo account. Accounts are created in the Calfo iPhone app.
- Claude Code, the Claude apps, Cursor or Grok Bot.

## Install

### Claude Code

```
claude plugin marketplace add calfo-app/calfo-plugin
claude plugin install calfo@calfo
```

Then run `/mcp`, choose **calfo** and sign in with your Calfo account. Step-by-step help: https://www.calfo.app/mcp/claude?app=claude-code

### Cursor and Grok Bot

Install Calfo from the marketplace, then sign in with your Calfo account when asked.

## How to use it

Ask in plain words, for example:

- "What's in my pantry that expires this week?"
- "What can I cook tonight with what I have?"
- "Add the groceries I just bought: eggs, spinach, two chicken breasts."
- "Plan dinners for the next three nights around what's about to expire."

The plugin includes two skills:

- **get-started** checks your connection and gives you a short picture of your pantry. It only reads.
- **plan-from-pantry** proposes meals for your empty plan slots using food that is about to expire, and adds them only after you agree.

## Tools

| Tool | Kind | What it does |
|---|---|---|
| `calfo_pantry_get` | read | Lists pantry items, optionally only what expires soon. |
| `calfo_pantry_add_items` | write | Adds items, merging into ones you already have. |
| `calfo_pantry_update_item` | write | Sets how much is left, or removes an item as used or tossed. |
| `calfo_goals_get` | read | Reads your calorie and macro targets. |
| `calfo_goals_set` | write | Updates your calorie and macro targets. |
| `calfo_recipes_search` | read | Searches Calfo recipes and your saved drafts. |
| `calfo_plan_get` | read | Reads a week's meal plan. |
| `calfo_plan_add_meal` | write | Puts a recipe in a meal slot. |
| `calfo_plan_remove_meal` | write | Removes a planned meal. |
| `calfo_recipe_generate` | write | Writes a new recipe. Uses one of your daily generations; saves nothing. |
| `calfo_recipe_save` | write | Saves a generated recipe as a private draft. |
| `calfo_recipe_delete` | write | Deletes one of your own saved drafts. |

## Your data

This plugin contains no code that runs on your computer. It only tells your assistant where Calfo's server is: `https://mcp.calfo.app/api/mcp`. The assistant talks to that server using your Calfo sign-in, and nothing is stored locally by the plugin. Calfo returns only your own account's data (and your household's, if you share a pantry). When you connect, you can choose to give the assistant read-only access. You can disconnect at any time from your assistant's connector settings.

- Privacy policy: https://www.calfo.app/privacy
- Terms: https://www.calfo.app/terms

## Support

Email support@calfo.app or visit https://www.calfo.app/support.

## License

MIT. See [LICENSE](LICENSE).
