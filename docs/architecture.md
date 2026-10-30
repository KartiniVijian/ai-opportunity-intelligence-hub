# Architecture and design notes

## Processing stages

1. **Discovery:** manual or six-hour schedule starts a run.
2. **Source fan-out:** source registry emits one item per configured RSS feed.
3. **Collection:** RSS reader retrieves entries; feed-level errors continue without stopping other sources.
4. **Normalization:** records are converted into a stable internal shape.
5. **Deduplication:** normalized URLs are checked against a rolling 30-day static-data index.
6. **Enrichment:** an LLM returns structured metadata. Source content is treated as untrusted.
7. **Validation:** malformed JSON fails; numeric values are clamped.
8. **Scoring:** weighted score is calculated in code, outside the model.
9. **Routing:** high-priority records alert Slack; others enter a bounded review queue.
10. **Operations:** a separate Error Trigger workflow sends a failure notification.

## Trust boundaries

RSS content is untrusted. The system prompt tells the model not to follow instructions embedded in article content. Deterministic code validates fields and calculates the final score. Human verification remains required before acting on eligibility or deadlines.

## Production considerations

Replace static workflow data with PostgreSQL and a unique URL hash for durable deduplication and queueing. Add retries, dead-letter handling, persistence, rate limits, and monitoring.
