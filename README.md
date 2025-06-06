# 🧾 Receipt Processor API

A Go-based RESTful API that processes digital receipts, validates input fields, and calculates reward points based on predefined business rules using a modular rules engine.

## ✨ Features

- Accepts receipt data in JSON format via API
- Validates fields like date, time, price, and description using custom rules
- Calculates reward points based on 7 well-defined conditions
- Stores receipts in memory using UUIDs
- Built with Gin framework and containerized using Docker

## 🛠 Tech Stack

- Go 1.20  
- Gin (Web Framework)  
- go-playground/validator (Input Validation)  
- google/uuid (ID Generation)  
- Docker (Containerization)

## 📮 API Endpoints

### POST `/receipts/process`

Submit a receipt for processing and validation.

#### Sample Request

```json
{
  "retailer": "Target",
  "purchaseDate": "2023-08-01",
  "purchaseTime": "14:30",
  "items": [
    {
      "shortDescription": "Mountain Dew 12PK",
      "price": "6.49"
    },
    {
      "shortDescription": "Emory Boards",
      "price": "2.49"
    }
  ],
  "total": "8.98"
}

```

### Sample Request

{
  "id": "550e8400-e29b-41d4-a716-446655440000"
}

### GET /receipts/{id}/points
Fetch the reward points for a previously submitted receipt.

### Sample Response

{
  "points": 28
}
### 🧠 Points Calculation Logic
The following rules are applied to calculate points for each receipt:

- +1 point for every alphanumeric character in the retailer name

- +50 points if the total is a round dollar amount (e.g. 20.00)

- +25 points if the total is a multiple of 0.25

- +5 points for every two items listed in the receipt

- +20% of item price (rounded up) if the trimmed description length is divisible by 3

- +6 points if the purchase day is an odd number

- +10 points if the purchase time is between 2:00 PM and 4:00 PM

### 🐳 Run Locally with Docker
# Build the Docker image
docker build -t receipt-processor .

# Run the container
docker run -p 8080:8080 receipt-processor

### 📁 Project Structure
receipt-processor/
├── main.go                  # Application entry point
├── models/
│   └── receipt.go           # Data models and validation logic
├── rules/
│   └── rules.go             # Business rules and point calculations
├── go.mod                   # Module dependencies
├── go.sum                   # Module versions
└── Dockerfile               # Multi-stage Docker build







