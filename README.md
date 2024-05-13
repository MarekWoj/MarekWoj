<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="utf-8">
    <title>Canvas cz. 2/2</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">    
    <meta http-equiv="X-Ua-Compatible" content="IE=edge">
    <link rel="stylesheet" href="style.css">
</head>
<style>
    #canvas {
        background-image: url('obraz.png');
        background-size: cover;
        position: relative;
    }
    #box1 {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 150px;
        height: 80px;
        background-color: white;
    
    }
    #box2 {
        position: absolute;
        top: 20%;
        left: 30%;
        transform: translate(-50%, -50%);
        width: 150px;
        height: 80px;
        background-color: white;
    }
    #box3 {
        position: absolute;
        top: 20%;
        left: 70%;
        transform: translate(-50%, -50%);
        width: 150px;
        height: 80px;
        background-color: white;
    }
    #box4 {
        position: absolute;
        top: 80%;
        left: 30%;
        transform: translate(-50%, -50%);
        width: 150px;
        height: 80px;
        background-color: white;
    }
    #box5 {
        position: absolute;
        top: 80%;
        left: 70%;
        transform: translate(-50%, -50%);
        width: 150px;
        height: 80px;
        background-color: white;
    }
</style>
<body>
    <main>
        <article>
            <div class="board">
                <div id="points">Punkty: </div>
                
                <canvas id="canvas" width="1200" height="800">
                </canvas>
            </div>
       
            <div id="box1" width="150" height="80"></div>
            <div id="box2" width="150" height="80"></div>
            <div id="box3" width="150" height="80"></div>
            <div id="box4" width="150" height="80"></div>
            <div id="box5" width="150" height="80"></div>
        </article>
    </main>
    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');

       
        const img_idle = new Image();
        img_idle.onload = function() {
         
            ctx.drawImage(img_idle, 0, 0);
           
            update();
        };
        img_idle.src = 'statek1.png'; 
        var x1 = 550;
        var y1 = 600;
        var lewo = 0; 
        var prawo = 0; 
        var dol = 0;  
        var objectWidth = 55; 
        var objectHeight = 55; 
        const img_idle1 = new Image();
        img_idle1.onload = function() {
          
            ctx.drawImage(img_idle1, 0, 0);
           
            update();
        };
        img_idle1.src = 'statek2.png';


       

   
        var x2 = (Math.floor(Math.random()*600+1));;
        var y2 = (Math.floor(Math.random()*600+1));;
        var objectWidth1 = 55; 
        var objectHeight1 = 55;
        var xyz =1.5; 
        var xyz2 =1.5;

       
        function update() {
            
            ctx.clearRect(0, 0, canvas.width, canvas.height);

          
            x1 += lewo + prawo;
            y1 += dol;

           
            if (x1 <= 0 || x1 + objectWidth >= canvas.width) {
                 lewo = -lewo; 
            }
            if (y1 <= 0 || y1 + objectHeight >= canvas.height) {
               dol = -dol; 
            }
                 

          
            ctx.drawImage(img_idle, x1, y1);

           
            x2 += xyz;
            y2 += xyz2;

            
            if (x2 <= 0 || x2 + objectWidth1 >= canvas.width) {
                xyz = -xyz; 
            }
            if (y2 <= 0 || y2 + objectHeight1 >= canvas.height) {
                xyz2 = -xyz2; 
            }

        
            collision();

           
            ctx.drawImage(img_idle1, x2, y2);

           
            requestAnimationFrame(update);
        }

        window.addEventListener("keydown", function(event) {
            if (event.code == 'KeyD') prawo = 2;
            if (event.code == 'KeyA') lewo = -2;
            if (event.code == 'KeyS') dol = 2;
            if (event.code == 'KeyW') dol = -2;
        });

        window.addEventListener("keyup", function(event) {
            if (event.code == 'KeyD') prawo = 0;
            if (event.code == 'KeyA') lewo = 0;
            if (event.code == 'KeyS') dol =0;
            if (event.code == 'KeyW') dol = 0;
        });

        var points = 0;

function addPoints() {
    if (collision()) {
        points = points + 1;
       
    }
}

function collision() {
   
    if (x1 < x2 + objectWidth1 &&
        x1 + objectWidth > x2 &&
        y1 < y2 + objectHeight1 &&
        y1 + objectHeight > y2) {
       
        points = points + 1;
        document.getElementById("points").innerHTML = "Punkty: " + points; 
        teleport(); 
        return true; 
    }
    return false; 
}
        function teleport() {
            
            x2 = (Math.floor(Math.random()*600+1)); 
            y2 = (Math.floor(Math.random()*600+1)); 
        }

    </script>
</body>
</html>
