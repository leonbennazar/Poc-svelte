<div class='container'>
  <h1>Welcome</h1>
  <h2>Explore the world of Titans and key moments</h2>
  <div class='boxes'>

    <div class = 'progress'> <h3>See and mark key moments</h3> </div>

    <div class = 'titans'> <h3>Learn about different titans and their qualities</h3></div>
  </div>
</div>

<style>
  .container{
    display: flex;
    flex-direction: column; 
    align-items: center;    
    justify-content: center;
  }
  .container h1{
    font-size: 120px;
    margin-bottom: 20px;
    margin-top: 40px;
    color: #fff; /* cambio a blanco */
    text-shadow: 2px 2px 8px rgba(0,0,0,0.7); /* opcional, para resaltar más */                        
                            /*font-size: 120px;
                            margin-bottom: 20px;
                            margin-top: 40px;
                            transition: 1s ease;*/
  }
.container h2 {
    font-size: 20px;
    color: #ddd; /* gris claro */
    margin-bottom: 40px;
    text-shadow: 1px 1px 6px rgba(0,0,0,0.6);
  /*font-size: 20px;
  color: #555;
  margin-bottom: 40px;*/
}
  .boxes{
    display:flex;
    gap: 100px;

    
  }

  .progress, .titans{
    display:flex;
    text-align: center;
    /*box-shadow: 0px 0px 10px;*/
    border-radius: 10px;
    width: 250px;
    padding: 10px;
    transition: transform 0.2s ease, box-shadow 0.3s ease, background-color 0.2s ease;
    cursor: pointer;
    background: rgba(255,255,255,0.85);  /*más suave */
    box-shadow: 0px 4px 12px rgba(0,0,0,0.3);
  }

  
  .progress:hover, .titans:hover{
    transform: translateY(-5px);                                                                  /*box-shadow: 0px 0px 30px #d50000;*/
    box-shadow: 0px 8px 20px rgba(213, 0, 0, 0.4);                                              /*transition: 1s ease;*/
  }

  h1:hover{
    color: #d50000;
    transition: 1s ease;
    cursor: default;
  }

/* modificaciones*/

.progress, .titans {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;

  width: 250px;
  padding: 20px;

  background: #ffffff;          /* Fondo blanco limpio */
  border-radius: 12px;
  box-shadow: 0px 4px 12px rgba(0,0,0,0.1); 

  transition: transform 0.2s ease, box-shadow 0.3s ease, background-color 0.2s ease;
  cursor: pointer;
  font-weight: 600;
}

/* Hover: resaltar la tarjeta */
.progress:hover, .titans:hover {
  box-shadow: 0px 8px 20px rgba(213, 0, 0, 0.4);
  transform: translateY(-4px); /* efecto de "flotar" */
}

/* Active: simular "clic presionado" */
.progress:active, .titans:active {
  background-color: #f0f0f0;
  box-shadow: 0px 2px 8px rgba(0,0,0,0.2);
  transform: scale(0.96); /* efecto de botón presionado */
}

:global(body) {
  margin: 0;
  padding: 0;
  min-height: 100vh;
  background: url('/fondo-attack-on-titan.jpg') no-repeat center center fixed;
  background-size: cover;
  position: relative;
}

:global(body)::before {
  content: "";
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  z-index: -1;
}


</style>