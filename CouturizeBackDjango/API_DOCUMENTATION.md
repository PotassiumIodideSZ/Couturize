# Couturize API Documentation

## Authentication Endpoints

### 1. User Registration
- **Endpoint**: `POST /api/auth/register/`
- **Description**: Register a new user
- **Request Body**:
```json
{
  "username": "string",
  "email": "string",
  "password": "string",
  "password2": "string",
  "first_name": "string (optional)",
  "last_name": "string (optional)"
}
```
- **Success Response**: 
  - Status Code: 201 Created
  - Returns user details

### 2. User Login
- **Endpoint**: `POST /api/auth/login/`
- **Description**: Obtain JWT access and refresh tokens
- **Request Body**:
```json
{
  "username": "string",
  "password": "string"
}
```
- **Success Response**:
  - Status Code: 200 OK
  - Returns access and refresh tokens

### 3. Token Refresh
- **Endpoint**: `POST /api/auth/login/refresh/`
- **Description**: Get a new access token using refresh token
- **Request Body**:
```json
{
  "refresh": "string"
}
```
- **Success Response**:
  - Status Code: 200 OK
  - Returns new access token

### 4. Get User Details
- **Endpoint**: `GET /api/auth/user/`
- **Description**: Retrieve authenticated user's details
- **Authentication**: Bearer Token Required
- **Success Response**:
  - Status Code: 200 OK
  - Returns user profile and details

## User Profile Endpoints

### 1. Get My Profile
- **Endpoint**: `GET /api/profiles/my_profile/`
- **Description**: Retrieve current user's profile
- **Authentication**: Bearer Token Required
- **Success Response**:
  - Status Code: 200 OK
  - Returns user profile details

### 2. Update Profile Measurements
- **Endpoint**: `PATCH /api/profiles/update_measurements/`
- **Description**: Update user's body measurements
- **Authentication**: Bearer Token Required
- **Request Body**:
```json
{
  "chest": "number",
  "waist": "number", 
  "hips": "number",
  "height": "number"
}
```
- **Success Response**:
  - Status Code: 200 OK
  - Returns updated profile with detected body type

## Body Type Endpoints

### 1. List Body Types
- **Endpoint**: `GET /api/body-types/`
- **Description**: Retrieve list of body types
- **Query Parameters**:
  - `body_type_id`: Filter by specific body type ID
- **Authentication**: Optional
- **Success Response**:
  - Status Code: 200 OK
  - Returns body type(s)

### 2. Get Clothing Recommendations
- **Endpoint**: `GET /api/recommendations/`
- **Description**: Retrieve clothing recommendations
- **Query Parameters**:
  - `body_type_id`: Filter recommendations by body type
- **Authentication**: Bearer Token Required
- **Success Response**:
  - Status Code: 200 OK
  - Returns clothing recommendations

## Authentication

### JWT Token Flow
1. Register user
2. Login to receive access and refresh tokens
3. Use access token for authenticated requests
4. Use refresh token to obtain new access token when expired

## Support
For any issues or questions, please contact our support team.
skobelkin.zahar@gmail.com