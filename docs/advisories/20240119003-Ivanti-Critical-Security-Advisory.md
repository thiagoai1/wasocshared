# Ivanti EPMM and MobileIron Core added to CISA Known Exploited Catalog - 20240119003

## Overview

Ivanti have released a critical security advisory relating to a vulnerability impacting Ivanti Endpoint Manager Mobile (EPMM) and MobileIron Core. The risk of exploitation depends on the individual customer’s configurations.

## What is vulnerable?

| Product(s) Affected                                     | CVE                                                                             | Severity     | CVSS |
| ------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------ | ---- |
| Ivanti Endpoint Manager Mobile (EPMM) 11.8, 11.9, 11.10 | [CVE-2023-35082](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-35082) | **Critical** | 10   |
| MobileIron Core 11.7 and below                          | [CVE-2023-35082](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-35082) | **Critical** | 10   |

## What has been observed?

CISA added this vulnerabilty in their [Known Exploited Vulnerabilties](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) catalog. There is no evidence of exploitation affecting Western Australian Government networks at the time of publishing.

## Recommendation

The WA SOC recommends administrators apply the solutions as per vendor instructions to all affected devices within expected timeframe of *48 Hours...* (refer [Patch Management](../guidelines/patch-management.md)):

- <https://forums.ivanti.com/s/article/CVE-2023-35082-Remote-Unauthenticated-API-Access-Vulnerability-in-MobileIron-Core-11-2-and-older?language=en_US>

### Additional Resources

- CISA "CVE-2023-35082 Detail": <https://nvd.nist.gov/vuln/detail/CVE-2023-35082>
