<script>
    let currentPoint = { 
        latitude:0, 
        longitude:0 
    };

    let points = [];


    function capture(){
        var point = {
            latitude: 0,
            longitude:0
        };

        point.latitude = currentPoint.latitude;
        point.longitude = currentPoint.longitude;

        points.push(point);
        drawPoints();

        if(points.length >=2){
            // coordonnées du point A
            var alphaA = points[points.length-2].latitude; // latitude
            var phiA = points[points.length-2].longitude; // longitude

            // coordonnées du point B
            var alphaB = points[points.length-1].latitude; // latitude 
            var phiB = points[points.length-1].longitude; // longitude
            
            // calcule de la distance
            var x = (alphaB - alphaA) * Math.cos((phiA + phiB) / 2);
            var y = phiB - phiA;
            var z = Math.sqrt(Math.pow(x, 2) + Math.pow(y, 2));
            var d = 1.852 * 60 * z;

            drawDistance(d);
        }
    }

    function reset(){
        points = [];
        drawPoints();
    }

    function remove(){
        points.pop();
        drawPoints();
    }

    function drawPoints(){
        document.getElementById('points').innerHTML = "";
        points.forEach(element => {
            document.getElementById('points').innerHTML += "latitude = " + element.latitude + " longitude = " + element.longitude + "<br>"
        });
    }

    function drawDistance(distance){
        document.getElementById('distance').innerHTML = distance + " km";
    }

    function getPosition(){
        navigator.geolocation.watchPosition(
            function(position){
                currentPoint.latitude = position.coords.latitude;
                currentPoint.longitude = position.coords.longitude;
                document.getElementById('position').innerHTML = "latitude = " + currentPoint.latitude + " longitude = " + currentPoint.longitude;
            }, 
            function(){ 
                document.getElementById('position').innerHTML = "Erreur de geolocalisation :("; 
            }, 
            {
                timeout:3000, 
                enableHighAccuracy:true, 
                maximumAge:1000
            }
        );
    }

    if("geolocation" in navigator){  
        getPosition();
    }
    else{
        document.getElementById('position').innerHTML = "la géolocalisation n'est pas disponible :(";
    }
</script>
<button onclick="capture()">Capture</button>
<button onclick="remove()">Remove</button>
<button onclick="reset()">Reset</button>
<span id="position"></span><br>
<span id="points"></span>
<span id="distance"></span>
