- [1. API Specs](#1-api-specs)
  - [1.1. Authentication API](#11-authentication-api)
  - [1.2. Get revenueue API](#12-get-revenueue-api)

# 1. API Specs
## 1.1. Authentication API
- Request:
  - Method: POST
  - Path: /auth
  - Body: JSON format
```json
    {
        "customer_id": string
        "otp": string
    }
```
- Response: 
  - Body: JSON format
    - In case OTP match:
  
```json 
{
  "version": "v2",
  "content": {
    "messages": [
      {
        "type": "text",
        "text": "Nhập OTP chính xác, bạn có thể tiếp tục nhập lại yêu cầu!"
      }
    ],
    "actions": [
      {
        "action": "set_field_value",
        "field_name": "session_key",
        "value": "xyz"
      }
    ]
  }
}
```
  - In case OTP mismatch:
  
```json 
{
  "version": "v2",
  "content": {
    "messages": [
      {
        "type": "text",
        "text": "Nhập OTP chưa chính xác, bạn có thể tiếp tục nhập lại yêu cầu!",
        "buttons": [
          {
            "type": "flow",
            "caption": "Nhập OTP",
            "target": "content20240617043132_101126"
          }
        ]
      }
    ],
    "actions": []
  }
}
```

## 1.2. Get revenueue API
- Request: 
  - Method: GET
  - Path: /revenue
  - Header: 
    - session_key: string
  - Query: 
    - customer_id: string
- Response: 
  - Body: JSON format
    - In case nornal:

```json
{ 
"version": "v2",
"content": {
    "messages": [
      {
        "type": "text",
        "text": "Doanh số của bạn là 364.323.000 VND"
      }
    ],
    "actions": []
  }
}
```

- In case session key not existed or expired 
  
``` json 
{
  "version": "v2",
  "content": {
    "messages": [
      {
        "type": "text",
        "text": "Yêu cầu nhập mã OTP để xác thực",
        "buttons": [
          {
            "type": "flow",
            "caption": "Nhập OTP",
            "target": "content20240617043132_101126"
          }
        ]
      }
    ],
    "actions": [],
    "quick_replies": []
  }
}
```
