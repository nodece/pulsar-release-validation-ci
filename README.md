# Pulsar Release Validation CI

GitHub Actions workflow to validate Apache Pulsar release candidates using the [pulsar-release-validation](https://github.com/lhotari/pulsar-release-validation) scripts.

## Usage

### Manual Trigger (GitHub UI)

1. Go to **Actions** tab in your repository
2. Select **Validate Pulsar Release** workflow
3. Click **Run workflow**
4. Fill in the required parameters:
   - **release_version**: Pulsar release version (e.g. `3.1.0`)
   - **candidate_number**: RC candidate number (e.g. `1`)

### API Trigger (repository_dispatch)

```bash
gh repo dispatch -R <your-org>/pulsar-release-validation-ci \
  --event-type validate-pulsar-release \
  -f release_version=3.1.0 \
  -f candidate_number=1
```

Or via curl:

```bash
curl -X POST https://api.github.com/repos/<your-org>/pulsar-release-validation-ci/dispatches \
  -H "Accept: application/vnd.github.everest+json" \
  -H "Authorization: Bearer $GITHUB_TOKEN" \
  -d '{
    "event_type": "validate-pulsar-release",
    "client_payload": {
      "release_version": "3.1.0",
      "candidate_number": "1"
    }
  }'
```

## What It Does

1. Clones the [lhotari/pulsar-release-validation](https://github.com/lhotari/pulsar-release-validation) repository
2. Executes `./scripts/validate_pulsar_release_in_docker.sh` with the provided parameters
3. Runs validation inside Docker to ensure consistent environment

## References

- [Apache Pulsar Release Validation](https://github.com/lhotari/pulsar-release-validation)
- [Apache Pulsar Release Documentation](https://pulsar.apache.org/contribute/release-guide/)
