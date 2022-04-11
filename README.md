# Products-Management
In this project we will work feature wise. That means we pick one object like user, book, blog, etc at a time. We work through it's feature. The steps would be:
*  We create it's model.
* We build it's APIs.
* We test these APIs.
* We deploy these APIs.
* We integrate these APIs with frontend.
* We will repeat steps from Step 1 to Step 5 for each feature in this project.

> This project is divided into 4 features namely User, Product, Cart and Order. You need to work on a single feature at a time. Once that is completed as per above     mentioned steps. You will be instructed to move to next Feature.


>  In this project we are changing how we send token with a request. Instead of using a custom header key like x-api-key, you need to use Authorization header and send the JWT token as Bearer token.

> Create a group database groupXDatabase. You can clean the db you previously used and resue that.

> This time each group should have a single git branch. Coordinate amongst yourselves by ensuring every next person pulls the code last pushed by a team mate. You branch will be checked as part of the demo. Branch name should follow the naming convention project/productsManagementGroupX

> Follow the naming conventions exactly as instructed.

# FEATURE I - User

# Models

*
*   User Model

{ 
  fname:  {string, mandatory},
  
  lname:  {string, mandatory},
  
  email:  {string, mandatory, valid email, unique},
  
  profileImage:  {string, mandatory}, // s3 link
  
  phone:  {string, mandatory, unique, valid Indian mobile number}, 
  
  password:  {string, mandatory, minLen 8, maxLen 15}, // encrypted password
  
  address: {
  
    shipping: {
    
      street:  {string, mandatory},
      
      city:  {string, mandatory},
      
      pincode:  {number, mandatory}
      
    },
    
    
   billing: {
   
      street:  {string, mandatory},
      
      city:  {string, mandatory},
      
      pincode:  {number, mandatory}
    }
  },

    createdAt:  {timestamp},
    
   updatedAt:  {timestamp}
}


# User APIs
Create a user document from request body. Request body must contain image.

Upload image to S3 bucket and save it's public url in user document.

Save password in encrypted format. (use bcrypt)

Response format

On success - Return HTTP status 201. Also return the user document. The response should be a JSON object like this

On error - Return a suitable error message with a valid HTTP status code. The response should be a JSON object like this

{
    "status": true,
    "message": "User created successfully",
    
    "data": {
        "fname": "John",
        
        "lname": "Doe",
        
        "email": "johndoe@mailinator.com",
        
        "profileImage": "https://classroom-training-bucket.s3.ap-south-1.amazonaws.com/user/copernico-p_kICQCOM4s-unsplash.jpg",
        
        "phone": 9876543210,
        
        "password": "$2b$10$DpOSGb0B7cT0f6L95RnpWO2P/AtEoE6OF9diIiAEP7QrTMaV29Kmm",
        
        "address": {
            "shipping": {
                "street": "MG Road",
                
                "city": "Indore",
                
                "pincode": 452001
                
            },
            
            "billing": {
                "street": "MG Road",
                
                "city": "Indore",
                
                "pincode": 452001
                
            }
        },
        "_id": "6162876abdcb70afeeaf9cf5",
        
        "createdAt": "2021-10-10T06:25:46.051Z",
        
        "updatedAt": "2021-10-10T06:25:46.051Z",
        
        "__v": 0
    }
}

POST /login
Allow an user to login with their email and password.

On a successful login attempt return the userId and a JWT token contatining the userId, exp, iat.

NOTE: There is a slight change in response body. You should also return userId in addition to the JWT token.


Response format

On success - Return HTTP status 200 and JWT token in response body. The response should be a JSON object like this

On error - Return a suitable error message with a valid HTTP status code. The response should be a JSON object like this
