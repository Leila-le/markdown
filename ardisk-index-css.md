body {
    margin: 0;
    width: 100vw;
    font-size: 0.7292vw;
    background: white linear-gradient(180deg, #111111 8%, rgba(255, 255, 255, 0.17) 1920px);
    font-family: Helvetica, 'Hiragino Sans GB', 'Microsoft Yahei', '微软雅黑', Arial, sans-serif;
}

a {
    text-decoration: none;
}

.navigator {
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
    width: 75vw;
    margin: 0 23vw 0 23vw;
    padding-top: 2.7083vw;
}

.navigator .title {
    font-size: 1.4583vw;
    font-weight: 700;
    margin-right: auto;
    vertical-align: top;
}

.navigator img {
    height: 42px;
    margin: auto 13px 2px 0;
}

.navigator a {
    font-size: 1em;
    font-weight: 500;
    cursor: pointer;
    margin-left: 50px;
    color: white;
}

.navigator .menu {
    width: 56%;
    text-align: left;
}

.focus {
    display: flex;
    align-items: flex-start;
    height: 904px;
    flex-direction: column;
    color: white;

}

.focus a {
    font-size: 1.75em;
    color: #735B2A;
    text-align: justify;
    font-weight: 500;
}

.focus span {
    margin-left: 349px;
    font-size: 3.25em;
    text-align: justify;
    font-weight: 500;
}

.focus .title {
    height: 72px;
    min-width: 770px;
    font-size: 3.25em;
    font-weight: 500;
    margin: 293px auto 0 23%;

}

.focus .sub-title {
    height: 29px;
    min-width: 464px;
    font-size: 1.3125em;
    font-weight: 400;
    margin: 29px auto 0 23%;
}

.focus .download {
    min-width: 296px;
    height: 64px;
    margin: 93px auto auto 23%;
    background-image: linear-gradient(90deg, #E0C28A 0%, #F1DCB3 100%, #F0DCB2 100%);
    border-radius: 10px;
    background-size: 100% 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    line-height: 72px;
    color: #735B2A;
    font-weight: 500;
}


.features {
    height: 82px;
    display: flex;
    flex-direction: row;
    align-items: center;
    margin: 0 auto 150px auto;
    padding: 0 16% 0 16%;
    background: url(banner.png) no-repeat;
    background-size: 100% 100%;
}

.features .feature-item {
    color: rgba(37, 42, 42, 1);
    font-size: 1.5em;
    font-weight: 500;
    line-height: 33px;
    cursor: pointer;
    text-align: center;
    flex: 1 0 auto;
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
}


.feature {
    display: flex;
    flex-direction: row;
    margin-bottom: 204px;
}

.feature .left {
    width: 15%;
    margin: 0 100px auto auto;
}

.feature .left .title {
    color: rgba(37, 42, 42, 1);
    font-size: 1.75em;
    font-weight: 700;
    line-height: 38px;
}

.feature .left .sub-title {
    color: rgba(37, 42, 42, 1);
    font-size: 2.625em;
    font-weight: 700;
    line-height: 58px;
    margin-top: 32px;
}

.feature .left .description {
    overflow-wrap: break-word;
    margin-top: 19px;
    color: #252A2A;
    font-size: 1.1325em;
    text-align: justify;
    line-height: 32px;
    font-weight: 400;
}

.feature .right {
    width: 55%;
}

.feature .right img {
    width: 679px;
}


.partners {

}

.partners .header {
    background: #434343;
    color: #EEDAAE;
    text-align: center;
    font-weight: 500;
    height: 326px;
    width: 100%;
}

.partners .title {
    padding-top: 86px;
    font-size: 3em;
    text-align: center;
    font-weight: 500;
}

.partners .sub-title {
    margin-top: 28px;
    font-size: 1.5em;
    text-align: center;
    font-weight: 400;
}

.partners .list {
    width: 1278px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 30px;
    margin: 125px auto 115px auto;
}

.partners .list img {
    border-radius: 4px;
    height: 160px;
    width: 304px;
}


.about-us {

}

.about-us .header {
    height: 326px;
    background: #434343;
}

.about-us .title {
    padding-top: 120px;
    font-size: 3em;
    color: #EEDAAE;
    text-align: center;
    font-weight: 500;
}

.about-us .sub-title {
    margin-top: 28px;
    font-size: 1.5em;
    color: #EEDAAE;
    text-align: center;
    font-weight: 400;
}

.about-us .list {
    display: flex;
    flex-flow: row;
    justify-content: center;
    align-items: center;
    height: 958px;
}

.about-us .list .block1 {
    width: 48%;
    height: 58.1%;
    padding: 20.5% 0 20% 0;
}

.about-us .list .block1 img {
    width: 100%;
    max-height: 565px;
}

.about-us .list .block2 {
    background: #DBC496;
    border: 1px solid #FFFFFF;
    margin: 157px 0 151px 0;
    width: 17.8125%;
    height: 67.8%;

}

.about-us .list .block2 a {
    margin: 73.3% 40% 19.5% 12.2%;
    width: 34%;
    max-width: 116px;
    height: 46px;
    background: #FFFFFF;
    box-shadow: 0 2px 4px 0 rgba(136, 104, 43, 0.31);
    border-radius: 10px;
    font-size: 1.125em;
    color: #735B2A;
    text-align: justify;
    font-weight: 500;
    padding: 10px 9% 10px 9%;
    text-decoration: underline;
}

.about-us .list .block2 img {
    width: 12%;
    max-width: 20px;
}

.about-us .list .block3 {
    background: #FFECC4;
    border: 1px solid #FFFFFF;
    margin: 157px 0 151px 0;
    width: 17.8125%;
    min-width: 342px;
    height: 67.8%;
}

.about-us .list .block4 {
    background: #FFF5E0;
    border: 1px solid #FFFFFF;
    margin: 157px 0 151px 0;
    width: 17.8125%;
    height: 67.8%;
}

.about-us .list .block4 img {
    margin: 18px auto 40px auto;
    max-width: 190px;
    height: 100%;
}

.about-us .list .title {
    font-size: 1.5em;
    color: #111111;
    font-weight: 500;
    text-align: center;
    margin-bottom: 43px;
}

.about-us p {
    padding: 0 50px 0 50px;
    font-size: 1.125em;
    color: #111111;
    line-height: 28px;
    font-weight: 400;
    text-indent: 40px;
    margin: 14px 0 14px 0;
}

.about-us .qrcode {
    width: 80%;
}

.business {
    width: 100%;
    height: 326px;
    background-image: linear-gradient(90deg, #AD945A 0%, #F1DCB3 100%, #FFF9ED 100%);
    text-align: center;
}


.business .title {
    padding-top: 87px;
    font-size: 3em;
    color: #111111;
    text-align: center;
    font-weight: 500;
    margin-bottom: 33px;
}

.business a {
    width: 270px;
    height: 27px;
    padding: 15px 75px 15px 75px;
    background: #FFFFFF;
    box-shadow: 0 2px 4px 0 rgba(136, 104, 43, 0.31);
    border-radius: 10px;
    font-size: 1.875em;
    color: #735B2A;
    letter-spacing: 0;
    font-weight: 500;
}


.last-section {
    font-size: 1.125em;
    max-height: 674px;
    color: #FFFFFF;
    text-align: center;
    line-height: 38px;
    font-weight: 400;
    background: url(Navigation_bar.png) 100% no-repeat;
    background-size: cover;
    padding-top: 231px;
}

.last-section p, .last-section .block p {
    color: #FFFFFF;
    text-align: center;
    line-height: 38px;
}

.last-section a {
    color: #ffffff;
    margin-bottom: 18px;
}

.last-section .title {
    font-size: 1.5em;
    font-weight: 500;
}

.last-section .sub-title {
    margin: 29px 0;
}

.last-section .list {
    padding: 0 20%;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
}

.block {
    margin: 0 auto 107px 0;
    text-align: left;
}

.block .title {
    margin-bottom: 29px;
}

.footer {
    padding-bottom: 46px;
}
