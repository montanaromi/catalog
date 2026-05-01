Security assessments MUST execute the following tool sequence against the locally running application on localhost:

* nmap (full-port \+ service detection)  
* wapiti or ZAP (passive crawl, ≥10 URLs)  
* nuclei (all severities)  
* ffuf (directory brute-force with the seclists raft-medium-directories wordlist)  
* sqlmap (all parameterized endpoints, \--level 3 \--risk 2\)  
* hydra (login endpoint brute-force)  
* semgrep (OWASP Top Ten config plus the language-appropriate community config for the detected stack)  
* ecosystem dependency audit tool matching the project's package manager (npm audit, pip-audit, retire-net, or equivalent)

All findings MUST be documented in \<repo-root\>/security/results/{DATE}.md as a table with columns:

* ID  
* Tool  
* Severity  
* Title  
* Affected Component  
* Description  
* Reproduction Steps  
* Recommendation

Severity MUST be classified via CVSS v3.1.

The following results MUST also be included in \<repo-root\>/security. Each result set should append the date and newly generated results should NOT replace existing results from previous dates.

* \<repo-root\>/security/{tool}/{DATE}.md contains one non-empty output folder with a file per tool  
* \<repo-root\>/security/results/{DATE}.md exists with all findings severity-classified  
* Zero Critical findings trigger after remediation  
* The project's test or build gate passes clean

Scope: scanning is strictly confined to localhost — production hosts, external endpoints, and cloud services are explicitly excluded.

