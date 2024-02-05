# OCD3 Notify Workflow

This workflow is named `Notify OCD3`. It is designed to send notifications to OCD3 about the workflow run.

## Workflow Triggers

This workflow is triggered when it is called from another workflow.

## Inputs

- `notify-ocd3`: A boolean value to decide whether to notify OCD3 or not. Default is `true`.
- `webhook-url`: The webhook URL to send the notification to. Default is `'https://openmrs-cd.mekomsolutions.net/generic-webhook-trigger/invoke'`.

## Secrets

- `OCD3_USERNAME`: Required for the workflow.
- `OCD3_PASSWORD`: Required for the workflow.

## Jobs

1. `notify`: Sends a notification to OCD3 about the status of a workflow run.

## Usage

This workflow is designed to be used as part of the CI/CD pipeline. It is triggered automatically at the end of a workflow run to send a notification to OCD3 about the run.

```yaml
name: Notify OCD3

on:
  ...
    # Triggered at the end of a workflow run

jobs:
  notify-ocd3:
    uses: mekomsolutions/shared-github-workflow/.github/workflows/ocd3-notify.yml@main
    with:
      notify-ocd3: true # Optional default value: true
      webhook-url: 'https://openmrs-cd.mekomsolutions.net/generic-webhook-trigger/invoke' # Optional default value: 'https://openmrs-cd.mekomsolutions.net/generic-webhook-trigger/invoke'
    secrets:
      OCD3_USERNAME: ${{ secrets.OCD3_USERNAME }}
      OCD3_PASSWORD: ${{ secrets.OCD3_PASSWORD }}
```

Replace `OCD3_USERNAME` and `OCD3_PASSWORD` with the credentials to access the OCD3 API. You also need to set the `OCD3_USERNAME` and `OCD3_PASSWORD` secrets in your repository settings.
