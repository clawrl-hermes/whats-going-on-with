# Cron Job Management Patterns

## Batch Model Updates

When changing the model for all cron jobs in the pipeline (e.g., switching from owl-alpha to deepseek-v4-pro due to provider availability), update all jobs simultaneously in one call batch.

**Format:** The `cronjob` tool's `model` parameter is an object, not a string:

```python
# Correct
cronjob(action='update', job_id='<id>', model={"model": "deepseek/deepseek-v4-pro"})

# Wrong — produces "No updates provided." error
cronjob(action='update', job_id='<id>', model="deepseek/deepseek-v4-pro")
```

To add a provider pin (otherwise the current default provider is pinned at creation):
```python
cronjob(action='update', job_id='<id>', model={"model": "deepseek/deepseek-v4-pro", "provider": "openrouter"})
```

## Triggering a Failed Job After Fixing Its Model

When a cron job failed due to provider/model issues:
1. Update the model on the job via `cronjob(action='update', job_id=<id>, model={"model": "..."})`
2. Trigger the job manually: `cronjob(action='run', job_id=<id>)`
3. Verify success: `cronjob(action='list')` — check `last_status` and `last_run_at`
4. Read the output at `~/.hermes/cron/output/<job_id>/<date>.md` to see what was produced
5. Send the output to the user if they request it