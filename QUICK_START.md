# ✅ API Testing Assignment - COMPLETED

## 🚀 Quick Start

1. **Re-import the updated files** (the Restful API URL has been fixed):
   - `API_Testing_Assignment.postman_collection.json`
   - `API_Testing_Environment.postman_environment.json`

2. **Set Environment**: Select "API Testing Environment" in Postman

3. **Run Tests**: Right-click collection → "Run collection" → "Start Run"

## ✅ Fixed Issues

**Problem**: The original environment had `https://restful-api.dev` 
**Solution**: Updated to `https://api.restful-api.dev` (the correct endpoint)

## 🎯 What You'll See When It Works

### Expected Results:
- ✅ **45+ passing tests** across 16 API requests
- ❌ **2 intentional failing tests** (for demonstration)
- 🔄 **API chaining** working perfectly
- 📊 **Console logs** showing data flow between requests

### Console Output Sample:
```
=== Starting API Test ===
Generated random data: Device_abc123, 2023, $599.99, silver
Stored created object ID: 1567
Created object: {id: "1567", name: "Device_abc123", ...}
Stored access token for API authentication
Found available book: The Russian ID: 1
Order created with ID: xyz789
=== Test Completed ===
```

## 📋 Assignment Requirements ✓

- ✅ **All HTTP Methods**: GET, POST, PUT, PATCH, DELETE
- ✅ **Base URL Variables**: `{{base_url_restful}}`, `{{base_url_books}}`, `{{base_url_countries}}`
- ✅ **Random Data Generation**: Names, prices, colors, emails dynamically created
- ✅ **JSON Response Parsing**: Complete logging and data extraction
- ✅ **Chai Assertions**: 47 test cases including intentional failures
- ✅ **Pre-request Scripts**: Variable generation and authentication
- ✅ **API Chaining**: Complete CRUD flows using response variables

## 🔗 API Flows Demonstrated

### 1. Restful API CRUD Flow:
```
GET objects → POST create → GET single → PUT update → PATCH modify → DELETE
```

### 2. Books API Authentication Flow:
```
GET books → POST register → POST order → GET orders → PATCH update → DELETE order
```

### 3. Countries API Data Discovery:
```
GET all countries → GET by name → GET by region
```

## 🏆 Ready for Submission

Your collection demonstrates professional API testing practices with:
- ✅ Comprehensive error handling
- ✅ Real-world API chaining scenarios  
- ✅ Dynamic data generation
- ✅ Proper variable management
- ✅ Complete documentation

**Status**: Assignment Complete - Ready to Submit GitHub Link! 🎉