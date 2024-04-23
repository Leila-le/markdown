body {
    background: white;
    margin: 0;
    min-width: 1920px;
    font: normal 100% Helvetica, Arial, sans-serif;
    font-size: 0.875em;
    font-family: Helvetica, 'Hiragino Sans GB', 'Microsoft Yahei', '微软雅黑', Arial, sans-serif;
}

a {
    text-decoration: none;
}

.bg {
    height: 630px;
    background: url(about-us-bg2.png) 100% /cover;
}

.navigator {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
    width: 75%;
    margin: 0 23%;
    padding-top: 52px;
}
    .navigator .logo {
        display: flex;
        align-items: center;
    }
    .navigator img {
        height: 42px;
        margin: auto 13px 2px 0;
    }

    .navigator .title {
        font-size: 2em;
        font-weight: 700;
        margin-right: auto;
        margin-bottom: 5px;
        vertical-align: top;
    }

    .navigator a {
        color: white;
        font-size: 1em;
        font-weight: 500;
        cursor: pointer;
        margin-left: 50px;

    }

    .navigator .menu {
        width: 56%;
        text-align: left;
    }

    .navigator .logo {
        margin-left: 0;
    }

.focus {
    display: flex;
    align-items: flex-start;
    flex-direction: column;
    color: white;
    height: 500px;
}

    .focus a {
        color: #735B2A;
    !important;
        font-weight: 500;
        font-size: 1.5em;
        letter-spacing: 0;
        text-align: center;
    }

    .focus span {
        margin-left: 23%;
    }

    .focus .title {
        padding-top: 117px;
        height: 82px;
        font-size: 3.75em;
        font-weight: 500;
    }

    .focus .sub-title {
        font-size: 1.3125em;
        line-height: 30px;
        font-weight: 400;
        margin-top: 35px;
        width: 27%;
    }

    .focus .register {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-left: 23%;
        min-width: 216px;
        height: 52px;
        background-image: linear-gradient(90deg, #E0C28A 0%, #F1DCB3 100%, #F0DCB2 100%);
        box-shadow: 0 2px 4px 0 rgba(136, 104, 43, 0.31);
        border-radius: 5px;
        margin-top: 79px;
    }


.features {
    height: 82px;
    display: flex;
    flex-direction: row;
    align-items: center;
    margin: 0 auto 150px auto;
    padding: 0 17% 0 17%;
    border-bottom: 1px solid #979797;
}

    .features .feature-item {
        color: rgba(37, 42, 42, 1);
        font-size: 1.5em;
        font-weight: 500;
        line-height: 33px;
        cursor: pointer;
        text-align: center;
        flex: 1;
    }

    .features a {
        display: block;
        color: rgba(37, 42, 42, 1) !important;
    }

    .features .feature-item:hover::after {
        display: block;
        width: 84px;
        height: 4px;
        background-color: rgba(231, 204, 147, 1);
        content: "";
        position: relative;
        top: 4px;
        margin: -4px auto 0 auto;
        opacity: 1;
    }


.feature {
    margin-bottom: 116px;
    display: flex;
}

    .feature .title-container {
        height: 50px;
        padding-left: 20%;
        padding-top: 40px;
        margin-bottom: 40px;
        font-weight: 500;
        color: #1F1F1F;
    }

    .feature .title {
        font-size: 2.25em;
        text-align: left;
    }

    .feature .sub-title {
        font-size: 1.125em;
        margin-left: 24px;
    }

    .feature .description {
        font-size: 1.125em;
        color: #1F1F1F;
        line-height: 32px;
        font-weight: 400;
        text-indent: 40px;
        text-align: left;
        margin-left: 20%;
    }

    #section_introduction {
        flex-direction: row;
        margin: 0 20% 0 20%;
    }

    #section_introduction .left {
        width: 40%;
    }

    #section_introduction .right {
        width: 60%;
    }

    #section_introduction .left img {
        width: 100%;
        max-width: 407px;
    }

    #section_introduction .title-container {
        height: 50px;
        padding-top: 40px;
        margin-bottom: 40px;
        padding-left: 0;
    }

    #section_introduction .description {
        overflow-wrap: break-word;
        margin: 19px 0 163px 0;
        width: 100%;
        height: 320px;
    }

    #section_about-us {
        flex-direction: column;
        height: 578px;
        background: url(about-us-bg4.png) 100% no-repeat;
        background-size: cover;
        padding-top: 3%;
    }

    #section_about-us .title, #section_about-us .sub-title {
        color: #FFFFFF;
    }

    #section_about-us .list {
        height: 528px;
        display: flex;
        flex-flow: row;
        margin: 36px 20% 0 20%;
    }

    #section_about-us .description .block {
        width: 30%;
        height: 53%;
        min-width: 553px;
        padding-top: 64px;
        font-size: 1.125em;
        color: #1F1F1F !important;
        text-align: left;
        line-height: 32px;
    }

    #section_about-us .description .block p {
        width: 81.7%;
        height: 192px;
        margin: 0 10% 0 7%;
    }

    #section_about-us .description .left {
        background: url(about-us-bg5.png) 100% no-repeat;
        background-size: 100% 100%;
        margin: 0 0;
    }

    #section_about-us .description .right {
        background: url(about-us-bg6.png) 100% no-repeat;
        background-size: 100% 100%;
        margin-right: 0;
    }

    #section_goal {
        flex-flow: column;
    }

    #section_goal .description {
        width: 75%;
        background: #FFE7B8;
        border-radius: 32px;
        padding: 89px 0 89px 0;
        margin: 0 auto 0 auto;
    }

    #section_goal .description p {
        width: 81%;
        margin: 0 auto 0 auto;
    }

    #section_values {
        height: 600px;
        margin: 0 10%;
    }

    #section_values .left {
        width: 41%;
        padding: 0 5%
    }

    #section_values .right {
        width: 30%;
    }

    #section_values .right img {
        max-width: 584px;
        margin: 0 11%;
        padding-top: 66px;
    }

.last-section {
    font-size: 1.125em;
    height: 890px;
    color: #FFFFFF;
    text-align: center;
    line-height: 38px;
    font-weight: 400;
    background: url(Navigation_bar.png) 100% no-repeat;
    background-size: cover;
    padding-top: 6%;
}

    .last-section p, .last-section .block p {
        font-size: 1em;
        color: #FFFFFF;
        line-height: 38px;
        font-weight: 400;
    }

    .last-section a {
        color: #FFFFFF;
        margin-bottom: 18px;
    }

    .last-section .title {
        font-size: 2.25em;
        font-weight: 500;
    }

    .last-section .sub-title {
        margin: 29px 0;
    }

    .last-section .download {
        margin: auto;
        width: 11.2%;
        height: 52px;
        background: #FFFFFF;
        box-shadow: 0 2px 4px 0 rgba(77, 67, 46, 0.31);
        border-radius: 10px;
    }

    .last-section .download a {
        font-size: 1.25em;
        color: #434343;
        letter-spacing: 0;
        font-weight: 500;
        margin-bottom: 0;
        text-align: center;
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100%;
    }

    .last-section .list {
        padding: 166px 20% 0 20%;
        display: grid;
        grid-template-columns: repeat(5, 1fr);
    }

    .block {
        margin: 0 auto;
        text-align: left;
    }

    .block .title {
        margin-bottom: 29px;
    }

======================================

body {
    background: white;
    margin: 0;
    font: normal 100vw Helvetica, Arial, sans-serif;
    font-size: 0.7292vw;
    font-family: Helvetica, 'Hiragino Sans GB', 'Microsoft Yahei', '微软雅黑', Arial, sans-serif;
}

a {
    text-decoration: none;
}

.bg {
    height: 32.8125vw;
    background: url(about-us-bg2.png) 100vw /cover;
}

.navigator {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
    width: 75vw;
    margin: 0 20.5vw;
    padding-top: 2.7083vw;
}

.navigator .logo {
    display: flex;
    align-items: center;
}

.navigator img {
    height: 2.1875vw;
    margin: auto 0.6771vw 0.1042vw 0;
}

.navigator .title {
    font-size: 1.4583vw;
    font-weight: 700;
    margin-right: auto;
    margin-bottom: 0.2604vw;
    vertical-align: top;
}

.navigator a {
    color: white;
    font-size: 0.8333vw;
    font-weight: 500;
    cursor: pointer;
    margin-left: 2.6042vw;

}

.navigator .menu {
    width: 56vw;
    text-align: center;

}

.navigator .logo {
    margin-left: 0;
}

.focus {
    display: flex;
    align-items: flex-start;
    flex-direction: column;
    color: white;
    height: 26.0417vw;
}

.focus a {
    color: #735B2A;
!important;
    font-weight: 500;
    font-size: 1.25vw;
    letter-spacing: 0;
    text-align: center;
}

.focus span {
    margin-left: 23vw;
}

.focus .title {
    padding-top: 6.0938vw;
    height: 4.2708vw;
    font-size: 3.125vw;
    font-weight: 500;
}

.focus .sub-title {
    font-size: 1.0938vw;
    line-height: 1.5625vw;
    font-weight: 400;
    margin-top: 1.8229vw;
    width: 27vw;
}

.focus .register {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-left: 23vw;
    min-width: 11.25vw;
    height: 2.7083vw;
    background-image: linear-gradient(90deg, #E0C28A 0%, #F1DCB3 100vw, #F0DCB2 100vw);
    box-shadow: 0 0.1042vw 0.2083vw 0 rgba(136, 104, 43, 0.31);
    border-radius: 0.2604vw;
    margin-top: 4.1146vw;
}


.features {
    height: 4.2708vw;
    display: flex;
    flex-direction: row;
    align-items: center;
    margin: 0 auto 7.8125vw auto;
    padding: 0 17vw 0 17vw;
    border-bottom: 0.0521vw solid #979797;
}

.features .feature-item {
    color: rgba(37, 42, 42, 1);
    font-size: 1.25vw;
    font-weight: 500;
    line-height: 1.71875vw;
    cursor: pointer;
    text-align: center;
    flex: 1;
}

.features a {
    display: block;
    color: rgba(37, 42, 42, 1) !important;
}

.features .feature-item:hover::after {
    display: block;
    width: 4.375vw;
    height: 0.2083vw;
    background-color: rgba(231, 204, 147, 1);
    content: "";
    position: relative;
    top: 0.2083vw;
    margin: -0.2083vw auto 0 auto;
    opacity: 1;
}


.feature {
    margin-bottom: 6.0417vw;
    /*display: flex;*/
    display: grid;
}

.feature .title-container {
    height: 2.6042vw;
    padding-left: 20vw;
    padding-top: 2.0833vw;
    margin-bottom: 2.0833vw;
    font-weight: 500;
    color: #1F1F1F;
}

.feature .title {
    font-size: 1.875vw;
    text-align: left;
}

.feature .sub-title {
    font-size: 0.9375vw;
    margin-left: 1.25vw;
}

.feature .description {
    font-size: 0.9375vw;
    color: #1F1F1F;
    line-height: 1.6667vw;
    font-weight: 400;
    text-indent: 2.0833vw;
    text-align: left;
    margin-left: 20vw;
}

#section_introduction {
    grid-template-columns: 1fr 1fr;
    margin: 0 20vw 0 20vw;
}

#section_introduction .right {
    width: 34.2708vw;
}

#section_introduction .left img {
    width: 21.1979vw;
}

#section_introduction .title-container {
    height: 2.6042vw;
    padding-top: 2.0833vw;
    margin-bottom: 2.0833vw;
    padding-left: 0;
}

#section_introduction .description {
    overflow-wrap: break-word;
    margin: 0.9896vw 0 8.4896vw 0;
    height: 16.6667vw;
}

#section_about-us {
    flex-direction: column;
    height: 30.1042vw;
    background-image: url(about-us-bg4.png);
    background-repeat: no-repeat;
    background-size: cover;
    padding: 3vw 20vw 0 20vw;
}

#section_about-us .title-container {
    padding-left: 0;
    color: #FFFFFF;
}

#section_about-us .list {
    height: 27.5vw;
    display: flex;
    flex-flow: row;
    margin: 1.875vw auto 0 auto;
}

#section_about-us .description .block {
    width: 30vw;
    height: 53vw;
    min-width: 28.8021vw;
    padding: 3.3333vw 2.1354vw 0 2.1354vw;
    font-size: 0.9375vw;
    color: #1F1F1F !important;
    text-align: left;
    line-height: 1.6667vw;
}

#section_about-us .description .block p {
    width: 23.5417vw;
    height: 10vw;
    margin: 0;
}

#section_about-us .description .left {
    background-image: url(about-us-bg5.png);
    background-repeat: no-repeat;
    background-size: 28.8021vw 16.1979vw;
    margin: 0;
}

#section_about-us .description .right {
    background-image: url(about-us-bg6.png);
    background-repeat: no-repeat;
    background-size: 28.8021vw 16.1979vw;
    margin-right: 0;
}

#section_goal {
    flex-flow: column;
}

#section_goal .description {
    width: 75vw;
    background: #FFE7B8;
    border-radius: 1.6667vw;
    padding: 4.6354vw 0 4.6354vw 0;
    margin: 0 auto 0 auto;
}

#section_goal .description p {
    width: 60.625vw;
    margin: 0 auto 0 auto;
}

#section_values {
    display: grid;
    grid-template-columns: 1fr 1fr;
    margin: 0 10vw 7.7083vw 10vw;
}

#section_values .left {
    width: 27.7604vw;
}

#section_values .title-container {
    padding-left: 10vw;
}

#section_values .description {
    margin-left: 10vw;
}

#section_values .right {
    width: 30vw;
}

#section_values .right img {
    width: 30.4167vw;
    padding-top: 3.4375vw;
}

.last-section {
    height: 48.2813vw;
    font-size: 0.9375vw;
    color: #FFFFFF;
    text-align: center;
    line-height: 1.9792vw;
    font-weight: 400;
    background-image: url(Navigation_bar.png);
    background-repeat: no-repeat;
    background-size: cover;
    padding-top: 6vw;
}

.last-section p, .last-section .block p {
    font-size: 0.8333vw;
    color: #FFFFFF;
    line-height: 1.9792vw;
    font-weight: 400;
}

.last-section a {
    color: #FFFFFF;
    margin-bottom: 0.9375vw;
}

.last-section .title {
    font-size: 1.875vw;
    font-weight: 500;
}

.last-section .sub-title {
    margin: 1.5104vw 0;
}

.last-section .download {
    margin: auto;
    width: 11.2vw;
    height: 2.7083vw;;
    background: #FFFFFF;
    box-shadow: 0 0.1042vw 0.2083vw 0 rgba(77, 67, 46, 0.31);
    border-radius: 0.5208vw;
    display: flex;
    align-items: center;
    justify-content: center;
}

.last-section .download a {
    margin: 0;
    font-size: 1.0417vw;
    color: #434343;
    letter-spacing: 0;
    font-weight: 500;
}

.last-section .list {
    padding: 8.6458vw 20vw 0 20vw;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
}

.block {
    margin: 0 auto;
    text-align: left;
}

.block .title {
    margin-bottom: 1.5104vw;
}

.block .logo2 {
    width: 3.75vw;
}

.block .contactImg {
    width: 5.0521vw;
}

.block .weixinImg, .pengyouquanImg, .weiboImg {
    width: 0.7813vw;
}

.block .pengyouquanImg {
    margin: 0 1.0938vw;
}

.last .footer {
    margin: 6.0417vw auto auto auto;
}

.last .footer .separator {
    margin: 0 0.5vw;
}
