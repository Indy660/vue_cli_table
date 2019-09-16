<template>
    <div>

        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">

            <div class="collapse navbar-collapse" id="navbar1">
                <ul class="navbar-nav mr-auto">
                    <li v-bind:class="{'nav-item': true, active: (mainPage==='users')}">
                        <a class="nav-link" v-on:click="showArrayUsers">Таблца пользователей <span class="sr-only">(current)</span></a>
                    </li>
                    <li v-bind:class="{'nav-item': true, active: (mainPage==='files')}">
                        <a class="nav-link" v-on:click="showArrayFiles">Таблца файлов</a>
                    </li>
<!--                    <li class="nav-item dropdown">-->
<!--                        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown1" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">Dropdown</a>-->
<!--                        <div class="dropdown-menu" aria-labelledby="navbarDropdown1">-->
<!--                            <a class="dropdown-item" href="#">Action</a>-->
<!--                            <a class="dropdown-item" href="#">Another action</a>-->
<!--                            <div class="dropdown-divider"></div>-->
<!--                            <a class="dropdown-item" href="#">Something else here</a>-->
<!--                        </div>-->
<!--                    </li>-->
                </ul>
                <form class="form-inline my-2 my-lg-0">
<!--                    <input class="form-control mr-sm-2" type="search" placeholder="Логин" aria-label="Search">-->
<!--                    <input class="form-control mr-sm-2" type="password" placeholder="Пароль" aria-label="Search">-->
                    <h5  class="text-info mr-sm-2">Вы вошли как: {{authorizedUser}}</h5>
                    <button class="btn btn-outline-info my-5 my-sm-0" type="submit" v-on:click="Logout">Выйти</button>
                </form>
            </div>
        </nav>
    </div>
</template>

<script>
    export default {
        name: "navbar",
        props:[ "Logout", "authorizedUser", "showArrayUsers", "showArrayFiles","mainPage"],

    }
</script>
