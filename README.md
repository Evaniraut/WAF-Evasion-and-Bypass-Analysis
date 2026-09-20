# WAF Evasion and Bypass Analysis

A web application security project evaluating the effectiveness of a Web Application Firewall (WAF) against **Cross-Site Scripting (XSS)** and **Server-Side Request Forgery (SSRF)** attacks in a controlled OWASP Juice Shop environment.

The project demonstrates how baseline malicious requests can be detected and blocked by signature-based filtering, while modified payloads and alternative URL representations can bypass those protections.

## Project Overview

The testing followed a structured security assessment process:

- Reconnaissance and application mapping
- Input and endpoint discovery
- Baseline vulnerability testing
- XSS vulnerability validation
- SSRF vulnerability validation
- WAF detection and blocking tests
- WAF evasion testing
- Post-exploitation impact analysis
- Mitigation analysis

All testing was performed in a controlled local lab environment.

## Key Findings

### XSS Testing

A standard script-tag payload was initially tested against the application and did not execute.

A modified event-handler payload successfully demonstrated XSS execution.

When requests were routed through the WAF, known XSS patterns were blocked with an HTTP `403 Forbidden` response.

Further testing demonstrated that an adapted payload could bypass the WAF's signature-based filtering and execute successfully in the application.

### SSRF Testing

SSRF behavior was validated by supplying a local server URL through the application's profile image URL functionality and observing the resulting server-side request.

The WAF successfully blocked requests containing the literal localhost address:

`127.0.0.1`

However, testing showed that an alternative numeric representation of localhost could bypass the filter while still resolving to the same internal host.

The bypass was subsequently used in the controlled environment to demonstrate access to an internal-only service.

## Tools & Environment

- Kali Linux
- OWASP Juice Shop
- Python HTTP Server
- Browser Developer Tools
- Chrome / Firefox
- Local WAF proxy

## Security Concepts Demonstrated

- Web Application Firewall (WAF) testing
- Cross-Site Scripting (XSS)
- Server-Side Request Forgery (SSRF)
- Signature-based filtering
- Payload adaptation
- Input validation
- WAF evasion
- HTTP request/response analysis
- Internal service access testing
- Layered security controls

## Documentation

### Full Documentation

[`Documentation.pdf`](./Documentation.pdf)

Complete project documentation covering the methodology, testing process, findings, analysis, mitigation strategies, and conclusions.

### Attack Demonstration

[Attack Demonstration.pdf](./Attack%20Demonstration.pdf)

Focused practical demonstration containing the reconnaissance, vulnerability validation, WAF blocking tests, XSS and SSRF bypass testing, and post-exploitation evidence.

## Key Takeaway

The testing demonstrated that signature-based WAF rules can successfully block known attack patterns but may be bypassed when equivalent malicious input is represented differently.

The results highlight the importance of combining WAF protection with secure input handling, validation, normalization, application-level security controls, and defense-in-depth.

## Disclaimer

This project was conducted exclusively in a controlled local lab environment for cybersecurity education and security testing. No unauthorized systems or third-party infrastructure were targeted.
