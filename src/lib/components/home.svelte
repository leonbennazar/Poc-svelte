<div class='container'>
  <h1>Welcome</h1>
  <div class='boxes'>

    <div class = 'progress'> <h2>See and mark key moments</h2> </div>

    <div class = 'titans'> <h2>Learn about different titans and their qualities</h2></div>

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
    font-size: 300px;
    margin-bottom: 10px;
    margin-top: 40px;
    transition: 1s ease;

  }


  .boxes{
    display:flex;
    gap: 100px;

    
  }

  .progress, .titans{
    display:flex;
    text-align: center;
    box-shadow: 0px 0px 10px;
    border-radius: 10px;
    width: 250px;
    padding: 10px;
    transition: 1s ease;
  }

  
  .progress:hover, .titans:hover{
    box-shadow: 0px 0px 30px #d50000;
    transition: 1s ease;
  }

  h1:hover{
    color: #d50000;
    transition: 1s ease;
  }
</style>|