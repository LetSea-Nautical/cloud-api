# LetSea

What is LetSea :3
LetSea is an Android-based mobile application that is used as a realtime tracking cargo ships. This project is part of the Bangkit 2023 Capstone Project Batch 1.

Getting Started:

In deployment the app to GCP, here is the step by step:

**1. Prequerities:**
   - NodeJS
   - NPM
   - Cloud Run

**2. How to Run It:**
   
   - Pull the project on our [Github Repo](https://github.com/LetSea-Nautical/cloud-api)
   - Open Google Cloud Platform, then run the command inside the repo directory using console to install all the node modules in package.json  
   ```
     $ npm install
   ```
   - Create connection inside the database folder and create the database from the sql we have exported.

   - Run the command below to build the docker
   ```
   docker build -t gcr.io/${PROJECT_ID}/your-name-app .
   ```
   - Then we need to push the docker image we have built, we run it with the command below
   ```
   docker push gcr.io/${PROJECT_ID}/your-name-app
   ```

   - After that, we deploy the docker image to Cloud Run
   ```
   gcloud run deploy --image gcr.io/${PROJECT_ID}/your-name-app --platform managed
   ```
## API Architecture
![Architecture of our API](https://github.com/LetSea-Nautical/cloud-api/blob/main/assets/Cloud%20Architecture.jpeg)

We have 2 main routes that can be used, those are:

1. Auth
2. Shipment

<details>
<summary>Login</summary>
<br>
REQUEST
   
```
POST http://URL/login
Content-Type: application/json
{
    "username": "ariqz",
    "password": "1231234"
}
```
RESULT

```
{
    "message": "Login succeed",
    "success": true,
    "data": [
        {
            "id_company": 1,
            "username": "ariqz",
            "password": "1231234",
            "email": "ariq@gmail.com",
            "company_name": "pelni",
            "created_at": "2023-06-15T00:58:16.166Z"
        }
    ],
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE2ODY4MjE2NjF9.1WQkxNF300mnxIm31yA4LzLq8Gb9EU8ow6Z3Umn9FAM"
}
```
</details>

<details>
<summary>Edit Password</summary>
<br>
REQUEST

```
PUT http://URL/editpassword
Content-Type: application/json
{
    "username" : "ariqz",
    "password" : "123anjay",
    "confirm_password" : "123anjay"
}
```

RESULT

```
{
    "payload": {
        "messages": "Succeed",
        "status_Code": 200,
        "datas": {
            "fieldCount": 0,
            "affectedRows": 1,
            "insertId": 0,
            "serverStatus": 2,
            "warningCount": 0,
            "message": "(Rows matched: 1  Changed: 1  Warnings: 0",
            "protocol41": true,
            "changedRows": 1
        }
    }
}
```
</details>

<details>
<summary>Logout</summary>
<br>
REQUEST

```
DELETE http://URL/logout
Content-Type: application/json
HEADERS :
TOKEN
```
RESULT

```
{
    "payload": {
        "messages": "Logout Succeed!",
        "status_Code": 200,
        "datas": null
    }
}
```
</details>

<details>
<summary>Tracking Detail</summary>
<br>
REQUEST

```
GET http://URL/shipment/trackdetail/:id
```   
RESULT
   
```
{
    "payload": {
        "messages": "Shipment Tracking",
        "status_Code": 200,
        "datas": [
            {
                "id_tracking": 1,
                "ship_name": "Kapal KEGIH",
                "mmsi": 209087000,
                "arrival_datetime": "2022-03-30 00:00:05",
                "lat": 39.84931,
                "lon": -75.30936,
                "sog": 12.7,
                "cog": 91.6,
                "arr_lat": 38.43993,
                "arr_lon": -74.71892
            }
        ]
    }
}
```
</details>

<details>
<summary>Vessel Detail</summary>
<br>
REQUEST

```
GET http://URL/shipment/ship/:id
```
RESULT

```
{
    "payload": {
        "messages": "Data of certain ship",
        "status_Code": 200,
        "datas": [
            {
                "mmsi": 24781,
                "imo": 2749875,
                "ship_name": "Kapal Kalimutu",
                "builder": "Budi Cahyadi",
                "place_build": "Riau",
                "year_build": 1998
            },
            {
                "mmsi": 209087000,
                "imo": 24722,
                "ship_name": "Kapal KEGIH",
                "builder": "Yamato",
                "place_build": "Serang",
                "year_build": 1985
            }
        ]
    }
}
```
</details>

<details>
<summary>Register Ship (Regship)</summary>
<br>
REQUEST

```
POST http://URL/regship
{
    "mmsi": "34807623",
    "id_company": "1",
    "imo" : "624876",
    "ship_name": "Yacth Kaligede",
    "builder": "Sutejo",
    "place_build": "Antartica",
    "year_build": "1885"
}
```
RESULT

```
{
    "payload": {
        "messages": "Register ship success",
        "status_Code": 200,
        "datas": {
            "fieldCount": 0,
            "affectedRows": 1,
            "insertId": 1,
            "serverStatus": 2,
            "warningCount": 0,
            "message": "",
            "protocol41": true,
            "changedRows": 0
        }
    }
}
```
</details>

<details>
<summary>Show All - Home</summary>
<br>
REQUEST

```
GET http://URL/shipment/
```
RESULT

```
{
    "payload": {
        "messages": "data berhasil diambil",
        "status_Code": 200,
        "datas": [
            {
                "mmsi": 24781,
                "id_company": 1,
                "imo": 2749875,
                "ship_name": "Kapal Kalimutu",
                "builder": "Budi Cahyadi",
                "place_build": "Riau",
                "year_build": 1998
            },
            {
                "mmsi": 12985796,
                "id_company": 5,
                "imo": 347962,
                "ship_name": "Kapal Tanah",
                "builder": "Yoasobi",
                "place_build": "Bogor",
                "year_build": 2014
            },
            {
                "mmsi": 209087000,
                "id_company": 1,
                "imo": 24722,
                "ship_name": "Kapal KEGIH",
                "builder": "Yamato",
                "place_build": "Serang",
                "year_build": 1985
            },
            {
                "mmsi": 876235235,
                "id_company": 5,
                "imo": 1232466,
                "ship_name": "Kapal Air",
                "builder": "Zutomayo",
                "place_build": "Osaka",
                "year_build": 2014
            }
        ]
    }
}
```
</details>



