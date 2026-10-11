## Summary

<!-- What does this PR change, and why? Link the issue it closes: "Closes #123". -->

## Type of change

- [ ] Bug fix (non-breaking)
- [ ] New feature (non-breaking)
- [ ] Breaking change
- [ ] Documentation only
- [ ] Refactor / chores / CI

## Scope

VaultRAG Lite is intentionally small. Please confirm this PR fits the Lite edition:

- [ ] It keeps Lite **fully local** - no new outbound network calls, no telemetry, no cloud API
- [ ] It does not add heavyweight dependencies without a strong reason
- [ ] It does not reimplement a feature listed as *Enterprise-only* in the README (those PRs will be closed politely)

## How was this tested?

<!-- Commands you ran, models used (e.g. qwen2.5:7b), sample documents (non-confidential!). -->

- [ ] `docker compose up -d --build` in `src_lite/` works end to end
- [ ] Uploaded a file and got a sensible answer
- [ ] Checked `docker compose logs` for new warnings or errors

## Checklist

- [ ] My code follows the style of the surrounding code (type hints, small functions, no dead code)
- [ ] I updated the README / docs where behaviour or configuration changed
- [ ] I added or updated pinned versions in `requirements.txt` only if needed
- [ ] I did not commit secrets, `.env` files, documents, or model files
- [ ] I agree that my contribution is licensed under the project's MIT License

## Screenshots / logs (optional)

<!-- UI changes: before / after. Do not include confidential data. -->
