# MaliPoPay SDK Conformance Tests

Language-agnostic test scenarios for all MaliPoPay SDKs. These JSON fixtures ensure consistent behavior across all SDK implementations.

## Structure

```
scenarios/
  payments.json    - Payment collection, disbursement, verification
  customers.json   - Customer CRUD and verification
  invoices.json    - Invoice creation and payment recording
  sms.json         - Single, bulk, and scheduled SMS
  references.json  - Banks, currencies, countries, institutions
```

## Scenario Format

Each scenario defines:

```json
{
  "name": "collect_mobile_money",
  "description": "Initiate a mobile money collection",
  "method": "POST",
  "path": "/api/v1/payment/collection",
  "headers": { "apiToken": "test-key" },
  "request_body": { ... },
  "expected_status": 200,
  "expected_response": {
    "success": true,
    "data": {
      "reference": "string",
      "amount": "number"
    }
  }
}
```

- `expected_response` values like `"string"`, `"number"`, `"array"` indicate type checks, not exact values
- `path_params` are substituted into the path (e.g., `{reference}` -> value)
- `query_params` are appended as URL query parameters

## Usage in SDKs

Each SDK should:

1. Load the scenario JSON files
2. For unit tests: mock HTTP responses matching `expected_response` and verify the SDK method produces the correct HTTP request (`method`, `path`, `headers`, `request_body`)
3. For integration tests: execute against UAT and verify `expected_status`

## SDKs

| SDK | Repository |
|-----|-----------|
| Node.js | [malipopay-node](https://github.com/Malipopay/malipopay-node) |
| Python | [malipopay-python](https://github.com/Malipopay/malipopay-python) |
| PHP | [malipopay-php](https://github.com/Malipopay/malipopay-php) |
| Java | [malipopay-java](https://github.com/Malipopay/malipopay-java) |
| .NET | [malipopay-dotnet](https://github.com/Malipopay/malipopay-dotnet) |
| Ruby | [malipopay-ruby](https://github.com/Malipopay/malipopay-ruby) |

## License

MIT - Lockwood Technology Ltd
