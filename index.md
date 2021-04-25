<script>
    function getPosition(){
        navigator.geolocation.watchPosition(function(position){
            document.getElementById('position').innerHTML = "latitude = " + position.coords.latitude + " longitude = " + position.coords.longitude
        });
    }
    if("geolocation" in navigator){
        //document.getElementById('position').innerHTML = "la géolocalisation est disponible :)";
        getPosition();
    }
    else{
        document.getElementById('position').innerHTML = "la géolocalisation n'est pas disponible :(";
    }
</script>

<span id="position"></span>
