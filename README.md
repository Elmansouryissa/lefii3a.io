<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS Envelope + Letter (Open/Close on Click)</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Gill+Sans:wght@400;700&display=swap">
    <style>
        :root{
            --primary: #fff;
            --bg-color: rgb(5, 53, 61);
            --bg-envelope-color: #f5edd1;
            --envelope-tab: #ecdeb8;
            --envelope-cover: #e6cfa7;
            --shadow-color: rgba(0, 0, 0, 0.2);
            --txt-color: #444;
            --heart-color: rgb(252, 8, 231);
        }

        body{
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            background: var(--bg-color);
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .container {
            height: 100vh;
            display: grid;
            place-items: center;
        }

        .container > .envelope-wrapper {
            background: var(--bg-envelope-color);
            box-shadow: 0 0 40px var(--shadow-color);
            position: relative;
        }

        .envelope-wrapper > .envelope {
            position: relative;
            width: 300px;
            height: 230px;
        }

        .envelope-wrapper > .envelope::before {
            content: "";
            position: absolute;
            top: 0;
            z-index: 2;
            border-top: 130px solid var(--envelope-tab);
            border-right: 150px solid transparent;
            border-left: 150px solid transparent;
            transform-origin: top;
            transition: all 0.5s ease-in-out 0.7s;
        }

        .envelope-wrapper > .envelope::after {
            content: "";
            position: absolute;
            z-index: 2;
            width: 0px;
            height: 0px;
            border-top: 130px solid transparent;
            border-right: 150px solid var(--envelope-cover);
            border-bottom: 100px solid var(--envelope-cover);
            border-left: 150px solid var(--envelope-cover);
        }

        .envelope > .letter {
            position: absolute;
            right: 10%;
            bottom: 0;
            width: 54%;
            height: 80%;
            background: var(--primary);
            text-align: justify; /* إضافة الخاصية لمحاذاة النص */
            transition: all 1s ease-in-out;
            box-shadow: 0 0 5px var(--shadow-color);
            padding: 23px 10px;
            overflow-y: auto;
        }

        .envelope > .letter > .text {
            font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
            color: var(--txt-color);
            text-align: left;
            font-size: 16px;
        }

        .heart {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 15px;
            height: 15px;
            background: var(--heart-color);
            z-index: 4;
            transform: translate(-50%, -20%) rotate(45deg);
            transition: transform 0.5s ease-in-out 1s;
            box-shadow: 0 1px 6px var(--shadow-color);
            cursor: pointer;
        }

        .heart:before, 
        .heart:after {
            content: "";
            position: absolute;
            width: 15px;
            height: 15px;
            background-color: var(--heart-color);
            border-radius: 50%;
        }

        .heart:before {
            top: -7.5px;
        }

        .heart:after {
            right: 7.5px;
        }

        .flap > .envelope:before {
            transform: rotateX(180deg);
            z-index: 0;
        }

        .flap > .envelope > .letter {
            bottom: 100px;
            transform: translateY(-95%);
            transition-delay: 1s;
            height: 70%;
            width: 75%;
        }

        .flap > .heart {
            transform: rotate(90deg);
            transition-delay: 0.4s;
        }

        /* تحسين تجربة المستخدم على الأجهزة المحمولة */
        @media only screen and (max-width: 600px) {
            .envelope > .letter {
                width: 90%;
            }

            .footer-text {
                position: absolute;
                bottom: 20px;
                left: 50%;
                transform: translateX(-50%);
                font-size: 14px;
                color: rgb(231, 173, 63);
            }
          
            .noscript-msg {
                display: none;
            }
        }

        @media only screen and (min-width: 601px) {
            .footer-text {
                position: absolute;
                bottom: 300px;
                left: 50%;
                transform: translateX(-50%);
                font-size: 20px;
                color: rgba(229, 95, 241, 0.568);
                font-style: italic;
            }

            .noscript-msg {
                position: absolute;
                top: 20px;
                left: 20px;
                font-size: 16px;
                color: red;
            }
        }
    </style>
</head>
<body>
    <noscript class="noscript-msg">JavaScript is disabled. Enable JavaScript to view the content.</noscript>
    <div class="container">
        <div class="envelope-wrapper">
            <div class="envelope">
                <div class="letter">
                    <div class="text">
                        <strong>Dear Khaoula</strong>
                        <p>Awalan Kanbghiik onmot ala din mook .Mohim  lyom 04/04/2004 Ye3ni Lyom Kmelna 4 snin  ghi lbareh  kanet 2021  banti  nji ndi korsi  jiti bghiti tdih nti  tghanina alih la ndih ana la ana  derbt yomin ala dak nhar  tsahbna  awel mra tlaqina ana lbestk  lbesti djin o bokliti ch3er  bhala ghi lbareh  galolk yae wach Aissa maradich yjib M3ak ta siimana hahia daba 2021 /2022 /2023 /2024 *4  saraha wahowa fik lmachakil bzzaf ye3ni katejebdi zga bzzaf ms wakha hakk nbghik  nbghi din mok  ha7na galolek Mradich Yjib m3ak ta simana ha7na daba Tal3in 5 Mohim knbgheeek oradi tbqay nti Ahsen bent 3reftha   la jit n3eberlk  khassni ktab</p>
                    </div>
                </div>
            </div>
            <div class="heart"></div>
        </div>
        <div class="footer-text">04/04/2021   04/04/2024 4 Years</div>
       
    <script>
        const envelope = document.querySelector('.envelope-wrapper');
        envelope.addEventListener('click', () => {
            envelope.classList.toggle('flap');
        });
    </script>
</body>
</html>
