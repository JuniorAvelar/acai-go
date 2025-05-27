<template>
    <div >
        <div class="container">
            <div class="img-container">
                <img src="img/Login-rafiki (1).png" alt="">
            </div>
            <div class="form-container">
                <h2>Login  </h2>
                <form class="form-control">
                    <label for="email">Email:</label>
                    <input type="email" name="email" id="email" placeholder="Digite seu email">

                    <label for="password">Senha:</label>
                    <input type="password" name="password" id="password" placeholder="********">

                    <button>Login</button>
                </form>

                <p >Esqueceu sua senha?</p>
            </div>

        </div>
    </div>
</template>


<script>  
    export default {
        name: 'Login'
    }
</script>

<style scoped>

    .container {
        width: 700px;
        height: 500px;
        margin: 5rem auto;
        box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;  
        display: flex;
        border-radius: 10px;
    }

    .img-container {
        flex: 1;        
        background: #E2C6F9;
        display: flex;
        justify-content: center;
        align-items: center;
        border-top-left-radius: 10px;
        border-bottom-left-radius: 10px;
    }

    .img-container img {
        width: 300px;
        margin-bottom: 70px;
    }

    .form-container {
        flex: 2;
        border-top-right-radius: 10px;
        border-bottom-right-radius: 10px;
    }

    .form-container h2 {
        margin-top: 2rem;
        text-align: center;
        font-size: 32px;
        color: #200D2F;
    }

    .form-control {
        display: flex;
        flex-direction: column;
        width: 350px;
        margin: 1rem auto;
    }

    .form-control input {
        padding: 5px 10px;
        font-size: 14px;
        border-radius: 8px;
        border: none;
        background: #D9D9D9;
        margin-top: 5px;
        margin-bottom: 10px;
    }

    .form-control button {
        margin-top: 40px;
        padding: 7px;
        font-size: 14px;
        border-radius: 8px;
        border: none;
        background-color: #28A745;
        color: #fff;
        font-weight: bold;
        cursor: pointer;
        transition: 0.4s;
    }

    .form-control button:hover {
        background-color: #28a746c9;
    }

    .form-container p {
        margin-top: 40px;
        text-align: center;
        transition: 0.3s;
        color: #383636dd;
    }

    .form-container p:hover {
        color: rgb(0, 94, 255);
        cursor: pointer;
    }
</style>