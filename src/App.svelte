<script>
    let title="";
    let author="";
    let description="";
    let link="";
    let postsDb = [{id:1, user:"frida123", title:"Sherlock", author:"Arthur Conan Doyle", description:"About a guy and his companion...", link:"https://www.google.se/", liked:false, posted:"00:00"},{id:2, user:"abc123", title:"Dexter", author:"Jeff Lindsey", description:"About a disguised killer", link:"https://www.google.se/",liked:false, posted:"00:00"}];

    //yourPosts ska läggas till i användarens objekt
    let yourPosts = [];
    let savedDb = [];


    function addPost(event){


        title = title.trim();
        author = author.trim();
        link = link.trim();

        if(!title && !author && !link) return;

        const post = {
            title: title,
            author: author,
            description:description,
            link: link,
            liked:false,
            posted: Date.now(),
            id:Date.now(),
            user: "Lasse123"
            //user = användarnamn
        };

        postsDb = [...postsDb, post];
        yourPosts = [...yourPosts, post];
        console.log(postsDb);

        title="";
        author="";
        description="";
        link="";
    }

    function savePost(post){
        //lägg till inlägg i sparade
        savedDb = [...savedDb, post];
        console.log(savedDb);
    }
    function deletePost(id){
        alert("Are you sure you want to delete this post?"); //fixa fungerande alert
	    postsDb = postsDb.filter(item => item.id !== id);
    }


</script>



														<!-- HTML -->



	<header>
        <h1>Discover</h1>
    </header>
    <nav>
        <!-- prydnad, ett extra projekt om jag hade tid-->
        <div id="search">
            <input type="text" placeholder="Searchbar">
            <button>Search</button>
        </div>

    </nav>

    <div id="main-container">
        <aside id="left-aside">
            <div id="profile">
                <div id="profile-img">

                </div>
                <div id="profile-text">
                    <p>username</p>
                    <p>Joined (time)</p>
                    <p>Posts</p>
                </div>

            </div>
            <div id="booklists">
                <h3>Your booklists</h3>
                <ul>
                    <li><a href="abc">Your posts</a></li>
                    <li><a href="abc">Saved</a></li>
                </ul>
            </div>
            <div class="add">
                <h3>Add an audiobook!</h3>
                <form action="/add" method="post" id="taskForm" on:submit|preventDefault={addPost}>
                    <input type="text" name ="title" placeholder="Title" bind:value={title}>
                    <br>
                    <input type="text" name ="author" placeholder="Author" bind:value={author}>
                    <br>
                    <textarea name="description" id="description" cols="40" rows="10" placeholder="description" bind:value={description}></textarea>
                    <br>
                    <input type="text" placeholder="link">
                    <input type="submit" value="Submit">
                </form>
            </div>

        </aside>


        <main>
            <!--Bands, top 3 songs, edit, delete -->

            <div id="posts">
                {#each [...postsDb].reverse() as post (post.id)}
                    <div class="post-container">
                        <div class="post-header">
                            <p>{post.user} {post.posted}</p>
                            <button id="liked" class="post-btn">Liked</button>
                            <button id="saved" on:click={() => savePost(post)} class="post-btn">Save</button>
                        </div>

                        <div class="post-content">
                            <h2 class="italic">{post.title} <span>by</span> {post.author}</h2>
                            <p>{post.description}</p>
                            <p><a href="{post.link}" target="_blank" >Listen to {post.title}</a></p>
                        </div>
                    </div>
                    <br>
                {/each}
            </div>
        </main>


    </div>

    <!-- <footer>
        <p class="p-footer">&copy;Fridas playlists</p>
    </footer> -->




                <!--STYLE-->

<style>
header{
    width: 100%;
    margin-bottom: 3px;
    padding: 10px 0 10px 0;
    text-align: center;
    background-color: #20242ec4;
}
nav{
    width: 100%;
    background-color: rgba(235, 248, 115, 0.507);
    height: 50px;
}
#search{
    float: right;
    padding-top: 5px;
}

#main-container{
    display: flex;
    flex-direction: row;

}


#left-aside{
    background-color: #20242ec4;
    flex: 1

}


#profile{
    padding-top: 5px;
    width: 180px;
    height: 325px;
    margin: auto;
}
#profile-img{
    width: 180px;
    height: 180px;
    border: solid black 1px;
}
#profile-text{
    width: 180px;
    height: 125px;
    border: solid black 1px;
}
#booklists{
    margin-top: 20px;
}


main{
    width: 900px;
    margin-top: 10px;
    flex: 4;
}





.post-container{
    background: #20242e;
    width: 60%;
    margin: auto;
    color: white;
}
.post-header{
    color: cadetblue;
    display: block;
    width: 100%;
    padding-bottom: 20px;

}
.post-header p{
    float: left;
}
.post-btn{
    float: right;
}


.post-content{
    width: 100%;
    height: 200px;
    text-align: center;
    display: flex;
    flex-direction: column;

}
</style>