body {
    background: white;
    padding: 0;
    margin: 0;
    font: normal 100vw Helvetica, Arial, sans-serif;
    font-size: 0.7292vw;
    font-family: Helvetica, 'Hiragino Sans GB', 'Microsoft Yahei', '微软雅黑', Arial, sans-serif;
    display: flex;
    flex-flow: column;
    overflow-x: hidden;
}

.bg {
    width: 100vw;
    height: 46.875vw;
    background: linear-gradient(black, white);
}

a {
    text-decoration: none;
    color: #111111;
}

.banner {
    background: #1F1F1F;
    height: 3.125vw;
    display: flex;
    justify-content: center;
    align-items: center;
}

.banner span {
    font-size: 1.0938vw;
    color: #FFF8F8;
    text-align: center;
    font-weight: 500;
}

.navigator {
    display: flex;
    align-items: center;
    height: 3.125vw;
    padding: 0 19.84vw;
    background: #FFFFFF;
    box-shadow: 0 0.1042vw 0.2083vw 0 rgba(207, 207, 207, 0.50);
}

.navigator span {
    font-size: 1.4583vw;
    color: #111111;
    font-weight: 500;
    margin-right: auto;
    margin-bottom: 0.2604vw;
    vertical-align: middle;
}

.navigator .logo {
    display: flex;
    align-items: center;
}

.navigator .logo img {
    width: 1.6667vw;
    height: 1.6667vw;
    margin: auto 0.6771vw auto 0;
    vertical-align: middle;
}

.navigator .menu {
    display: flex;
    margin: 0 0.5vw 0 auto;
    height: 1.5625vw;
}

.navigator .menu .menu-item {
    margin: 0 0.4688vw 0 0.4688vw;
    padding: 0 0.8333vw;
    background: #FFFFFF;
    border: 0.0521vw solid #BABABA;
    border-radius: 0.2083vw;
    color: #7D7D7D;
    font-size: 0.8333vw;
    font-weight: 400;
    text-align: center;
}

.navigator .menu .item1:hover {
    color: #FF6F08;;
}

.navigator .menu .item2 {
    background: #FF6F08;
    color: #FFFFFF;
    border: 0.0521vw solid #FF6F08;
}


.main {
    display: grid;
    grid-template-columns: 60vw 1fr;

}

.header {
    margin-left: 10vw;
    padding-top: 5.7292vw;
    color: white;
    background-image: url(big-show.webp);
    background-size: contain;
    background-repeat: no-repeat;
    background-position: 0 10vw;
}

.header h1 {
    margin-left: 11vw;
    font-size: 2.7083vw;
    font-weight: 700;
}

.header h2 {
    margin-left: 11vw;
    font-size: 1.3542vw;
    font-weight: 400;
}

.register-form {
    background: #FFFFFF;
    box-shadow: 0 0.1042vw 0.2083vw 0 rgba(204, 204, 204, 0.50);
    border-radius: 0.7292vw;
    width: 25vw;
    height: 37.7083vw;
    display: flex;
    flex-direction: column;
    margin-top: 3.25vw;
    justify-content: center;
    padding: 2.21vw 2.21vw 0 2.21vw;
}

.form-controls {
    margin: 2.9167vw 3.2813vw auto 3.2813vw;
    position: relative;
}

.form-controls input {
    background: #FFFFFF;
    border: 0.0521vw solid #AEAEAE;
    border-radius: 0.1042vw;
    font-size: 0.6771vw;
    color: #9C9C9C;
    font-weight: 400;
}

.form-controls input:hover {
    border: 0.0521vw solid #FF7C1F;
}

.form-controls .login {
    color: #121212;
    line-height: 1.0417vw;
    font-weight: 400;
    display: flex;
    justify-content: flex-end;
    margin-bottom: 0.9896vw;
}

.form-controls .login a {
    color: #FF6F08;
    line-height: 1.0417vw;
    font-weight: 400;
}

.form-controls .caption {
    display: flex;
    margin: 0 auto 0.6771vw auto;
    font-size: 1.5625vw;
    font-weight: 400;
    color: #121212;
    justify-content: center;
}

.form-controls .subtitle {
    display: flex;
    margin: 0 auto 1.1458vw auto;
    font-weight: 400;
    color: #121212;
    justify-content: center;
}

.form-controls .tooltip {
    position: relative;
    display: inline-block;
}

.form-controls .tooltip-text {
    visibility: hidden;
    width: 15vw;
    background-color: rgba(93, 93, 93, 0.45);
    color: #fff;
    text-align: left;
    border-radius: 0.3125vw;
    padding: 0.3vw 1vw;
    position: absolute;
    z-index: 1;
    left: 5vw;
    margin-top: -0.7292vw;
    font-size: 0.5208vw;
    margin-left: -3.125vw;
}

.form-controls .tooltip-text p {
    margin: 0;
}

.form-controls .tooltip .tooltip-text::after {
    content: "";
    position: absolute;
    bottom: 100%;
    left: 3vw;
    border-style: solid;
    border-width: 0.5vw;
    border-color: transparent transparent rgba(93, 93, 93, 0.45) transparent;
}

.form-controls input[type='text'], input[type='tel'], input[type='password'] {
    margin: 0;
    width: 18vw;
    height: 1.6vw;
    color: #121212;
    padding-left: 1.21vw;
}

.form-controls .tooltip:hover .tooltip-text {
    visibility: visible;
}

.form-controls button {
    border: 0.0521vw;
    font-size: 0.7292vw;
    color: white;
    width: 19.3vw;
    height: 1.6667vw;
    background: #FF6F08;
    border-radius: 0.1042vw;
}

.form-controls button:hover {
    background: #FF8935;
    border-radius: 0.1042vw;
}

.form-controls .error-message {
    display: block;
    font-size: 0.625vw;
    height: 1.4583vw;
    color: red;
    width: 25vw;
}

.form-controls .sms-code {
    width: 20vw;
    display: flex;
    align-items: center;
}

.form-controls .sms-code input[type="text"] {
    width: 20vw;
}

.form-controls .sms-code button {
    margin: 0 0.6vw 0 0.61vw;
    width: 15vw;
    font-size: 0.6875vw;
    font-weight: 400;
    height: 1.7708vw;
}

.form-controls .agreement {
    height: 1.4583vw;
    display: flex;
    align-items: center;
    font-size: 0.625vw;
    color: #FF6F08;
    text-align: justify;
    line-height: 0.8854vw;
    font-weight: 400;
    padding-top: 0.7292vw;
}

.form-controls .agreement span {
    color: #121212;
}

.form-controls .agreement a {
    text-decoration: underline;
    color: #FF6F08;
}

.form-controls #btnRegister {
    margin-bottom: 5.4167vw;
}

.footer {
    margin: 5vw 0 0 0;
    text-align: center;
    font-size: 0.8333vw;
    color: #111111;
    line-height: 1.9792vw;
    font-weight: 400;
}

.footer .separator {
    margin: 0 0.5vw;
}

@media (max-width: 1024px) {
    body {
        min-width: 610px;
        font-size: 14px;
        min-height: 100vh;
        overflow-x: hidden;
    }

    .bg {
        width: 100%;
        flex: 1;
    }

    .banner {
        height: 60px;
    }

    .banner span {
        font-size: 1.3125em;
    }

    .navigator {
        height: 60px;
        padding: 0 5vw;
    }

    .navigator span {
        font-size: 1.75em;
    }

    .navigator .logo {
        display: flex;
        align-items: center;
    }

    .navigator .logo img {
        width: 32px;
        height: 32px;
    }

    .navigator .menu {
        height: 30px;
    }

    .navigator .menu .menu-item {
        padding: 0.5vw 0.8333vw;
        border: 1px solid #BABABA;
        border-radius: 4px;
        font-size: 1em;
    }

    .navigator .menu .item1:hover {
        color: #FF6F08;;
    }

    .navigator .menu .item2 {
        border: 1px solid #FF6F08;
    }


    .main {
        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: 1fr 5fr;
        margin-bottom: 1vw;
        /*padding-bottom: 5vw;*/
    }

    .header {
        margin-left: 0;
        padding-top: 9vw;
        color: white;
        background-image: none;
    }

    .header h1 {
        margin: 0;
        font-size: 3.25em;
        font-weight: 700;
        text-align: center;
    }

    .header h2 {
        margin: 0;
        text-align: center;
        font-size: 1.625em;
        font-weight: 400;
    }

    .register-form {
        background: #FFFFFF;
        box-shadow: 0 2px 4px 0 rgba(204, 204, 204, 0.50);
        border-radius: 14px;
        width: 28.64%;
        min-width: 450px;
        height: auto;
        display: flex;
        flex-direction: column;
        margin: 6.25vw auto 5vw auto;
        justify-content: center;
        padding: 4.21vw 2.21vw 2.21vw 3.21vw;
        align-items: center;
    }

    .form-controls {
        margin: 2.9167vw 3.2813vw auto 3.2813vw;
        position: relative;
    }

    .form-controls input {
        background: #FFFFFF;
        border: 1px solid #AEAEAE;
        border-radius: 2px;
        font-size: 0.8125em;
        color: #9C9C9C;
        font-weight: 400;
    }

    .form-controls input:hover {
        border: 2px solid #FF7C1F;
    }

    .form-controls .login {
        color: #121212;
        line-height: 20px;
        font-weight: 400;
        display: flex;
        justify-content: flex-end;
        margin-bottom: 0.9896vw;
    }

    .form-controls .login a {
        color: #FF6F08;
        line-height: 20px;
        font-weight: 400;
    }

    .form-controls .caption {
        display: flex;
        margin: 0 auto 0.6771vw auto;
        font-size: 1.875em;
        font-weight: 400;
        color: #121212;
        justify-content: center;
    }

    .form-controls .subtitle {
        display: flex;
        margin: 0 auto 1.1458vw auto;
        font-weight: 400;
        color: #121212;
        justify-content: center;
    }

    .form-controls .tooltip {
        position: relative;
        display: inline-block;
        width: 100%;
    }

    .form-controls .tooltip-text {
        visibility: hidden;
        width: 50%;
        background-color: rgba(93, 93, 93, 0.45);
        color: #fff;
        text-align: left;
        border-radius: 4px;
        padding: 0.3vw 1vw;
        position: absolute;
        z-index: 1;
        left: 5vw;
        margin-top: -0.7292vw;
        font-size: 0.625em;
        margin-left: -3.125vw;
    }

    .form-controls .tooltip-text p {
        margin: 0;
    }

    .form-controls .tooltip .tooltip-text::after {
        content: "";
        position: absolute;
        bottom: 100%;
        left: 3vw;
        border-style: solid;
        border-width: 10px;
        border-color: transparent transparent rgba(93, 93, 93, 0.45) transparent;
    }

    .form-controls input[type='text'], input[type='tel'], input[type='password'] {
        margin: 0;
        width: 95%;
        height: 32px;
        color: #121212;
        padding-left: 1.21vw;
    }

    .form-controls .tooltip:hover .tooltip-text {
        visibility: visible;
    }

    .form-controls button {
        border: 0.0521vw;
        font-size: 0.875em;
        color: white;
        width: 100%;
        height: 32px;
        background: #FF6F08;
        border-radius: 0.1042vw;
    }

    .form-controls button:hover {
        background: #FF8935;
        border-radius: 2px;
    }

    .form-controls .error-message {
        display: block;
        font-size: 0.75em;
        height: 28px;
        color: red;
        width: 20%;
    }

    .form-controls .sms-code {
        width: 98%;
        display: flex;
        align-items: center;
    }

    .form-controls .sms-code input[type="text"] {
        width: 75%;
        height: 32px;
    }

    .form-controls .sms-code button {
        flex-grow: 1;
        margin: 0 0 0 1vw;
        font-size: 0.8125em;
        font-weight: 400;
        height: 32px;
    }

    .form-controls .agreement {
        display: flex;
        align-items: center;
        font-size: 0.75em;
        color: #FF6F08;
        text-align: justify;
        line-height: 17px;
        font-weight: 400;
        padding-top: 5%;
    }

    .form-controls .agreement span {
        color: #121212;
    }

    .form-controls .agreement a {
        text-decoration: underline;
        color: #FF6F08;
    }

    .form-controls #btnRegister {
        margin-bottom: 0;
        width: 98%;
    }

    .footer {
        margin: auto 0 5vw 0;
        text-align: center;
        font-size: 1em;
        color: #111111;
        line-height: 38px;
        font-weight: 400;
    }

    .footer .separator {
        margin: 0 0.5vw;
    }

}

====================================================================================================
body {
    min-width: 1280px;
    min-height: 100vh;
    background: white;
    padding: 0;
    margin: 0;
    font: normal 100% Helvetica, Arial, sans-serif;
    font-size: 1em;
    font-family: Helvetica, 'Hiragino Sans GB', 'Microsoft Yahei', '微软雅黑', Arial, sans-serif;
    display: flex;
    flex-flow: column;
}

.bg {
    background: linear-gradient(black, white);
    width: 100%;
    flex: 1;
}

a {
    text-decoration: none;
    color: #111111;
}

.banner {
    height: 60px;
    background: #1F1F1F;
    display: flex;
    justify-content: center;
    align-items: center;
}

.banner span {
    font-size: 1.3125em;
    color: #FFF8F8;
    text-align: center;
    font-weight: 500;
}


.navigator {
    display: grid;
    grid-template-columns: 20% 80%;
    grid-gap: 38.5%;
    align-items: center;
    color: white;
    padding: 70px 17% 0 23%;
}

.navigator .title {
    font-size: 1.625em;
    font-weight: 700;
    margin-right: auto;
}

.logo {
    display: flex;
    justify-content: start;
    align-items: center;
    margin-left: -1.7%;
}

.logo a {
    min-width: 12em;
    display: flex;
    flex-flow: row;
    align-items: center;
    text-decoration: none;
}

.logo img {
    height: 27px;
    display: block;
    margin-right: 5px;
}

.navigator a {
    font-size: 1em;
    font-weight: 500;
    cursor: pointer;
    color: white;
    width: 4em;
}

.navigator .menu {
    width: 49%;
    text-align: center;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 2em;
    justify-items: start;
}

.main {
    width: 90%;
    display: grid;
    grid-template-columns: 1fr 1fr;
    margin: auto 0 1% 10%;
}

.header-container {
    padding-top: 128px;
    margin-left: 0;
    margin-right: -20%;
}

.header {
    color: white;
}

.header-container .img-container {
    height: 600px;
    background-image: url(big-show.webp);
    background-size: contain;
    background-repeat: no-repeat;
    background-position: 30% 40%;
    z-index: -1;
    margin-top: -100px;
}

.header h1 {
    margin-left: 24%;
    font-size: 3.25em;
    font-weight: 700;
    text-align: left;
}

.header h2 {
    margin-left: 24%;
    text-align: left;
    font-size: 1.625em;
    font-weight: 400;
}

.register-form {
    background: #FFFFFF;
    box-shadow: 0 2px 4px 0 rgba(204, 204, 204, 0.50);
    border-radius: 14px;
    width: 45%;
    min-width: 450px;
    height: 50%;
    min-height: 700px;
    display: flex;
    flex-direction: column;
    margin: 120px auto 110px 12%;
    justify-content: center;
    align-items: center;
}

.form-controls {
    height: 90%;
    width: 70%;
}

.form-controls input {
    background: #FFFFFF;
    border: 1px solid #AEAEAE;
    border-radius: 2px;
    font-size: 0.8125em;
    color: #9C9C9C;
    font-weight: 400;
}

.form-controls input:hover {
    border-color: #FF7C1F;
}

.form-controls .login {
    color: #121212;
    line-height: 20px;
    font-weight: 400;
    display: flex;
    justify-content: flex-end;
    margin-bottom: 0.9896vw;
}

.form-controls .login a {
    color: #FF6F08;
    line-height: 20px;
    font-weight: 400;
}

.form-controls .caption {
    display: flex;
    margin: 0 auto 1% auto;
    font-size: 1.875em;
    font-weight: 400;
    color: #121212;
    justify-content: center;
}

.form-controls .subtitle {
    display: flex;
    margin: 0 auto 8% auto;
    font-weight: 400;
    color: #121212;
    justify-content: center;
}

.form-controls .tooltip {
    position: relative;
    display: inline-block;
    width: 100%;
}

.form-controls .tooltip-text {
    visibility: hidden;
    width: 50%;
    background-color: rgba(93, 93, 93, 0.45);
    color: #fff;
    text-align: left;
    border-radius: 4px;
    padding: 0.3vw 1vw;
    position: absolute;
    z-index: 1;
    left: 5vw;
    margin-top: -0.7292vw;
    font-size: 0.625em;
    margin-left: -3.125vw;
}

.form-controls .tooltip-text p {
    margin: 0;
}

.form-controls .tooltip .tooltip-text::after {
    content: "";
    position: absolute;
    bottom: 100%;
    left: 3vw;
    border-style: solid;
    border-width: 10px;
    border-color: transparent transparent rgba(93, 93, 93, 0.45) transparent;
}

.form-controls input[type='text'], input[type='tel'], input[type='password'] {
    margin: 0;
    width: 93%;
    height: 32px;
    color: #121212;
    padding-left: 5%;
}

.form-controls .tooltip:hover .tooltip-text {
    visibility: visible;
}

.form-controls button {
    border: 0.0521vw;
    font-size: 0.875em;
    color: white;
    width: 100%;
    height: 32px;
    background: #FF6F08;
    border-radius: 0.1042vw;
}

.form-controls button:hover {
    background: #FF8935;
    border-radius: 2px;
}

.form-controls .error-message {
    display: block;
    font-size: 0.75em;
    height: 28px;
    color: red;
    width: 99%;
}

.form-controls .sms-code {
    width: 98%;
    display: flex;
    align-items: center;
}

.form-controls .sms-code input[type="text"] {
    width: 75%;
    height: 32px;
}

.form-controls .sms-code button {
    flex-grow: 1;
    margin: 0 -1% 0 5%;
    font-size: 0.8125em;
    font-weight: 400;
    height: 32px;
}

.form-controls .agreement {
    display: flex;
    align-items: center;
    font-size: 0.75em;
    color: #FF6F08;
    text-align: justify;
    line-height: 17px;
    font-weight: 400;
    padding-top: 5%;
}

.form-controls .agreement span {
    color: #121212;
}

.form-controls .agreement a {
    text-decoration: underline;
    color: #FF6F08;
}

.form-controls #btnRegister {
    margin-bottom: 0;
    width: 100%;
}

.footer {
    margin: auto;
    text-align: center;
    font-size: 1em;
    color: #111111;
    line-height: 38px;
    font-weight: 400;
}

.footer .separator {
    margin: 0 0.5vw;
}

@media (max-width: 1660px) {
    .navigator {
        display: grid;
        grid-template-columns: 20% 80%;
        grid-gap: 47%;
        align-items: center;
        color: white;
        padding: 70px 23% 0 13.5%;
    }

    .main {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr;
    margin: auto 0 1% 0;
}
    .header h1 {
    margin-left: 22%;
    font-size: 3.25em;
    font-weight: 700;
    text-align: left;
}

.header h2 {
    margin-left: 22%;
    text-align: left;
    font-size: 1.625em;
    font-weight: 400;
}
.header-container .img-container {
    height: 600px;
    background-image: url(big-show.webp);
    background-size: contain;
    background-repeat: no-repeat;
    background-position: 15% 40%;
    z-index: -1;
    margin-top: -100px;
}
}
