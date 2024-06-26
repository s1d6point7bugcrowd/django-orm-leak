# Django ORM Information Leak (Enhanced) Nuclei Template

## Overview

This Nuclei template, identified as `django-orm-leak-enhanced`, is designed to identify a broader range of information leaks in Django applications stemming from improper handling of ORM (Object-Relational Mapping) queries. It extends the original `django-orm-leak` template by incorporating checks for various data types and leakage methods, including numeric, text-based, and regex pattern filters.

## Author

s1d6p01nt7

## Severity

High

## Description

This enhanced template specifically targets vulnerabilities in Django applications that could allow unauthorized access to sensitive data through ORM queries. By testing different types of data filters (numeric, text, regex), the template helps in pinpointing areas where ORM query handling might be misconfigured or too permissive, leading to potential data exposure.

## HTTP Requests

The template executes several HTTP requests to validate the security of ORM handling:

1. **Admin Interface Check**:
   - Verifies the presence of a Django administration login page to confirm that the application is built with Django.

2. **Numeric Data Leak Check**:
   - Tests for numeric-based data leaks by attempting to retrieve articles with IDs greater than a specified value.

3. **Text-based Data Leak Check**:
   - Probes for text-based data leaks by filtering articles that start with a specific title string, checking for unrestricted access to text data.

4. **Regex Pattern Leakage Check**:
   - Assesses the handling of regex patterns in queries by filtering usernames based on a complex regex pattern, observing for server errors or performance degradation indicative of potential security issues.

## Matchers

Each test is equipped with specific matchers:
- **Status codes** (e.g., 200, 500) to detect successful interactions or server errors.
- **Response body content** to identify whether the filter results include expected or sensitive data.
- **Response times** to identify potential performance issues that might suggest ReDoS vulnerabilities.

## Usage

### Prerequisites

Ensure Nuclei is installed on your system. For installation details, refer to [Nuclei's official documentation](https://github.com/projectdiscovery/nuclei).

### Running the Template

To use this template against a target, execute the following command:

```bash
nuclei -t django-orm-leak-enhanced.yaml -target https://example.com
