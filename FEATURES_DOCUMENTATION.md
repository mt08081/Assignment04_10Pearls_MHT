# API Testing Collection - Features & Examples

## Assignment Requirements Fulfillment

### 1. ✅ All HTTP Methods Used

#### GET Requests
- **Restful API**: `GET /objects` - Retrieve all objects
- **Books API**: `GET /books` - Retrieve available books
- **Countries API**: `GET /v3.1/all` - Retrieve all countries

#### POST Requests
- **Restful API**: `POST /objects` - Create new device object
- **Books API**: `POST /api-clients/` - Register API client
- **Books API**: `POST /orders` - Order a book

#### PUT Requests
- **Restful API**: `PUT /objects/{id}` - Complete object update

#### PATCH Requests
- **Restful API**: `PATCH /objects/{id}` - Partial object update
- **Books API**: `PATCH /orders/{id}` - Update order details

#### DELETE Requests
- **Restful API**: `DELETE /objects/{id}` - Remove object
- **Books API**: `DELETE /orders/{id}` - Cancel order

### 2. ✅ Base URLs as Variables

Environment variables configured:
```json
{
  "base_url_restful": "https://restful-api.dev",
  "base_url_books": "https://simple-books-api.glitch.me",
  "base_url_countries": "https://restcountries.com"
}
```

Usage in requests:
```
{{base_url_restful}}/objects
{{base_url_books}}/books
{{base_url_countries}}/v3.1/all
```

### 3. ✅ Random Request Body Data Generation

#### Device Object Creation (Restful API)
```javascript
// Pre-request Script
const randomName = "Device_" + Math.random().toString(36).substring(2, 8);
const randomYear = Math.floor(Math.random() * (2024 - 2000) + 2000);
const randomPrice = parseFloat((Math.random() * 1000 + 100).toFixed(2));
const randomColor = ["red", "blue", "green", "black", "white"][Math.floor(Math.random() * 5)];

pm.environment.set("random_name", randomName);
pm.environment.set("random_year", randomYear);
pm.environment.set("random_price", randomPrice);
pm.environment.set("random_color", randomColor);
```

#### Client Registration (Books API)
```javascript
// Pre-request Script
const randomName = "TestClient_" + Math.random().toString(36).substring(2, 8);
const randomEmail = "test_" + Math.random().toString(36).substring(2, 8) + "@example.com";

pm.environment.set("client_name", randomName);
pm.environment.set("client_email", randomEmail);
```

### 4. ✅ JSON Response Parsing & Logging

#### Object Creation Response
```javascript
// Test Script
const responseJson = pm.response.json();

console.log("Created object:", responseJson);
console.log("Object ID:", responseJson.id);
console.log("Object Name:", responseJson.name);
console.log("Created At:", responseJson.createdAt);
```

#### Books API Response
```javascript
// Test Script
const responseJson = pm.response.json();

console.log("Books response:", responseJson);
console.log("Number of books:", responseJson.length);
responseJson.forEach((book, index) => {
    console.log(`Book ${index + 1}: ${book.name} (Available: ${book.available})`);
});
```

#### Countries API Response
```javascript
// Test Script
const responseJson = pm.response.json();

console.log("Number of countries:", responseJson.length);
console.log("Sample country:", {
    name: responseJson[0].name.common,
    capital: responseJson[0].capital,
    region: responseJson[0].region,
    population: responseJson[0].population
});
```

### 5. ✅ Chai Assertions (Including Failing Tests)

#### Passing Assertions
```javascript
// Status Code Tests
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Status code is 201 for creation", function () {
    pm.response.to.have.status(201);
});

// Response Structure Tests
pm.test("Response has required fields", function () {
    pm.expect(responseJson).to.have.property('id');
    pm.expect(responseJson).to.have.property('name');
    pm.expect(responseJson).to.have.property('createdAt');
});

// Data Type Tests
pm.test("Response is an array", function () {
    pm.expect(responseJson).to.be.an('array');
});

pm.test("ID is a string", function () {
    pm.expect(responseJson.id).to.be.a('string');
});

// Performance Tests
pm.test("Response time is less than 2000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(2000);
});

// Data Validation Tests
pm.test("Created object has correct name", function () {
    pm.expect(responseJson.name).to.equal(pm.environment.get("random_name"));
});

pm.test("All countries belong to the same region", function () {
    const targetRegion = pm.environment.get("random_country_region");
    responseJson.forEach(country => {
        pm.expect(country.region).to.equal(targetRegion);
    });
});
```

#### Intentional Failing Tests
```javascript
// Demonstrating failing test cases
pm.test("Intentional Failing Test - Price should be negative (This will fail)", function () {
    pm.expect(responseJson.data.price).to.be.below(0);
});

pm.test("Intentional Failing Test - Population should be exactly 1000 (This will fail)", function () {
    pm.expect(responseJson[0].population).to.equal(1000);
});
```

### 6. ✅ Pre-request and Tests Sections for Variable Handling

#### Pre-request Script Examples
```javascript
// Generate Authentication Data
const clientName = "Client_" + Math.random().toString(36).substring(2, 8);
const clientEmail = "test_" + Math.random().toString(36).substring(2, 8) + "@example.com";

pm.environment.set("client_name", clientName);
pm.environment.set("client_email", clientEmail);

console.log("Generated client credentials:", {
    name: clientName,
    email: clientEmail
});

// Generate Product Data
const productData = {
    name: "Product_" + Math.random().toString(36).substring(2, 8),
    year: Math.floor(Math.random() * (2024 - 2020) + 2020),
    price: parseFloat((Math.random() * 1000 + 100).toFixed(2)),
    color: ["red", "blue", "green", "black", "white"][Math.floor(Math.random() * 5)]
};

Object.keys(productData).forEach(key => {
    pm.environment.set(`product_${key}`, productData[key]);
});
```

#### Test Script Variable Management
```javascript
// Store Response Data for Chaining
const responseJson = pm.response.json();

// Store object ID for subsequent requests
pm.environment.set("created_object_id", responseJson.id);
console.log("Stored object ID:", responseJson.id);

// Store authentication token
pm.environment.set("access_token", responseJson.accessToken);
console.log("Stored access token for API authentication");

// Store available book for ordering
const availableBook = responseJson.find(book => book.available === true);
if (availableBook) {
    pm.environment.set("available_book_id", availableBook.id);
    console.log("Found available book:", availableBook.name);
}

// Cleanup variables after use
pm.environment.unset("temporary_variable");
console.log("Cleaned up temporary variables");
```

### 7. ✅ API Chaining Using Response Variables

#### Chain 1: Restful API Complete CRUD Flow
```
1. GET /objects 
   → Store first_object_id
   
2. POST /objects 
   → Store created_object_id
   
3. GET /objects/{{created_object_id}} 
   → Verify creation using stored ID
   
4. PUT /objects/{{created_object_id}} 
   → Update using stored ID
   
5. PATCH /objects/{{created_object_id}} 
   → Partial update using stored ID
   
6. DELETE /objects/{{created_object_id}} 
   → Delete using stored ID
```

#### Chain 2: Books API Authentication & Ordering Flow
```
1. GET /books 
   → Store available_book_id
   
2. POST /api-clients/ 
   → Store access_token
   
3. POST /orders (using access_token + available_book_id) 
   → Store order_id
   
4. GET /orders (using access_token) 
   → List all orders
   
5. PATCH /orders/{{order_id}} (using access_token) 
   → Update order using stored ID
   
6. DELETE /orders/{{order_id}} (using access_token) 
   → Cancel order using stored ID
```

#### Chain 3: Countries API Data Discovery Flow
```
1. GET /v3.1/all 
   → Store random_country_name & random_country_region
   
2. GET /v3.1/name/{{random_country_name}} 
   → Get details using stored country name
   
3. GET /v3.1/region/{{random_country_region}} 
   → Get all countries using stored region
```

## Variable Dependencies

### Global Variables (Collection Level)
- `collection_version`: "1.0.0"

### Environment Variables (Per Test Run)

#### Base URLs
- `base_url_restful`
- `base_url_books`
- `base_url_countries`

#### Chaining Variables
- `created_object_id` (Restful API chain)
- `access_token` (Books API authentication)
- `order_id` (Books API order chain)
- `available_book_id` (Books API selection)
- `random_country_name` (Countries API chain)
- `random_country_region` (Countries API chain)

#### Dynamic Data Variables
- `random_name`, `random_year`, `random_price`, `random_color`
- `client_name`, `client_email`
- `customer_name`, `new_customer_name`
- `updated_name`, `updated_year`, `updated_price`
- `patch_color`

## Error Handling Examples

### Network Timeout Handling
```javascript
pm.test("Response time is acceptable", function () {
    pm.expect(pm.response.responseTime).to.be.below(5000);
});
```

### Authentication Error Handling
```javascript
pm.test("Authentication successful", function () {
    if (pm.response.status === 401) {
        console.error("Authentication failed - check access token");
    }
    pm.response.to.not.have.status(401);
});
```

### Data Validation Error Handling
```javascript
pm.test("Required data is present", function () {
    if (!responseJson.id) {
        console.error("Missing required field: id");
    }
    pm.expect(responseJson).to.have.property('id');
});
```

This collection demonstrates comprehensive API testing practices including all required HTTP methods, variable management, random data generation, response parsing, assertions, and API chaining techniques.