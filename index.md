<html>
    <head>
        <meta charset="UTF-8" />
        <script>
            // début du script géo
            
            function getPosition(){
                navigator.geolocation.getCurrentPosition(function(position){
                    document.getElementById('position').innerHTML = "latitude = " + position.coords.latitude + " longitude = " + position.coords.longitude
                });
            }

            if("geolocation" in navigator){
                document.getElementById('position').innerHTML = "la géolocalisation est disponible :)";   
            }
            else{
                document.getElementById('position').innerHTML = "la géolocalisation n'est pas disponible :(";
            }
 
        </script>
    </head>
    <body>
        <button onclick="getPosition()">Localiser</button>
        <span id="position"></span>
    </body>
</html>
