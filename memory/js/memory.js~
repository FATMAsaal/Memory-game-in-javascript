(function () {
    'use strict';
    var tabTuile = new Array();
    var tuile_t = null;
    var instance = false;
    var start = false;
    var temps = 120;
    var timeout = false;
    
    /* objets */
    function Tuile(id) {
        this.retourne = false;
        this.id = id;
        this.found = false;
    }
    
    /* prototype ARRAY */
    Array.prototype.getid = function(idi) {
        var i = 0;
        for(i; i < this.length; i += 1)
            if(this[i].id == idi)
                return this[i];
        return null;
    }
    
    Array.prototype.retourner = function () {
        var i = 0;
        for(i; i < this.length; i += 1)
            if(this[i].retourne)
                this[i].retourne = false;
    }
    
    Array.prototype.estGagne = function () {
        var i = 0;
        for(i; i < this.length; i += 1)
            if(!this[i].found)
                return false;
        return true;
    }
    
    /* creer le dom */
    init();
    /* listeners */
    document.getElementById("start").addEventListener("click", function() {
        /* commencer la partie */
        start = true;
        upd();
    }, false);
    
    function upd() {
        var int = setInterval(function() {
            temps -= 1;
            updateTime();
            if(temps <= 0) {
                alert("Temps écoulé !");
                clearInterval(int);
                timeout = true;
                endGame();
            }
        }, 1000);
    }
    /* sur chaque image */ 
    
    document.getElementById("memory-content").addEventListener("click", function (event) {
        event.preventDefault();
        var target = event.target;
        console.log(target);
        if(!timeout && start && !instance && target && target.classList.contains("mem")) {
            if(!tuile_t || (tuile_t.id != target.dataset.idimage && !tabTuile[target.dataset.idimage - 1].retourne)) {
                var elem_id = target.dataset.idimage;
                var id_image = id(elem_id);
                /* retourner l'image */
                var tuile_tmp = tabTuile.getid(elem_id); 
                tuile_tmp.retourne = true/* retourner la tuile */
                if(!tuile_t)
                    tuile_t = tuile_tmp;
                else {
                    /* verifier si elles sont identique */
                    var id_a = id(tuile_t.id);
                    var id_b = id(tuile_tmp.id);
                    if(id_a == id_b) {
                        /* paire trouvee */
                        tuile_t.found = true;
                        tuile_tmp.found = true;
                        tuile_t = null;
                        /* reafficher le content */
                        displayContent();
                        return;
                    } else {
                        /* faux retourner toutes les tuiles */
                        displayContent();
                        instance = true;
                        setTimeout(function(){
                            tabTuile.retourner();
                            /* reafficher le content */
                            displayContent();
                            tuile_t = null;
                            instance = false;
                        }, 1000);
                        return;
                    }
                    
                }
                /* reafficher le content */
                displayContent();
                /* verifier si la partie est gagnee */
                if(tabTuile.estGagne()) {
                	alert("victoire");
                }
            }
        } else return false;
    });
    
    function init () {
        var parent = document.getElementById("memory-content");
        var i = 0, content, img;
        /* creer tuiles */
        for(i = 0; i < 16; i += 1) {
            tabTuile.push(new Tuile(i+1));
        }
        shuffle(tabTuile); /* melanger */
        tabTuile.forEach(function (elem, ind) {
            content = document.createElement("div");
            content.classList.add("memclass");
            img = document.createElement("img");
            img.setAttribute("src", "./img/mem_back.jpg");
            img.classList.add("mem");
            img.dataset.idimage = elem.id;
            /* append */
            content.appendChild(img);
            /* append in memory content */
            parent.appendChild(content);
        });
    };
    
    function displayContent() {
        var parent = document.getElementById("memory-content");
        while (parent.firstChild) { /* vider */
            parent.removeChild(parent.firstChild);
        }
        var content, img;
        tabTuile.forEach(function (elem, ind) {
            content = document.createElement("div");
            content.classList.add("memclass");
            img = document.createElement("img");
            img.dataset.idimage = elem.id;
            if(elem.found || elem.retourne)
                img.setAttribute("src", "./img/mem" + id(elem.id) + ".jpg");
            else
                img.setAttribute("src", "./img/mem_back.jpg");
            img.classList.add("mem");
            content.appendChild(img);
            /* append in memory content */
            parent.appendChild(content);
        });
    }
    
    function updateTime() {
        var span = document.getElementById("time");
        var date = new Date(null);
        date.setSeconds(temps);
        span.innerHTML = "";
        span.insertAdjacentHTML("beforeend", date.getMinutes() + ":" + date.getSeconds());
    }
    
    function endGame() {
        
    }
    
    function id(i) {
        if(i > 8)
        	return i - 8;
        else
       	return i;
    } 
    
    function shuffle(a) {
        var j, x, i;
        for (i = a.length - 1; i > 0; i--) {
            j = Math.floor(Math.random() * (i + 1));
            x = a[i];
            a[i] = a[j];
            a[j] = x;
        }
    }
}());
