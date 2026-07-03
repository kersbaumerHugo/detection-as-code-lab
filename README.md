# Detection-as-Code Lab

A practical Detection Engineering lab focused on writing, validating, documenting, and versioning detection rules as code.

This project applies DevOps practices to the security detection lifecycle by using Sigma rules, Git, GitHub Actions, automated validation, sample logs, and investigation documentation.

---

## Objective

The goal of this project is to build a simple but structured Detection-as-Code workflow.

Instead of treating detection rules as isolated files, this lab treats them as code artifacts that should be:

* versioned;
* reviewed;
* validated;
* documented;
* tested;
* improved over time.

This approach helps connect Blue Team, SOC analysis, Detection Engineering, and DevOps practices.

---

## What is Detection-as-Code?

Detection-as-Code is the practice of managing security detection logic using software engineering principles.

In this model, detection rules are stored in a Git repository, reviewed through Pull Requests, validated with automated pipelines, and documented with investigation context.

This allows security teams to improve rule quality, reduce errors, track changes, and make detection logic easier to maintain.

---

## Current Project Status

Current maturity level: **Level 2 — Detection Engineering Documentation**

### Completed

* [x] Initial repository structure
* [x] Sigma detection rules
* [x] Local validation with `yamllint`
* [x] Local validation with `sigma check`
* [x] GitHub Actions CI pipeline
* [x] Rule-specific documentation
* [x] Sample logs
* [x] False positive analysis
* [x] Rule review checklist
* [x] Detection test plan

### Next Steps

* [ ] Simulate a Pull Request workflow
* [ ] Add Wazuh integration
* [ ] Create custom Wazuh rules
* [ ] Generate real alerts in a local SIEM lab
* [ ] Document evidence with screenshots
* [ ] Add a final architecture diagram

---

## Technologies Used

* Sigma
* Python
* sigma-cli
* yamllint
* Git
* GitHub
* GitHub Actions
* Markdown

---

## Repository Structure

```text
detection-as-code-lab/
├── detections/
│   └── sigma/
│       ├── linux_failed_ssh_login.yml
│       ├── windows_powershell_remote_download.yml
│       └── suspicious_dns_long_query.yml
│
├── docs/
│   ├── rules/
│   │   ├── linux_failed_ssh_login.md
│   │   ├── windows_powershell_remote_download.md
│   │   └── suspicious_dns_long_query.md
│   ├── false-positive-analysis.md
│   ├── rule-review-checklist.md
│   └── test-plan.md
│
├── tests/
│   └── sample_logs/
│       ├── linux_failed_ssh_login.log
│       ├── windows_powershell_remote_download.json
│       └── suspicious_dns_long_query.log
│
├── .github/
│   └── workflows/
│       └── detection-ci.yml
│
├── requirements.txt
└── README.md
```

---

## Implemented Detections

| Rule                                  | Log Source                 | Threat Scenario                                      | Severity | Documentation                                      | Sample Log                                                  |
| ------------------------------------- | -------------------------- | ---------------------------------------------------- | -------- | -------------------------------------------------- | ----------------------------------------------------------- |
| Linux Failed SSH Login Attempt        | Linux / SSHD               | SSH brute force or user enumeration                  | Medium   | `docs/rules/linux_failed_ssh_login.md`             | `tests/sample_logs/linux_failed_ssh_login.log`              |
| Suspicious PowerShell Remote Download | Windows / Process Creation | Remote payload download using PowerShell             | High     | `docs/rules/windows_powershell_remote_download.md` | `tests/sample_logs/windows_powershell_remote_download.json` |
| Suspicious Long DNS Query             | DNS                        | Possible DNS tunneling or encoded data in subdomains | Medium   | `docs/rules/suspicious_dns_long_query.md`          | `tests/sample_logs/suspicious_dns_long_query.log`           |

---

## Detection Engineering Workflow

This project follows a simple Detection-as-Code workflow:

1. Create or update a Sigma rule.
2. Validate YAML syntax locally.
3. Validate Sigma rule structure locally.
4. Add or update sample logs.
5. Document false positives and investigation steps.
6. Open a Pull Request.
7. Run CI/CD validation with GitHub Actions.
8. Merge only after validation passes.

The goal is to treat detection rules as maintainable engineering artifacts.

---

## CI/CD Pipeline

The project uses GitHub Actions to automatically validate detection rules.

The pipeline currently performs two checks:

1. YAML syntax validation with `yamllint`.
2. Sigma rule validation with `sigma check`.

This helps prevent broken rules, formatting issues, and invalid Sigma structure from being merged into the main branch.

---

## Local Setup

Create and activate a Python virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the project dependencies:

```bash
pip install -r requirements.txt
```

Run local validation:

```bash
yamllint detections/sigma
sigma check detections/sigma
```

---

## Documentation

This repository includes supporting documentation for the detection lifecycle.

| Document                          | Purpose                                                |
| --------------------------------- | ------------------------------------------------------ |
| `docs/false-positive-analysis.md` | Documents expected false positives and triage ideas    |
| `docs/rule-review-checklist.md`   | Defines quality criteria for reviewing detection rules |
| `docs/test-plan.md`               | Defines the current validation and testing approach    |
| `docs/rules/`                     | Contains rule-specific investigation notes             |

---

## Sample Logs

Each detection rule includes at least one sample log file.

These logs are used to document the expected behavior that each rule is designed to identify.

| Sample Log                                                  | Related Rule                          |
| ----------------------------------------------------------- | ------------------------------------- |
| `tests/sample_logs/linux_failed_ssh_login.log`              | Linux Failed SSH Login Attempt        |
| `tests/sample_logs/windows_powershell_remote_download.json` | Suspicious PowerShell Remote Download |
| `tests/sample_logs/suspicious_dns_long_query.log`           | Suspicious Long DNS Query             |

At this stage, the sample logs are static and used for documentation and manual review. Future versions may include automated test execution against these logs.

---

## Rule Review Criteria

Before a detection rule is considered complete, it should meet the following criteria:

* The rule has a clear title and description.
* The log source is properly defined.
* The detection logic is understandable.
* The severity level is documented.
* MITRE ATT&CK tags are included when applicable.
* False positives are documented.
* Investigation steps are provided.
* A sample log exists.
* The rule passes `yamllint`.
* The rule passes `sigma check`.
* The GitHub Actions pipeline passes.

---

## Current Limitations

This is an educational lab and does not yet execute detections against a live SIEM.

Current limitations:

* Sample logs are static.
* There is no real-time alert generation yet.
* There is no automated log parsing.
* There is no Wazuh integration yet.
* Correlation and thresholds are not implemented yet.
* The current rules are intentionally simple and focused on learning.

These limitations are intentional for the current stage. The next phase will focus on Wazuh integration and real alert generation.

---

## Roadmap

### Level 1 — Detection-as-Code Foundation

Completed.

* Create repository structure.
* Add initial Sigma rules.
* Add local validation.
* Add CI/CD validation with GitHub Actions.
* Document the basic project objective.

### Level 2 — Detection Engineering Documentation

Completed / in progress.

* Add rule-specific documentation.
* Add sample logs.
* Add false positive analysis.
* Add rule review checklist.
* Add detection test plan.
* Improve README structure.

### Level 3 — Wazuh Integration

Planned.

* Deploy a local Wazuh lab.
* Convert or adapt selected detections to Wazuh custom rules.
* Generate test events.
* Trigger alerts in Wazuh.
* Document results with screenshots.

### Level 4 — Portfolio-Ready Release

Planned.

* Add architecture diagram.
* Add screenshots of CI/CD validation.
* Add screenshots of Wazuh alerts.
* Write final lessons learned.
* Publish a LinkedIn post.
* Add the project to resume/portfolio.

---

## Lessons Learned

This project demonstrates how DevOps concepts can be applied to Blue Team and Detection Engineering workflows.

Main takeaways so far:

* Detection rules should be versioned and reviewed.
* Automated validation helps reduce syntax and structure errors.
* Documentation is essential for SOC investigation.
* False positives must be considered from the beginning.
* Detection Engineering benefits from repeatable and auditable workflows.

---

## Author

Created by Hugo Kersbaumer as part of a cybersecurity learning path focused on Blue Team, DevSecOps, Detection Engineering, and practical security automation.
