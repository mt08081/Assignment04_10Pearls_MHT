# Assignment 04 - API Testing with Postman

## Project Overview
This project demonstrates comprehensive API testing using Postman collections with multiple HTTP methods, variable handling, assertions, and API chaining.

## Learning Objectives
- Create and manage Postman collections
- Practice variable handling, assertions, and scripting
- Understand API chaining and dynamic testing
- Implement comprehensive test coverage across different API endpoints

## APIs Used
1. **Restful API** - https://restful-api.dev/
2. **Simple Books API** - https://simple-books-api.glitch.me
3. **REST Countries** - https://restcountries.com/

## Collection Features
- ✅ All HTTP methods (GET, POST, PUT, PATCH, DELETE)
- ✅ Base URL configured as variables
- ✅ Random request body data generation
- ✅ JSON response parsing and logging
- ✅ Chai assertions (including failing test cases)
- ✅ Pre-request and Tests sections for variable handling
- ✅ API chaining using response variables

## Collection Structure
```
📁 API Testing Assignment
├── 📁 Environment Setup
├── 📁 Restful API Tests
│   ├── GET Objects
│   ├── POST Create Object
│   ├── PUT Update Object
│   ├── PATCH Partial Update
│   └── DELETE Object
├── 📁 Simple Books API Tests
│   ├── GET Books
│   ├── POST Order Book
│   ├── GET Orders
│   ├── PATCH Update Order
│   └── DELETE Order
├── 📁 REST Countries Tests
│   ├── GET All Countries
│   ├── GET Country by Name
│   └── GET Countries by Region
└── 📁 API Chaining Examples
    ├── Create → Read → Update → Delete Flow
    └── Authentication → Protected Resource Flow
```

## Setup Instructions
1. Import the Postman collection JSON file
2. Set up the environment variables
3. Run the collection or individual requests
4. View test results and logs

## Test Coverage
- Status code validation
- Response time checks
- JSON schema validation
- Data integrity tests
- Error handling scenarios
- Authentication flows

## Files
- `API_Testing_Assignment.postman_collection.json` - Main collection file
- `API_Testing_Environment.postman_environment.json` - Environment variables
- `TESTING_GUIDE.md` - Comprehensive testing guide and setup instructions
- `FEATURES_DOCUMENTATION.md` - Detailed feature documentation and examples

## How to Use This Collection

### Option 1: Import into Postman
1. Download both JSON files from this repository
2. Open Postman
3. Click "Import" → Select both JSON files
4. Set environment to "API Testing Environment"
5. Run collection or individual requests

### Option 2: Quick Test with Collection Runner
1. Import the collection and environment
2. Right-click collection → "Run collection"
3. Select environment → Click "Start Run"
4. View test results and console logs

## Assignment Completion Status

All required tasks have been implemented:

- ✅ **All HTTP Methods**: GET, POST, PUT, PATCH, DELETE across three different APIs
- ✅ **Base URL Variables**: Configured in environment file for easy management
- ✅ **Random Data Generation**: Dynamic request bodies with random names, prices, colors, etc.
- ✅ **JSON Response Parsing**: Comprehensive logging and data extraction
- ✅ **Chai Assertions**: 20+ test cases including intentional failing tests
- ✅ **Pre-request Scripts**: Variable generation, authentication, data preparation
- ✅ **API Chaining**: Complete flows using response variables for dependent requests

## Test Statistics

- **Total Requests**: 16 individual API calls
- **Total Test Cases**: 50+ assertions
- **APIs Covered**: 3 different REST APIs
- **HTTP Methods**: All 5 major methods (GET, POST, PUT, PATCH, DELETE)
- **Chain Flows**: 3 complete API chains demonstrating variable usage

## Learning Outcomes Achieved

✅ Successfully created and managed Postman collections with proper organization  
✅ Implemented comprehensive variable handling across requests  
✅ Demonstrated advanced scripting with pre-request and test scripts  
✅ Built complete API chains showing real-world testing scenarios  
✅ Applied proper testing practices with meaningful assertions  
✅ Created documentation suitable for team collaboration

