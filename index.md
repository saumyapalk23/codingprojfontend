<head>
    <title>Photo Carousel</title>
</head>
<body>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.6.0/css/bootstrap.min.css">
    <style>
        body {
            background-color: #01060d;
            color: #fff;
            align-items: center;
        }
        img.displayed{
            margin-left: auto;
            margin-right: auto;
            }
    </style>

<body>
    <h1 class="text-center m-5">RMR Class Management Tool</h1>
    <h3 class="text-center m-5">Made by AP CSA Class of '22-'23</h3>
    <div id="carouselExampleIndicators" class="carousel slide" data-ride="carousel">
        <ol class="carousel-indicators">
            <li data-target="#carouselExampleIndicators" data-slide-to="0" class="active"></li>
            <li data-target="#carouselExampleIndicators" data-slide-to="1"></li>
            <li data-target="#carouselExampleIndicators" data-slide-to="2"></li>
            <li data-target="#carouselExampleIndicators" data-slide-to="3"></li>
            <li data-target="#carouselExampleIndicators" data-slide-to="4"></li>
            <li data-target="#carouselExampleIndicators" data-slide-to="5"></li>
        </ol>
        <div class="carousel-inner">
            <div class="carousel-item active">
                <img src="assets/images/dnhs.jpg" class="displayed d-block w-50" alt="Image 1">
            </div>
            <div class="carousel-item">
                <img src="assets/images/image2.jpg" class="displayed d-block w-50" alt="Image 2">
            </div>
            <div class="carousel-item">
                <img src="assets/images/teamptfive.jpg" class="displayed d-block w-50" alt="Image 3">
            </div>
             <div class="carousel-item">
                <img src="assets/images/imgfive.jpg" class="displayed d-block w-50" alt="Image 4">
            </div>
            <div class="carousel-item">
                <img src="assets/images/image1.jpg" class="displayed d-block w-50" alt="Image 5">
            </div>
             <div class="carousel-item">
                <img src="assets/images/imgsix.jpg" class="displayed d-block w-50" alt="Image 6">
            </div>
        </div>
        <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-slide="prev">
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
            <span class="sr-only">Previous</span>
        </a>
        <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-slide="next">
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
            <span class="sr-only">Next</span>
        </a>
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.6.0/js/bootstrap.min.js"></script>
</body>




