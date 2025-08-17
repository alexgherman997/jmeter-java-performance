# DemoQA Performance Test Suite

JMeter performance testing suite for the DemoQA Bookstore API, testing user account management and book operations.

## Overview

This project contains two JMeter test plans:
- Standard test plan with hard-coded values
- CSV data-driven test plan for parameterized testing

## Test Flow

1. User Creation → Authentication → Book Retrieval → Book Management → User Deletion

## Test Plans

### Standard Test Plan (`DemoQA-Performance-Test-Plan.jmx`)
- **Users**: 10 concurrent users
- **Variables**: Username: `Mark20` (with counter), Password: `Mark#12345`

### CSV-Driven Test Plan (`DemoQA-Performance-Test-Plan-CSV.jmx`)
- **Users**: 5 concurrent users
- **Data Source**: `data.csv` (comma-delimited)
- **Format**: `username,password` (one user per line)

## API Endpoints
- User registration: `POST /Account/v1/User` 
- Authentication: `POST /Account/v1/Authorized`
- Get books: `GET /BookStore/v1/Books`
- Add books: `POST /BookStore/v1/Books`
- Delete user: `DELETE /Account/v1/User/{userID}`

## Prerequisites

- Apache JMeter 5.4.2+
- Java 8+

## Quick Setup

```bash
# Install JMeter on macOS
brew install jmeter

# Or download from https://jmeter.apache.org/download_jmeter.cgi
```

## Running Tests

### GUI Mode
```bash
jmeter
# Open either test plan via File → Open
```

### Command Line Mode
```bash
# Standard test plan
jmeter -n -t DemoQA-Performance-Test-Plan.jmx -l results.jtl

# CSV test plan
jmeter -n -t DemoQA-Performance-Test-Plan-CSV.jmx -l csv_results.jtl
```

Note: Ensure `data.csv` is in the same directory when running the CSV test plan.

## Output & Metrics

Test plans include listeners for:
- Detailed request/response data (View Results Tree)
- Aggregated metrics (Summary Report)

Key metrics: response times, throughput, error rates

## Customizing Tests

To modify thread count or credentials:
1. Open the JMX file in JMeter
2. Adjust Thread Group properties (users, ramp-up, loops)
3. Modify user variables or update the CSV file

## CI Integration

This project uses GitHub Actions for continuous integration:

- Workflow file: `.github/workflows/jmeter-performance-tests.yml`
- Trigger: Push to main, pull requests, or manual trigger
- Process:
  1. Sets up Java 17
  2. Downloads JMeter
  3. Runs both test plans
  4. Uploads results as artifacts

Results are available in GitHub Actions as:
- `standard_results.jtl` and `csv_results.jtl`
- `jmeter_standard.log` and `jmeter_csv.log`

## References

- [Apache JMeter Documentation](https://jmeter.apache.org/usermanual/index.html)
- [DemoQA API Documentation](https://demoqa.com/)

