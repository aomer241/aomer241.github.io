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
           margin-top: -100px; /* Add margin to the top */
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
<script>
       // JavaScript to handle QR code scanning and changing parking spot status
       // Add your JavaScript code here
       // For example:
       function changeStatus(parkingSpotId) {
           var spot = document.getElementById(parkingSpotId);
           if (spot.classList.contains('in-use')) {
               spot.classList.remove('in-use');
           } else {
               spot.classList.add('in-use');
           }
       }
       // Function to create the parking spot div
       function createParkingSpot(spotId) {
           var spot = document.createElement('div');
           spot.className = 'parking-spot';
spot.id = spotId;
           spot.onclick = function() {
               changeStatus(spotId);
           };
           spot.innerText = spotId; // Add label to the spot
           return spot;
       }
       // Simulate adding parking spots to the map
       document.addEventListener('DOMContentLoaded', function() {
           var parkingMap = document.getElementById('parking-map');
           var columns = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J'];
           var rows = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10'];
           // Loop through columns and rows to create parking spots
           columns.forEach(function(col) {
               rows.forEach(function(row) {
                   var spotId = col + row;
                   var spot = createParkingSpot(spotId);
                   parkingMap.appendChild(spot);
               });
           });
       });
</script>
</body>
</html>
