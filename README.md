# aomer241.github.io

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Parking Map</title>
<style>
       /* Add your CSS styles here */
       /* For example: */
       body {
           background-color: lightblue; /* Background color of the parking lot */
           display: flex;
           flex-direction: column;
           align-items: center;
           justify-content: center;
           height: 100vh;
           margin: 0;
       }
       h1 {
           text-align: center; /* Center the heading */
           margin-top: 20px; /* Add margin to the top */
       }
       #parking-map {
           display: grid;
           grid-template-columns: repeat(10, 1fr); /* 10 columns */
           gap: 5px; /* Gap between parking spots */
           justify-content: center; /* Center the grid horizontally */
           align-items: center; /* Center the grid vertically */
       }
       .parking-spot {
           width: 30px;
           height: 30px;
           background-color: green; /* Available spot color */
           border: 1px solid #000;
           display: flex;
           justify-content: center;
           align-items: center;
           font-size: 12px;
           cursor: pointer;
       }
       .in-use {
           background-color: red; /* In use spot color */
       }
</style>
</head>
<body>
<h1>Parking Map</h1>
<div id="parking-map">
<!-- Parking spots will be dynamically added here -->
</div>
<script src="https://www.gstatic.com/firebasejs/9.6.2/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.6.2/firebase-database.js"></script>
<script>
       // Firebase configuration
       const firebaseConfig = {
           apiKey: "YOUR_API_KEY",
           authDomain: "YOUR_AUTH_DOMAIN",
           projectId: "YOUR_PROJECT_ID",
           storageBucket: "YOUR_STORAGE_BUCKET",
           messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
           appId: "YOUR_APP_ID"
       };
       // Initialize Firebase
       firebase.initializeApp(firebaseConfig);
       const database = firebase.database();
       // Function to handle changes in parking spot status
       function handleSpotStatusChange(snapshot) {
           const spotId = snapshot.key;
           const spot = document.getElementById(spotId);
           const isSpotInUse = snapshot.val();
           spot.classList.toggle('in-use', isSpotInUse);
       }
       // Function to create the parking spot div
       function createParkingSpot(spotId) {
           const spot = document.createElement('div');
           spot.className = 'parking-spot';
spot.id = spotId;
           spot.onclick = function() {
               database.ref('parking/' + spotId).set(spot.classList.contains('in-use') ? false : true);
           };
           spot.innerText = spotId; // Add label to the spot
           return spot;
       }
       // Simulate adding parking spots to the map
       document.addEventListener('DOMContentLoaded', function() {
           const parkingMap = document.getElementById('parking-map');
           const columns = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J'];
           const rows = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10'];
           // Loop through columns and rows to create parking spots
           columns.forEach(function(col) {
               rows.forEach(function(row) {
                   const spotId = col + row;
                   const spot = createParkingSpot(spotId);
                   parkingMap.appendChild(spot);
                   // Listen for changes in parking spot status
                   database.ref('parking/' + spotId).on('value', handleSpotStatusChange);
               });
           });
       });
</script>
</body>
</html>
