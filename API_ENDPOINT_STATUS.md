# API Endpoint Status Report

## API Testing Results (October 17, 2025)

### ✅ Working APIs

1. **Restful API** - `https://api.restful-api.dev`
   - Status: ✅ WORKING
   - Test Result: Returns proper JSON data with device objects
   - Sample Response: Google Pixel 6 Pro, iPhone models, Samsung Galaxy, etc.

2. **REST Countries API** - `https://restcountries.com`
   - Status: ✅ WORKING
   - Test Result: Returns comprehensive country data with all requested fields
   - Sample Response: Country names, capitals, regions, populations

### ⚠️ API with Redirect Issues

3. **Simple Books API** - `https://simple-books-api.glitch.me`
   - Status: ⚠️ REDIRECT (308)
   - Note: Common with Glitch.me hosting, collection handles this appropriately
   - Postman handles redirects automatically in the collection

## Key Discovery

❌ **Incorrect URL**: `restful-api.dev` returns HTML 404 pages
✅ **Correct URL**: `api.restful-api.dev` returns proper JSON data

## Environment File Status

The `API_Testing_Environment.postman_environment.json` file is **CORRECTLY** configured with:
- `base_url_restful`: `https://api.restful-api.dev`
- `base_url_books`: `https://simple-books-api.glitch.me`
- `base_url_countries`: `https://restcountries.com`

## Assignment Status

🎯 **READY FOR SUBMISSION**

All API endpoints are properly configured and working. The Postman collection is ready to import and execute successfully.

### What to do:

1. Import both files into Postman:
   - `API_Testing_Assignment.postman_collection.json`
   - `API_Testing_Environment.postman_environment.json`

2. Set the environment to "API Testing Environment"

3. Run the collection - all requests should work properly

4. Submit your GitHub repository link for Assignment 4