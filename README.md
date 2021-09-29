# Netflix Clone Web Application

# This Repo Holds The Server Side Code and the description for the Admin, & Client Applications.

---

## Server Side

---

The Server Side Application is built with Node.Js/Express.Js, utilizes MongoDB for Data Persistence, and Mongo Client for retrieving data.

The server uses Crypto.Js package to secure sensitive data, and manages JWT for Session Management & enhanced Authentication.

- **There are 4 Major REST End Points:**

  - Auth

    ```jsx
    // Supported Requests

    Auth/Register - POST

    // Sample Request Body
    {
        "username":"saneel",
        "email":"daniel@sjsu.edu",
        "password":"dummypassword"
    }

    // Sample Response Value
    {
        "isAdmin": false,
        "_id": "615415d80b9d690016c3f6d8",
        "username": "saneel",
        "email": "daniel@sjsu.edu",
        "password": "U2FsdGVkX1+i+ab+wDEsisN+Zok77MCN93IOBmTC8AI=",
        "createdAt": "2021-09-29T07:29:28.813Z",
        "updatedAt": "2021-09-29T07:29:28.813Z",
        "__v": 0
    }

    Auth/Login POST

    // Sample Request Body
    {
        "email":"daniel.saneel@sjsu.edu",
        "password":"dummypassword"
    }

    // Sample Response Value
    {
        "isAdmin": true,
        "_id": "614ea7fb3ad19c7a221bd39e",
        "username": "saneel_daniel",
        "email": "daniel.saneel@sjsu.edu",
        "createdAt": "2021-09-25T04:39:23.200Z",
        "updatedAt": "2021-09-25T05:00:56.074Z",
        "__v": 0,
        "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYxNGVhN2ZiM2FkMTljN2EyMjFiZDM5ZSIsImlzQWRtaW4iOnRydWUsImlhdCI6MTYzMjkwMDY2MSwiZXhwIjoxNjMzMzMyNjYxfQ.OzRCj_2DevOPIfy-qc3I84bbFhqTWF_aplXgyd3k1zA"
    }
    ```

  - Lists

    ```jsx
    // Create New List : POST - /lists (Only Admin Access)

    // Sample Request Body
    {
        "title": "Latest Movies",
        "type":"movies",
        "genre":"Sci Fi",
        "content":["6153746289e0d100164af272","6153c6412045a900160a8c41"]
    },
    {
    		"Headers": {Admin JWT Token}
    }

    // Sample Response Value
    {
        "content": [
            "6153746289e0d100164af272",
            "6153c6412045a900160a8c41"
        ],
        "_id": "6154189c0b9d690016c3f6e1",
        "title": "Latest Movies",
        "type": "movies",
        "genre": "Sci Fi",
        "createdAt": "2021-09-29T07:41:16.405Z",
        "updatedAt": "2021-09-29T07:41:16.405Z",
        "__v": 0
    }

    // Delete List: DELETE - /list/:id (Only Admin Access)

    // Sample Request Body
    {
        "Headers":{Admin JWT}
    }

    // Sample Success Response Value
    {"The list has been delete..."}

    // Get List: GET - /lists?type="series"
    {
    	"Headers": {Authenticated User - JWT}
    }
    [
        {
            "_id": "614f00548f7e7e209806a32a",
            "title": "Most Watched Series",
            "type": "series",
            "genre": "Sci Fi",
            "content": [
                "614ec6d01c5e55c2458f782c",
                "614ec71e1c5e55c2458f782e",
                "614ec7351c5e55c2458f7830",
                "614ec74f1c5e55c2458f7832",
                "614ec7621c5e55c2458f7834"
            ],
            "createdAt": "2021-09-25T10:56:20.103Z",
            "updatedAt": "2021-09-25T10:56:20.103Z",
            "__v": 0
        },
    		.....
    		.....
    ]
    ```

  - Movies

    ```jsx
    // Create New Movie : POST - api/movies (Only Admin Access)

    // Sample Request Data
    {
        "title":"Shang Chi",
        "desc":"The First Movie starting Marvel's Phase 5",
        "img": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215655imgmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=96a894d3-372b-4ba4-9466-a23bc6a8a457",
        "imgTitle":"https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "imgSm":"https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "trailer":"https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "video":"https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "year":"2021",
        "limit":16,
        "genre":"Sci Fi",
        "isSeries":false
    },
    {
        "Headers": {Admin JWT}
    }

    // Sample Success Response Value
    {
        "isSeries": false,
        "_id": "61541c4a0b9d690016c3f6e7",
        "title": "Shang Chi - The Legend Of the 10 rings",
        "desc": "The First Movie starting Marvel's Phase 5",
        "img": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215655imgmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=96a894d3-372b-4ba4-9466-a23bc6a8a457",
        "imgTitle": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "imgSm": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "trailer": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "video": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "year": "2021",
        "limit": 16,
        "genre": "Sci Fi",
        "createdAt": "2021-09-29T07:56:58.276Z",
        "updatedAt": "2021-09-29T07:56:58.276Z",
        "__v": 0
    }

    // Update Movie: PUT - api/movies/:id (Only Admin Access)

    // Sample Request Data
    {
        "title":"Shang Chi",
        "desc":"The First Movie starting Marvel's Phase 5",
        "img": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215655imgmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=96a894d3-372b-4ba4-9466-a23bc6a8a457",
        "imgTitle":"https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "imgSm":"https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "trailer":"https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "video":"https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "year":"2021",
        "limit":16,
        "genre":"Sci Fi",
        "isSeries":false
    },
    {
        "Headers":{Admin JWT}
    }

    // Sample Success Response Value
    {
        "isSeries": false,
        "_id": "61541c4a0b9d690016c3f6e7",
        "title": "Shang Chi",
        "desc": "The First Movie starting Marvel's Phase 5",
        "img": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215655imgmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=96a894d3-372b-4ba4-9466-a23bc6a8a457",
        "imgTitle": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "imgSm": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "trailer": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "video": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
        "year": "2021",
        "limit": 16,
        "genre": "Sci Fi",
        "createdAt": "2021-09-29T07:56:58.276Z",
        "updatedAt": "2021-09-29T08:56:58.276Z",
        "__v": 0
    }

    // Delete Movie : DELETE - api/movies/:id (Only Admin Access)

    // Sample Request Data
    {
        "Headers":{Admin JWT}
    }

    // Sample Success Response
    "The movie has been deleted..."

    // Get All Movies: GET - /api/movies
    {
        "Headers": {Authenticated User - JWT Token}
    }

    // Sample Successul Response
    [
        {
            "isSeries": false,
            "_id": "61541c4a0b9d690016c3f6e7",
            "title": "Shang Chi - The Legend Of the 10 rings",
            "desc": "The First Movie starting Marvel's Phase 5",
            "img": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215655imgmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=96a894d3-372b-4ba4-9466-a23bc6a8a457",
            "imgTitle": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
            "imgSm": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
            "trailer": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
            "video": "https://firebasestorage.googleapis.com/v0/b/netflix-adminapp.appspot.com/o/items%2F1632859215675imgSmmb_shangchi-sitewide_20210903_2x.jpeg?alt=media&token=8d6cdda1-55aa-417d-bed6-402c4fb2bc4b",
            "year": "2021",
            "limit": 16,
            "genre": "Sci Fi",
            "createdAt": "2021-09-29T07:56:58.276Z",
            "updatedAt": "2021-09-29T07:56:58.276Z",
            "__v": 0
        },
    		.....
    		.....
    ]
    ```

  - Users

    ```jsx
    // Get User By ID: GET - api/users/find/614eade77311462f6c50f729

    // Sample Request Data
    {
        "Header": {Current User JWT || Admin},
    }

    // Sample Response Value
    {
        "isAdmin": false,
        "_id": "614eade77311462f6c50f729",
        "username": "stoner",
        "email": "stoner@gmail.edu",
        "createdAt": "2021-09-25T05:04:39.621Z",
        "updatedAt": "2021-09-25T05:04:39.621Z",
        "__v": 0
    }

    // Delete User By ID: DELETE - api/users/615415d80b9d690016c3f6d8

    // Sample Request Data
    {
        "Header": {Current User JWT || Admin},
    }

    // Sample Response Value
    {"User has been successfully deleted"}

    // Get USer Stats Per Month: GET - api/users/stats

    // Sample Request Data
    {
        "Header": {Admin JWT},
    }

    // Sample Response Value
    [
        {
            "_id": 9,
            "total": 3
        },
    		...
    ]
    ```

- **Currently There are 3 Major Data Models:**
  List
  ```jsx
  {
      title: { type: String, required: true, unique: true },
      type: { type: String },
      genre: { type: String },
      content:{type: Array}
    },
    { timestamps: true }
  ```
  Movie
  ```jsx
  {
      title: { type: String, required: true, unique: true },
      desc: { type: String },
      img: { type: String },
      imgTitle: { type: String },
      imgSm: { type: String },
      trailer: { type: String },
      video: { type: String },
      year: { type: String },
      limit: { type: Number },
      genre: { type: String },
      isSeries: { type: Boolean, default: false },
    },
    { timestamps: true }
  ```
  User
  ```jsx
  {
      username: { type: String, required: true, unique: true },
      email: { type: String, required: true, unique: true },
      password: { type: String, required: true },
      profilePic: { type: String, defaut: "" },
      isAdmin: { type: Boolean, default: false },
    },
    { timestamps: true }
  ```

## **Client Application**

The Client Application is built with React.JS Framework, and utilized Material UI for additional UI Components.

The App is built with several re-usable components, and manages app state using Redux and Context Providers.

Utilizes 'react-router-dom' to manage app routes.

### Major Screenshots of the Application

- Register Page:

  ![Screen Shot 2021-09-29 at 1.25.36 AM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-29_at_1.25.36_AM.png)

- Login Page

  ![Screen Shot 2021-09-29 at 1.28.28 AM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-29_at_1.28.28_AM.png)

- Home Page

  ![Screen Shot 2021-09-28 at 8.13.05 PM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-28_at_8.13.05_PM.png)

  ![Screen Shot 2021-09-28 at 8.13.26 PM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-28_at_8.13.26_PM.png)

- Movies Section

  ![Screen Shot 2021-09-28 at 8.14.04 PM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-28_at_8.14.04_PM.png)

  ![Screen Shot 2021-09-28 at 8.15.08 PM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-28_at_8.15.08_PM.png)

  Genre - Horror

- Series Section

  ![Screen Shot 2021-09-29 at 1.33.28 AM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-29_at_1.33.28_AM.png)

- Play Movie / Series
  ![Screen Shot 2021-09-28 at 8.13.51 PM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-28_at_8.13.51_PM.png)

[Client App Repo](https://github.com/SaneelDaniel/netflix_clone_clientApp)

## Admin Application

The Client Application is built with React.JS Framework, and utilized Material UI for additional UI Components.

The App is built with several re-usable components, and manages app state using Redux and Context Providers.

The App Also Handles File Upload To The Firebase Storage endpoint.

Utilizes 'react-router-dom' to manage app routes.

### Major Screenshots of the Application

- Home Page

  ![Screen Shot 2021-09-29 at 1.49.47 AM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-29_at_1.49.47_AM.png)

- List Movies

  ![Screen Shot 2021-09-29 at 1.54.34 AM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-29_at_1.54.34_AM.png)

- Add New Content

  ![Screen Shot 2021-09-29 at 1.50.35 AM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-29_at_1.50.35_AM.png)

- List Of Lists

  ![Screen Shot 2021-09-29 at 1.50.26 AM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-29_at_1.50.26_AM.png)

- Add New List
  ![Screen Shot 2021-09-29 at 1.50.49 AM.png](Netflix%20Clone%20Web%20Application%20759a6f572138433b88aa4b55b50b94d8/Screen_Shot_2021-09-29_at_1.50.49_AM.png)

[Admin App Github Repo](https://github.com/SaneelDaniel/netflix_clone_admin_app)
