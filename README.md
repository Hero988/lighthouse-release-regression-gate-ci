# Lighthouse Release Regression Gate — GitHub Actions template

This repository is a copy-ready GitHub Actions example for the paid
[Lighthouse Release Regression Gate](https://apify.com/hero98/lighthouse-release-regression-gate)
on Apify. It compares a current Lighthouse run with explicit baselines and fails the job
when the configured regression rules return `REGRESSION`.

The Actor costs **USD 0.05 per successfully audited URL, plus Apify platform usage**.
The included one-URL workflow sets `maxTotalChargeUsd=0.05`. Invalid, blocked, private,
robots-disallowed, or failed URLs do not create a paid event.

This is an engineering regression signal, not a WCAG conformance test, legal opinion,
usability study, or guarantee of search or performance outcomes.

## Set up the template

1. Copy `.github/workflows/lighthouse-regression.yml` into your repository.
2. Create an Apify API token and save it as a GitHub Actions repository secret named
   `APIFY_TOKEN` under **Settings -> Secrets and variables -> Actions**.
3. Replace `AUDIT_URL` with a public URL you control or have permission to audit.
4. Run the Actor once without `baselines` to obtain a snapshot, then replace the example
   baseline scores and metrics in the workflow with that snapshot.
5. Run **Lighthouse release regression** manually from the Actions tab. Once the
   thresholds are stable, attach the job to the deployment event you want to gate.

The workflow begins with `workflow_dispatch` deliberately. It does not run on a fork or
pull request by default, and GitHub should never expose the token to untrusted forked
code.

## What the workflow does

- sends the token in an authorization header, never in the URL;
- confirms that the configured public target is authorised;
- supplies explicit category-score and loading-metric baselines;
- sets tolerances for score, LCP, CLS, and TBT changes;
- caps the one-URL Actor charge at USD 0.05; and
- requires exactly one returned Dataset result with a `PASS` verdict.

The full input, output, responsible-use, and billing reference is in the
[Actor documentation](https://apify.com/hero98/lighthouse-release-regression-gate).

## Responsible use

- Test only public URLs you control or have permission to audit.
- Do not submit credentials, private dashboards, private-network hosts, or sensitive
  query strings.
- Do not weaken GitHub's secret boundary or print `APIFY_TOKEN` in workflow logs.
- Expect some measurement variation. Set tolerances from repeated runs rather than
  treating tiny score movements as release failures.

## Licence

The workflow template and repository documentation are available under the MIT Licence.
The paid Actor service and its implementation are separate and are not licensed by this
repository.
