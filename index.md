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
            var alphaA = points[points.length-2].longitude;
            var alphaB = points[points.length-1].longitude;
            var phiA = points[points.length-2].latitude;
            var phiB = points[points.length-1].latitude;

            var delta = alphaB - alphaA ;
            var distance = Math.acos( (Math.sin(phiA) * Math.sin(phiB)) + (Math.cos(phiA) * Math.cos(phiB) * Math.cos(delta)) ) * 6378.137;
            drawDistance(distance);
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
