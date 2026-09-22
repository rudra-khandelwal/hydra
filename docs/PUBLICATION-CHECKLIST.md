# Public Release Checklist

This repository is private by design while research is ongoing.

Before making the repository public:

## Repository review

- [ ] Confirm intended license and upstream attribution.
- [ ] Review commit history for accidentally committed secrets.
- [ ] Search current files for passwords, tokens, cookies, API keys and private keys.
- [ ] Remove personal data and unnecessary machine-specific paths.
- [ ] Remove raw sensitive logs.
- [ ] Remove proprietary/copyrighted downloaded software.
- [ ] Review generated artifacts and build output.
- [ ] Review GitHub Actions and workflow permissions.
- [ ] Review third-party source references.

## Research review

- [ ] Separate facts from hypotheses.
- [ ] Preserve dates and attribution.
- [ ] Link findings to evidence.
- [ ] State uncertainty and alternative explanations.
- [ ] Avoid unsupported security verdicts.
- [ ] Clearly distinguish independent research from official Hydra statements.

## Final verification

- [ ] Fresh clone succeeds.
- [ ] Documentation matches the actual repository.
- [ ] Build instructions work from a clean environment.
- [ ] No secret material is present.
- [ ] Upstream provenance is clear.
