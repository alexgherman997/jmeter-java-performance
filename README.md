# DemoQA Performance Test Suite

A comprehensive JMeter performance testing suite for the DemoQA Bookstore API, designed to test user account management and book operations under concurrent load.

## Overview

This project contains JMeter test plans that simulate realistic user interactions with the DemoQA bookstore application, including user registration, authentication, book retrieval, and account management operations.

## Test Scenarios

The test plan covers the following user workflow:

1. **User Creation** - Register new users with unique usernames
2. **User Authorization** - Authenticate users with the system
3. **Book Retrieval** - Fetch available books from the bookstore
4. **Book Management** - Add books to user's collection
5. **User Cleanup** - Delete user accounts after testing

## Test Configuration

### Thread Group Settings
- **Number of Threads (Users)**: 10 concurrent users
- **Ramp-up Period**: 0 seconds (immediate load)
- **Loop Count**: 1 iteration per user

### User Variables
- **Username**: `Mark20` (with counter for uniqueness)
- **Password**: `Mark#12345`

### API Endpoints Tested
- `POST /Account/v1/User` - User registration
- `POST /Account/v1/Authorized` - User authentication
- `GET /BookStore/v1/Books` - Retrieve book catalog
- `POST /BookStore/v1/Books` - Add books to user collection
- `DELETE /Account/v1/User/{userID}` - Delete user account

## Prerequisites

- **Apache JMeter 5.4.2** or higher
- Java 8 or higher
- Internet connection (tests run against live DemoQA API)

## Installation & Setup

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd jmeter-performance
   ```

2. **Install JMeter** (if not already installed)
   ```bash
   # Using Homebrew (macOS)
   brew install jmeter
   
   # Or download from Apache JMeter official website
   # https://jmeter.apache.org/download_jmeter.cgi
   ```

3. **Verify JMeter installation**
   ```bash
   jmeter --version
   ```

## Running the Tests

### GUI Mode 

1. **Navigate to Apache JMeter installation directory**
   ```bash
   cd /path/to/apache-jmeter/bin
   ```

2. **Launch JMeter GUI**
   ```bash
   ./jmeter
   ```

3. **Open the test plan**
   - In the JMeter GUI, go to File → Open
   - Navigate to and select `DemoQA-Performance-Test-Plan.jmx`

Alternatively, you can open the test plan directly from command line:

## Test Results & Reports

The test plan includes built-in listeners:
- **View Results Tree** - Detailed request/response data
- **Summary Report** - Aggregated performance metrics

### Key Performance Metrics
- Response times (min, max, average)
- Throughput (requests per second)
- Error percentage
- 90th/95th/99th percentile response times

## Test Plan Components

### HTTP Samplers
- **Create User**: POST request with JSON payload
- **Authorize User**: Authentication endpoint
- **Get Books**: Retrieve book catalog
- **Add Books**: Add specific books to user collection
- **Delete User**: Cleanup user account

### Assertions
- HTTP response code validation (200, 201, 204)
- Response content verification

### Processors
- **JSR223 PostProcessor**: Extract userID from create user response
- **Counter Function**: Generate unique usernames

### Headers
- `Accept: */*`
- `Content-Type: application/json`
- `Cache-control: application/json`

## Customization

### Modifying Load Parameters
Edit the Thread Group properties in the JMX file:
```xml
<stringProp name="ThreadGroup.num_threads">10</stringProp>    <!-- Number of users -->
<stringProp name="ThreadGroup.ramp_time">0</stringProp>      <!-- Ramp-up time -->
<stringProp name="LoopController.loops">1</stringProp>       <!-- Loop count -->
```

### Updating Test Data
Modify user credentials in the Test Plan variables:
```xml
<stringProp name="Argument.value">Mark20</stringProp>        <!-- Username -->
<stringProp name="Argument.value">Mark#12345</stringProp>    <!-- Password -->
```

### Adding New Test Steps
1. Right-click on Thread Group
2. Add → Sampler → HTTP Request
3. Configure endpoint details
4. Add assertions and processors as needed

## Troubleshooting

### Common Issues
1. **Connection timeouts**: Check internet connectivity and DemoQA service status
2. **Authentication failures**: Verify username/password combination
3. **Rate limiting**: Reduce thread count if getting 429 responses

### Debug Mode
Run with GUI mode and enable "View Results Tree" to inspect:
- Request headers and body
- Response data
- Assertion results

## Best Practices

1. **Always run performance tests in non-GUI mode** for accurate results
2. **Use meaningful test data** that represents real user scenarios  
3. **Monitor system resources** during test execution
4. **Set appropriate timeouts** for network operations
5. **Clean up test data** after test completion

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## References

- [Apache JMeter Documentation](https://jmeter.apache.org/usermanual/index.html)
- [DemoQA API Documentation](https://demoqa.com/)
- [JMeter Best Practices](https://jmeter.apache.org/usermanual/best-practices.html)

---

**Note**: This test suite is designed for educational and testing purposes. Ensure you have proper authorization before running performance tests against any production systems.
