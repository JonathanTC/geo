<script>
    let currentPoint = [ 0, 0 ];
    let points = [];

    function capture(){
        points.push(currentPoint);
        drawPoints();
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
            document.getElementById('points').innerHTML += "latitude = " + element[0] + " longitude = " + element[1] + "<br>"
        });
    }

    function getPosition(){
        navigator.geolocation.watchPosition(
            function(position){
                currentPoint[0] = position.coords.latitude;
                currentPoint[1] = position.coords.longitude;
                document.getElementById('position').innerHTML = "latitude = " + currentPoint[0] + " longitude = " + currentPoint[1];
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
