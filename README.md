<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Viral Videos</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    background:#111;
    color:#fff;
    font-family:Arial,Helvetica,sans-serif;
}

/* HEADER */
.header{
    background:#1b1b1b;
    padding:18px 5%;
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:20px;
    border-bottom:1px solid #333;
}

.logo{
    font-size:26px;
    font-weight:bold;
    white-space:nowrap;
}

.logo span{
    color:#ff2d55;
}

.search{
    width:45%;
    display:flex;
}

.search input{
    width:100%;
    padding:12px 15px;
    border:0;
    outline:0;
    background:#292929;
    color:white;
    border-radius:6px 0 0 6px;
}

.search button{
    border:0;
    background:#ff2d55;
    color:white;
    padding:0 18px;
    cursor:pointer;
    border-radius:0 6px 6px 0;
}

/* CATEGORY BAR */
.categories{
    background:#181818;
    padding:13px 5%;
    display:flex;
    gap:10px;
    overflow-x:auto;
    border-bottom:1px solid #292929;
}

.categories button{
    background:#292929;
    color:#ddd;
    border:0;
    padding:9px 17px;
    border-radius:20px;
    cursor:pointer;
    white-space:nowrap;
}

.categories button:hover,
.categories button.active{
    background:#ff2d55;
    color:#fff;
}

/* AD */
.ad{
    margin:20px auto;
    max-width:1100px;
    height:90px;
    background:#202020;
    display:flex;
    align-items:center;
    justify-content:center;
    color:#777;
    border:1px dashed #444;
}

/* CONTENT */
.container{
    width:90%;
    max-width:1200px;
    margin:auto;
}

.section-title{
    margin:25px 0 15px;
    font-size:22px;
    border-left:4px solid #ff2d55;
    padding-left:10px;
}

/* VIDEO GRID */
.video-grid{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:18px;
}

.card{
    background:#1c1c1c;
    border-radius:8px;
    overflow:hidden;
    transition:.25s;
}

.card:hover{
    transform:translateY(-4px);
    box-shadow:0 5px 20px rgba(0,0,0,.5);
}

.thumb{
    position:relative;
    width:100%;
    aspect-ratio:16/9;
    background:#333;
    overflow:hidden;
}

.thumb img{
    width:100%;
    height:100%;
    object-fit:cover;
}

.duration{
    position:absolute;
    right:8px;
    bottom:8px;
    background:rgba(0,0,0,.8);
    padding:4px 7px;
    font-size:12px;
    border-radius:4px;
}

.info{
    padding:12px;
}

.title{
    font-size:15px;
    line-height:1.4;
    height:42px;
    overflow:hidden;
}

.meta{
    color:#888;
    font-size:12px;
    margin:8px 0;
}

.watch{
    display:block;
    text-align:center;
    background:#ff2d55;
    color:white;
    text-decoration:none;
    padding:9px;
    border-radius:5px;
    margin-top:8px;
    cursor:pointer;
}

/* PAGINATION */
.pagination{
    display:flex;
    justify-content:center;
    gap:10px;
    margin:35px 0;
}

.pagination button{
    background:#292929;
    border:0;
    color:white;
    padding:10px 18px;
    border-radius:5px;
    cursor:pointer;
}

.pagination button:hover{
    background:#ff2d55;
}

/* FOOTER */
footer{
    background:#181818;
    border-top:1px solid #333;
    padding:30px 5%;
    text-align:center;
    color:#888;
    margin-top:30px;
}

footer a{
    color:#aaa;
    margin:0 8px;
    text-decoration:none;
}

/* MOBILE */
@media(max-width:900px){
    .video-grid{
        grid-template-columns:repeat(3,1fr);
    }

    .search{
        width:40%;
    }
}

@media(max-width:650px){
    .header{
        flex-wrap:wrap;
    }

    .logo{
        width:100%;
        text-align:center;
    }

    .search{
        width:100%;
    }

    .video-grid{
        grid-template-columns:repeat(2,1fr);
        gap:12px;
    }

    .container{
        width:94%;
    }

    .ad{
        margin:15px 3%;
    }

    .title{
        font-size:13px;
    }
}
</style>
</head>

<body>

<header class="header">

    <div class="logo">
        🔥 Viral<span>Videos</span>
    </div>

    <div class="search">
        <input type="text" id="searchBox" placeholder="Search videos...">
        <button onclick="searchVideos()">🔍</button>
    </div>

</header>

<nav class="categories">
    <button class="active" onclick="filterVideos('All',this)">All</button>
    <button onclick="filterVideos('New',this)">New</button>
    <button onclick="filterVideos('Popular',this)">Popular</button>
    <button onclick="filterVideos('Funny',this)">Funny</button>
    <button onclick="filterVideos('Sports',this)">Sports</button>
    <button onclick="filterVideos('News',this)">News</button>
    <button onclick="filterVideos('Entertainment',this)">Entertainment</button>
</nav>

<div class="ad">
    ADVERTISEMENT
</div>

<main class="container">

    <h2 class="section-title">🔥 Latest Videos</h2>

    <div class="video-grid" id="videoGrid"></div>

    <div class="pagination">
        <button onclick="previousPage()">← Previous</button>
        <button onclick="nextPage()">Next →</button>
    </div>

</main>

<footer>
    <p>© 2026 ViralVideos. All rights reserved.</p>
    <br>
    <a href="#">Home</a>
    <a href="#">Categories</a>
    <a href="#">Privacy</a>
    <a href="#">Contact</a>
</footer>

<script>

const videos = [

{
title:"Amazing Viral Video You Should Watch",
category:"Popular",
views:"125K",
date:"Today",
duration:"04:32",
image:"https://picsum.photos/600/340?random=1"
},

{
title:"Latest Trending Entertainment Video",
category:"New",
views:"98K",
date:"Today",
duration:"06:15",
image:"https://picsum.photos/600/340?random=2"
},

{
title:"Funny Moments That Went Viral",
category:"Funny",
views:"210K",
date:"Yesterday",
duration:"03:48",
image:"https://picsum.photos/600/340?random=3"
},

{
title:"Top Sports Moments",
category:"Sports",
views:"76K",
date:"Yesterday",
duration:"05:20",
image:"https://picsum.photos/600/340?random=4"
},

{
title:"Breaking News Update",
category:"News",
views:"154K",
date:"Today",
duration:"08:10",
image:"https://picsum.photos/600/340?random=5"
},

{
title:"Popular Entertainment Clips",
category:"Entertainment",
views:"189K",
date:"2 days ago",
duration:"07:25",
image:"https://picsum.photos/600/340?random=6"
},

{
title:"New Viral Video Of The Day",
category:"New",
views:"65K",
date:"Today",
duration:"04:10",
image:"https://picsum.photos/600/340?random=7"
},

{
title:"Most Watched Video This Week",
category:"Popular",
views:"350K",
date:"3 days ago",
duration:"09:15",
image:"https://picsum.photos/600/340?random=8"
}

];

let currentVideos = videos;

function displayVideos(list){

    const grid = document.getElementById("videoGrid");

    grid.innerHTML = "";

    list.forEach((video,index)=>{

        grid.innerHTML += `

        <div class="card">

            <div class="thumb">

                <img src="${video.image}" alt="${video.title}">

                <span class="duration">
                    ${video.duration}
                </span>

            </div>

            <div class="info">

                <div class="title">
                    ${video.title}
                </div>

                <div class="meta">
                    👁 ${video.views} • ${video.date}
                </div>

                <a class="watch"
                   onclick="watchVideo('${video.title}')">
                   ▶ Watch Video
                </a>

            </div>

        </div>

        `;

    });

}

function filterVideos(category,button){

    document.querySelectorAll(".categories button")
    .forEach(btn=>btn.classList.remove("active"));

    button.classList.add("active");

    if(category==="All"){
        currentVideos=videos;
    }else{
        currentVideos=videos.filter(v=>v.category===category);
    }

    displayVideos(currentVideos);
}

function searchVideos(){

    const query =
        document.getElementById("searchBox")
        .value.toLowerCase();

    const results=videos.filter(video =>
        video.title.toLowerCase().includes(query)
    );

    currentVideos=results;

    displayVideos(results);
}

function watchVideo(title){

    alert(
        "You selected: " + title +
        "\\n\\nYour video player/link will be connected here."
    );

}

function nextPage(){
    alert("Next page will load here.");
}

function previousPage(){
    alert("Previous page will load here.");
}

displayVideos(videos);

</script>

</body>
</html>
