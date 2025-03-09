# E-Commerce Application
<div align="center"><img src="https://github.com/user-attachments/assets/146e20d4-c437-4571-b980-57ee0e7c3715" alt="E-Commerce App" width="500"></div>
An e-commerce app that integrates with an accounting & HR system, serving as a portal for retail clients' customers to purchase goods and other customer needs.  

## Features
- User login & email OTP confirmation  
- Add to basket  
- Save as draft  
- Edit drafts  
- See purchase history  
- Barcode scanning
- Generate pdf receipt for transaction

and many more 

# Technologies  
Built with .NET Web Forms, and RESTful API for server-side communication.

![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)  ![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white)  ![.NET](https://img.shields.io/badge/.NET%20Framework-%235C2D91.svg?style=for-the-badge&logo=dotnet&logoColor=white)  ![REST API](https://img.shields.io/badge/RESTful%20API-%2300843e.svg?style=for-the-badge&logo=api&logoColor=white)

# Architecture

### Initiate POST / GET From Client Side
``` javascript
url: '/UserControl/ValidatePassword',
data: { userName: username, password: password },
```

### Server Side 
Server side receive request and handle the controllers located at [Contollers/UserControlControllers](https://github.com/shofwanshiddiq/ecommerce-apps/blob/main/Controllers/UserControlController.cs)
```cs
 public JsonResult ValidatePassword(string userName, string password)
```

### Send OTP To Email

```cs
using System.Net.Mail;

public JsonResult SendOtpEmail(string emailID, string userName) {
  // Generate OTP
  // Create email Body 
  // Set mail service configuration

  // Send Mail
  mailMessage.To.Add(new MailAddress(emailID));
  smtpClient.Send(mailMessage);
}
```

### Generate Login Token 
* After user successfully login, server side generate login token and save it to Http Cookie & Database
```cs
// Generate Token
string token = Guid.NewGuid().ToString();

// Save the token in the HTTP-only cookie
var cookie = new HttpCookie("userToken", token)
{
    HttpOnly = true,      // Prevent JavaScript access
    Secure = true,        // Set to true if using HTTPS
    Expires = DateTime.Now.AddHours(48)  // Cookie Expiration
};

// Save token to userlogin table
var saveTokenResult = DataBase.Instance.SaveTableCRM(_tableName, false, data, dataDetail, action, NewToken);
```

### Token Validation
* Client side to initiate token validation [here](https://github.com/shofwanshiddiq/ecommerce-apps/blob/main/ViewModels/ECommerce.js)

Server side engine

```cs
public JsonResult ValidateToken() {
 // Check with the existing token in the database
}
```

### Generate Pdf
* User can generate pdf receipt consist of their transaction detail
```javascript
// Using CDN JsPdf
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

// Initiate Content
 const { jsPDF } = window.jspdf;
 const doc = new jsPDF({
      // Pdf modelling 
 });

 // Trigger PDF download
 doc.save(`recepit_title.pdf`);
```

### Barconde Scanning
Engine for barcone scanning using html5-qrcode in  [qrScript.js](https://github.com/shofwanshiddiq/ecommerce-apps/blob/main/Pages/qrScript.js) 

* Initiate from pages
```javascript
// Initialize the Html5Qrcode
const html5Qrcode = new Html5Qrcode("reader");

 // Success callback function
const qrCodeSuccessCallback = (decodedText, decodedResult)
 if (decodedText){
   // itemId = decodedText
}
```


# API Endpoints Documentation

This document provides an overview of the API endpoints, their methods, and functionality.

## Endpoints Table

| Method     | API Endpoint            | Description             | Pages      |
|------------|-------------------------|-------------------------|------------|
| **POST**    | `/UserControl/ValidateToken`            | Token validation after login success, Initiate on every page         | All Pages  |
| **GET**   | `/UserControl/GetStoreCRM`            | Retreive data from table database       | All Pages   |
| **POST**    | `UserControl/SaveTableCRM`       | Save transaction to database      | All Pages   |
| **POST**    | `/UserControl/Logout`       | Logout     | Dashboard Page   |
| **POST** | `/UserControl/ValidatePassword`       | Username & password for user validation     | Login Page   |
| **POST**    | `/UserControl/ValidateOTP`         | Validate OTP sent to user email      | Login Page   |

### Usage Instructions
- **GET Requests**: Used for retrieving data from the server. 
- **POST Requests**: Used for creating new resources, such as adding a new  product.

# Gallery

  <img src="https://github.com/user-attachments/assets/21e9e615-1ab1-4a30-88bf-6dbbf70c78cd" alt="Image 1" style="width: 200px;">
  <img src="https://github.com/user-attachments/assets/d9d185d3-870f-411f-97d6-b1540986ed86" alt="Image 2" style="width: 200px;">
  <img src="https://github.com/user-attachments/assets/6e10feef-f404-4fb2-860c-bb628716dacc" alt="Image 3" style="width: 200px;">
  <img src="https://github.com/user-attachments/assets/3dbce7f7-f533-4839-80f1-32468c189d11" alt="Image 4" style="width: 200px;">
  <img src="https://github.com/user-attachments/assets/87f4ef49-bb9b-4bb5-8aa1-69c23cc01303" alt="Image 5" style="width: 200px;">
  <img src="https://github.com/user-attachments/assets/4f2f361f-b678-4929-ac24-7793c9448429" alt="Image 6" style="width: 200px;">
  <img src="https://github.com/user-attachments/assets/e93993ee-fd47-4a9a-bb1a-4582e21341b8" alt="Image 7" style="width: 200px;">
  <img src="https://github.com/user-attachments/assets/ce034a29-c4c0-4878-9221-0db5329a8ec0" alt="Image 7" style="width: 200px;">



