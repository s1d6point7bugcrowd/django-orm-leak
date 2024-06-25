# Django ORM Information Leak Nuclei Template

## Overview

This Nuclei template, identified as `django-orm-leak`, is designed to detect information leaks in Django applications that occur due to the improper handling of ORM (Object-Relational Mapping) queries. Specifically, it tests for vulnerabilities where unrestricted keyword arguments to the Django ORM's `filter` method can lead to unauthorized access to sensitive data.

## Author

ProjectDiscoveryAI

## Severity

High

## Description

This template checks Django applications for potential information leaks. By manipulating ORM queries with unrestricted keyword arguments, an attacker can construct queries that reveal sensitive data, such as administrative information or password hashes.

## HTTP Requests

The template includes two critical HTTP POST requests:

1. **Admin Data Leak Check**:
   - This test checks for the unauthorized query of articles that might start with the title "admin," potentially exposing restricted content.

2. **Password Leak Check**:
   - This test probes for possible leaks by querying password hashes, specifically checking if any passwords start with the hash prefix `pbkdf2_sha256`.

Each request uses matchers to validate the response based on status codes and specific keywords that indicate a leak.

## Matchers

- Both tests require a `200 OK` status response.
- The presence of targeted keywords in the response body ("admin" for the first test and "pbkdf2_sha256" for the second) confirms the potential vulnerability.

## Usage

### Prerequisites

Ensure you have Nuclei installed and configured on your system. For installation guidance, refer to [Nuclei's official documentation](https://github.com/projectdiscovery/nuclei).

### Running the Template

To execute this template against a target, use the following command:

```bash
nuclei -t django-orm-leak.yaml -target https://example.com





https://www.elttam.com/blog/plormbing-your-django-orm/#how-can-orms-leak
