# viral-mms
A viral entertainment website featuring trending videos, news, updates, and popular content from around the web.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Viral Videos</title>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, sans-serif;
    background: #0f0f0f;
    color: white;
}

header {
    background: #181818;
    padding: 15px;
    position: sticky;
    top: 0;
    z-index: 10;
}

.logo {
    font-size: 25px;
    font-weight: bold;
    margin-bottom: 12px;
}

.search {
    width: 100%;
    padding: 12px;
    border: none;
    border-radius: 6px;
    background: #292929;
    color: white;
    font-size: 16px;
}

nav {
    display: flex;
    gap: 8px;
    overflow-x: auto;
    padding: 12px 0;
}

nav button {
    border: none;
    padding: 10px 18px;
    border-radius: 20px;
    background: #292929;
    color: white;
    white-space: nowrap;
    cursor: pointer;
}

nav button:hover {
    background: #e50914;
}

.ad {
    margin: 15px;
    height: 90px;
    background: #222;
    border: 1px dashed #555;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #aaa;
}

.container {
    padding: 10px 15px 30px;
}

.section-title {
    font-size: 22px;
    margin: 15px 0;
}

.videos {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
}

.card {
    background: #1c1c1c;
    border-radius: 8px;
    overflow: hidden;
}

.thumbnail {
    width: 100%;
    height: 130px;
    object-fit: cover;
    background: #333;
}

.card-content {
    padding: 10px;
}

.title {
    font-size: 15px;
    font-weight: bold;
    margin-bottom: 6px;
}

.date {
    font-size: 12px;
    color: #999;
    margin-bottom: 9px;
}

.watch {
    width: 100%;
    padding: 9px;
    border: none;
    border-radius: 5px;
    background: #e50914;
    color: white;
    font-weight: bold;
    cursor: pointer;
}

.pagination {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-top: 25px;
}

.pagination button {
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    background: #292929;
    color: white;
}

footer {
    text-align: center;
    padding: 25px;
    color: #888;
}

/* Video popup */

.modal {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.9);
    z-index: 100;
    align-items: center;
    justify-content: center;
    padding: 15px;
}

.modal-box {
    width: 100%;
    max-width: 700px;
    background: #181818;
    padding: 15px;
    border-radius: 8px;
}

.modal video {
    width: 100%;
    max-height: 70vh;
}

.close {
    float: right;
    font-size: 25px;
    cursor: pointer;
    margin-bottom: 10px;
}

/* Desktop */

@media (min-width: 700px) {
    .videos {
        grid-template-columns: repeat(4, 1fr);
    }

    .thumbnail {
        height: 170px;
    }

    .container {
        max-width: 1200px;
        margin: auto;
    }
}
</style>
</head>

<body>

<header>

<div class="logo">🔥 Viral Videos</div>

<input
class="search"
id="search"
type="text"
placeholder="Search videos..."
onkeyup="searchVideos()">

<nav>
<button onclick="showCategory('all')">All</button>
<button onclick="showCategory('new')">New</button>
<button onclick="showCategory('popular')">Popular</button>
</nav>

</header>

<div class="ad">
Advertisement
</div>

<main class="container">

<h2 class="section-title" id="heading">Latest Videos</h2>

<div class="videos" id="videoList"></div>

<div class="pagination">
<button onclick="previousPage()">← Previous</button>
<span id="pageNumber">Page 1</span>
<button onclick="nextPage()">Next →</button>
</div>

</main>

<footer>
© 2026 Viral Videos — All Rights Reserved
</footer>


<!-- Watch Video Popup -->

<div class="modal" id="modal">

<div class="modal-box">

<span class="close" onclick="closeVideo()">✕</span>

<video id="player" controls>
<source id="videoSource" src="" type="video/mp4">
</video>

<h3 id="videoTitle"></h3>

</div>

</div>


<script>

const videos = [

{
title: "Amazing Trending Video",
category: "new",
date: "Today",
popular: true,
thumbnail: "https://picsum.photos/600/400?random=1",
video: ""
},

{
title: "Funny Viral Moment",
category: "new",
date: "Today",
popular: true,
thumbnail: "https://picsum.photos/600/400?random=2",
video: ""
},

{
title: "Amazing Entertainment",
category: "all",
date: "Yesterday",
popular: false,
thumbnail: "https://picsum.photos/600/400?random=3",
video: ""
},

{
title: "Popular Trending Video",
category: "popular",
date: "Yesterday",
popular: true,
thumbnail: "https://picsum.photos/600/400?random=4",
video: ""
},

{
title: "New Viral Content",
category: "new",
date: "2 days ago",
popular: false,
thumbnail: "https://picsum.photos/600/400?random=5",
video: ""
},

{
title: "Top Trending Video",
category: "popular",
date: "3 days ago",
popular: true,
thumbnail: "https://picsum.photos/600/400?random=6",
video: ""
}

];

let currentCategory = "all";
let currentPage = 1;
const perPage = 6;


function displayVideos() {

let list = videos.filter(video => {

if(currentCategory === "all")
return true;

if(currentCategory === "popular")
return video.popular === true;

return video.category === currentCategory;

});

let start = (currentPage - 1) * perPage;
let end = start + perPage;

let pageVideos = list.slice(start, end);

let html = "";

pageVideos.forEach((video, index) => {

html += `

<div class="card">

<img
class="thumbnail"
src="${video.thumbnail}"
alt="${video.title}">

<div class="card-content">

<div class="title">
${video.title}
</div>

<div class="date">
${video.date}
</div>

<button
class="watch"
onclick="watchVideo(${videos.indexOf(video)})">
▶ Watch
</button>

</div>

</div>

`;

});

document.getElementById("videoList").innerHTML =
html || "<p>No videos found.</p>";

document.getElementById("pageNumber").innerText =
"Page " + currentPage;

}


function showCategory(category) {

currentCategory = category;
currentPage = 1;

if(category === "new")
document.getElementById("heading").innerText = "New Videos";

else if(category === "popular")
document.getElementById("heading").innerText = "Popular Videos";

else
document.getElementById("heading").innerText = "All Videos";

displayVideos();

}


function searchVideos() {

let search =
document.getElementById("search").value.toLowerCase();

let cards = document.querySelectorAll(".card");

cards.forEach(card => {

let title =
card.querySelector(".title").innerText.toLowerCase();

card.style.display =
title.includes(search) ? "block" : "none";

});

}


function watchVideo(index) {

let video = videos[index];

document.getElementById("modal").style.display = "flex";

document.getElementById("videoTitle").innerText =
video.title;

document.getElementById("videoSource").src =
video.video;

document.getElementById("player").load();

}


function closeVideo() {

document.getElementById("modal").style.display = "none";

document.getElementById("player").pause();

}


function nextPage() {

currentPage++;

displayVideos();

}


function previousPage() {

if(currentPage > 1) {

currentPage--;

displayVideos();

}

}


displayVideos();

</script>

</body>
</html>
