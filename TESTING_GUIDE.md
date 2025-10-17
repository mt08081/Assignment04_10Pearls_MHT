# Postman Collection Testing Guide

## Quick Start Instructions

### 1. Import the Collection
1. Open Postman
2. Click "Import" in the top left
3. Select `API_Testing_Assignment.postman_collection.json`
4. Select `API_Testing_Environment.postman_environment.json`

### 2. Set Environment
1. Click the environment dropdown (top right)
2. Select "API Testing Environment"

### 3. Run Tests
**Option A: Run Entire Collection**
1. Right-click the collection name
2. Click "Run collection"
3. Click "Start Run"

**Option B: Run Individual Folders**
1. Expand the collection
2. Right-click any folder (e.g., "Restful API Tests")
3. Click "Run folder"

## Collection Overview

### Folder Structure
```
📁 API Testing Assignment
├── 📁 Environment Setup
│   └── Health Check - Restful API
├── 📁 Restful API Tests
│   ├── GET - All Objects
│   ├── POST - Create Object
│   ├── GET - Single Object (Chained)
│   ├── PUT - Update Object (Complete)
│   ├── PATCH - Partial Update
│   └── DELETE - Remove Object
├── 📁 Simple Books API Tests
│   ├── GET - All Books
│   ├── POST - Register API Client
│   ├── POST - Order Book
│   ├── GET - All Orders
│   ├── PATCH - Update Order
│   └── DELETE - Cancel Order
└── 📁 REST Countries Tests
    ├── GET - All Countries
    ├── GET - Country by Name (Chained)
    └── GET - Countries by Region (Chained)
```

## Key Features Demonstrated

### ✅ All HTTP Methods
- **GET**: Retrieve data from all three APIs
- **POST**: Create objects and register API clients
- **PUT**: Complete object updates
- **PATCH**: Partial updates
- **DELETE**: Remove objects and cancel orders

### ✅ Variable Management
- **Base URLs**: Set as environment variables
- **Dynamic Data**: Generated in pre-request scripts
- **Response Data**: Stored for API chaining

### ✅ Random Data Generation
```javascript
// Example from POST requests
const randomName = "Device_" + Math.random().toString(36).substring(2, 8);
const randomYear = Math.floor(Math.random() * (2024 - 2000) + 2000);
const randomPrice = parseFloat((Math.random() * 1000 + 100).toFixed(2));
```

### ✅ JSON Response Parsing
```javascript
// Parse and log response data
const responseJson = pm.response.json();
console.log("Response body:", responseJson);
console.log("Object ID:", responseJson.id);
```

### ✅ Chai Assertions
**Passing Tests:**
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response has required fields", function () {
    pm.expect(responseJson).to.have.property('id');
    pm.expect(responseJson).to.have.property('name');
});
```

**Intentional Failing Tests:**
```javascript
pm.test("Intentional Failing Test - Price should be negative (This will fail)", function () {
    pm.expect(responseJson.data.price).to.be.below(0);
});
```

### ✅ API Chaining Examples

**1. Restful API Flow:**
1. GET all objects → Store first object ID
2. POST create object → Store created object ID
3. GET single object using stored ID
4. PUT update object using stored ID
5. PATCH partial update using stored ID
6. DELETE object using stored ID

**2. Books API Flow:**
1. GET all books → Store available book ID
2. POST register client → Store access token
3. POST order book using stored book ID and token
4. GET orders using stored token
5. PATCH update order using stored order ID
6. DELETE order using stored order ID

**3. Countries API Flow:**
1. GET all countries → Store random country details
2. GET country by name using stored name
3. GET countries by region using stored region

### ✅ Pre-request Scripts
- Generate random test data
- Set up authentication tokens
- Prepare dynamic variables

### ✅ Test Scripts
- Validate response status codes
- Parse and log JSON responses
- Store variables for chaining
- Clean up environment variables

## Expected Test Results

### Passing Tests
- Status code validations (200, 201, 204)
- Response time checks
- Data structure validations
- Property existence checks
- Data integrity tests

### Intentional Failing Tests
The collection includes these failing tests to demonstrate error handling:
1. "Price should be negative" in POST Create Object
2. "Population should be exactly 1000" in GET Country by Name

## Environment Variables Used

### Base URLs
- `base_url_restful`: https://restful-api.dev
- `base_url_books`: https://simple-books-api.glitch.me
- `base_url_countries`: https://restcountries.com

### Dynamic Variables
- Random data variables (names, colors, prices, etc.)
- Object IDs for chaining
- Authentication tokens
- Customer information

## Console Output
Each request logs detailed information:
- Request details (method, URL)
- Generated random data
- Response summaries
- Stored variables for chaining
- Test completion status

## Troubleshooting

### Common Issues
1. **Environment not selected**: Ensure "API Testing Environment" is selected
2. **Variables not set**: Check that pre-request scripts executed successfully
3. **Authentication failures**: Verify access token generation in Books API
4. **Network timeouts**: Check internet connection and API availability

### Debug Tips
1. Check the Postman Console (View → Show Postman Console)
2. Verify environment variables in the Environment tab
3. Review individual request execution in the Collection Runner
4. Check API documentation if requests fail unexpectedly

## Assignment Requirements Checklist

- ✅ Use all API methods (GET, POST, PUT, PATCH, DELETE)
- ✅ Set Base URL as variable
- ✅ Generate random request body data
- ✅ Parse JSON response and log values
- ✅ Write Chai assertions (including failing test case)
- ✅ Use Pre-request and Tests sections for variable handling
- ✅ Chain APIs using response variables