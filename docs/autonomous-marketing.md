# Rankavi in Autonomous Marketing Workflows

"Autonomous marketing" describes AI agents that run multi-step marketing tasks, content distribution, campaign execution, brand visibility work, with reduced day-to-day human oversight. It's an actively used term in 2026 marketing tooling, though the category is still forming rather than fully standardized.

## Where brand mentions fit

Traditional marketing automation focuses on email sequences, ad spend, and social scheduling. A growing part of the category is visibility work aimed specifically at AI answer engines (ChatGPT, Perplexity, Google AI Overviews), since these increasingly sit between a business and its next customer. Rankavi's API is built for that layer: placing real, unlinked brand mentions across relevant sites so an autonomous marketing pipeline can request mention coverage the same way it might request an ad campaign or a content push.

## A simple automated pattern

An agent or scheduled job can:

1. Call `GET /categories` to confirm the right category for a brand's industry.
2. Call `POST /mentions` with the brand name, category, and target URL whenever new mention capacity is needed.
3. Track `order.status` and `order.credits_used` from the response to manage a mention budget programmatically.

Because both endpoints return structured JSON and never require manual form-filling, they can be wired directly into a larger marketing automation stack, a cron job, or an agent's own tool-calling loop, without a human placing each order by hand.

## What this is not

Rankavi's API does not itself make marketing decisions, choose target sites autonomously on your behalf beyond category targeting, or write ad copy. It is a single, well-defined action, submit or check a mention order, meant to be one tool among several inside a broader autonomous marketing setup.
