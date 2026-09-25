/* =====================================================
   GAMEARENA - GAMING TOURNAMENT PORTAL
   JavaScript
===================================================== */


/* ================= LOGIN ================= */

function openLogin() {

    document
        .getElementById("loginModal")
        .classList.add("active");

}


function closeLogin() {

    document
        .getElementById("loginModal")
        .classList.remove("active");

}


function login() {

    const email =
        document.getElementById("loginEmail").value.trim();

    const password =
        document.getElementById("loginPassword").value.trim();


    if (email === "" || password === "") {

        alert("⚠️ Please enter your email and password.");

        return;
    }


    if (!email.includes("@")) {

        alert("⚠️ Please enter a valid email address.");

        return;
    }


    alert(
        "🎮 Login successful!\n\nWelcome to GameArena."
    );

    closeLogin();

}


/* ================= REGISTER ================= */

function openRegister() {

    document
        .getElementById("registerModal")
        .classList.add("active");

}


function closeRegister() {

    document
        .getElementById("registerModal")
        .classList.remove("active");

}


function registerUser() {

    const name =
        document.getElementById("registerName").value.trim();

    const email =
        document.getElementById("registerEmail").value.trim();

    const password =
        document.getElementById("registerPassword").value.trim();


    if (name === "" ||
        email === "" ||
        password === "") {

        alert(
            "⚠️ Please fill all the fields."
        );

        return;
    }


    if (!email.includes("@")) {

        alert(
            "⚠️ Please enter a valid email."
        );

        return;
    }


    if (password.length < 6) {

        alert(
            "⚠️ Password must contain at least 6 characters."
        );

        return;
    }


    alert(
        "🎉 Account created successfully!\n\nWelcome " +
        name +
        "!"
    );


    closeRegister();

}


/* ================= SWITCH MODALS ================= */

function switchToRegister() {

    closeLogin();

    openRegister();

}


function switchToLogin() {

    closeRegister();

    openLogin();

}


/* ================= TOURNAMENT REGISTRATION ================= */

function registerTournament(tournamentName) {

    const confirmation =
        confirm(
            "🏆 Tournament Registration\n\n" +
            "Do you want to register for:\n\n" +
            tournamentName +
            "?"
        );


    if (confirmation) {

        alert(
            "✅ Registration successful!\n\n" +
            "Tournament: " +
            tournamentName +
            "\n\nGood luck, Champion! 🎮"
        );

    }

}


/* ================= SEARCH & FILTER ================= */

function filterTournaments() {

    const searchValue =
        document
            .getElementById("searchTournament")
            .value
            .toLowerCase();


    const gameValue =
        document
            .getElementById("gameFilter")
            .value;


    const statusValue =
        document
            .getElementById("statusFilter")
            .value;


    const cards =
        document.querySelectorAll(
            ".tournament-card"
        );


    cards.forEach(card => {

        const title =
            card
                .querySelector("h3")
                .textContent
                .toLowerCase();


        const game =
            card.dataset.game;


        const status =
            card.dataset.status;


        const searchMatch =
            title.includes(searchValue);


        const gameMatch =
            gameValue === "all" ||
            game === gameValue;


        const statusMatch =
            statusValue === "all" ||
            status === statusValue;


        if (
            searchMatch &&
            gameMatch &&
            statusMatch
        ) {

            card.style.display = "block";

        } else {

            card.style.display = "none";

        }

    });

}


/* ================= NOTIFICATIONS ================= */

function showNotifications() {

    const panel =
        document
            .getElementById("notificationPanel");


    panel.classList.toggle("active");

}


function closeNotifications() {

    document
        .getElementById("notificationPanel")
        .classList.remove("active");

}


/* ================= LIVE MATCH ================= */

function watchMatch(matchName) {

    alert(
        "🔴 LIVE MATCH\n\n" +
        "You are now watching:\n" +
        matchName +
        "\n\nLive streaming feature can be connected to a streaming service later."
    );

}


/* ================= TEAM ================= */

function createTeam() {

    const teamName =
        prompt(
            "👥 Enter your new team name:"
        );


    if (teamName === null) {

        return;

    }


    if (teamName.trim() === "") {

        alert(
            "⚠️ Team name cannot be empty."
        );

        return;

    }


    alert(
        "🎉 Team created successfully!\n\n" +
        "Team Name: " +
        teamName +
        "\n\nYou can now invite players."
    );

}


function viewTeam(teamName) {

    alert(
        "👥 TEAM PROFILE\n\n" +
        "Team: " +
        teamName +
        "\n\n" +
        "🏆 Tournament Wins: 24\n" +
        "⭐ Win Rate: 90%\n" +
        "🎮 Active Players: 5"
    );

}


/* ================= CLOSE MODAL WHEN CLICKING OUTSIDE ================= */

window.addEventListener(
    "click",
    function(event) {

        const loginModal =
            document.getElementById(
                "loginModal"
            );


        const registerModal =
            document.getElementById(
                "registerModal"
            );


        if (
            event.target === loginModal
        ) {

            closeLogin();

        }


        if (
            event.target === registerModal
        ) {

            closeRegister();

        }

    }
);


/* ================= KEYBOARD ESCAPE ================= */

document.addEventListener(
    "keydown",
    function(event) {

        if (event.key === "Escape") {

            closeLogin();

            closeRegister();

            closeNotifications();

        }

    }
);


/* ================= NOTIFICATION COUNTER ================= */

let notificationCount = 3;


function clearNotifications() {

    notificationCount = 0;

    document
        .getElementById("notificationCount")
        .textContent = notificationCount;

}


/* ================= PAGE LOADED ================= */

document.addEventListener(
    "DOMContentLoaded",
    function() {

        console.log(
            "🎮 GameArena loaded successfully!"
        );


        /* Add a small live update effect */

        setInterval(
            updateLiveScores,
            10000
        );

    }
);


/* ================= LIVE SCORE SIMULATION ================= */

function updateLiveScores() {

    const scoreElements =
        document.querySelectorAll(
            ".live-card .team strong"
        );


    scoreElements.forEach(
        element => {

            let score =
                parseInt(
                    element.textContent
                );


            if (
                Math.random() > 0.65
            ) {

                score++;

                element.textContent =
                    score;

            }

        }
    );

}


/* ================= SMOOTH NAVIGATION ================= */

document
    .querySelectorAll(
        'a[href^="#"]'
    )
    .forEach(
        anchor => {

            anchor.addEventListener(
                "click",
                function(event) {

                    const target =
                        document.querySelector(
                            this.getAttribute("href")
                        );


                    if (target) {

                        event.preventDefault();

                        target.scrollIntoView({
                            behavior: "smooth"
                        });

                    }

                }
            );

        }
    );
