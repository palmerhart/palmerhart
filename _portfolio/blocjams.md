---
layout: post
title: BlocJams
feature-img: "img/sample_feature_img.png"
thumbnail-path: "https://d13yacurqjgara.cloudfront.net/users/3217/screenshots/2030966/blocjams_1x.png"
short-description: BlocJams lets you listen to the best Jams!
---

<H1>BlocJams Case Study</H1>

<h3>Summary</h3>
<p>BlocJams was created to listen to your favorite music.  The project allows you to view information about your favorite artists and listen to their albums!</p>

<h3>Explanation</h3>
<p>This music player was built for users to streaming their favorite jams from their computers of their mobile devices.  I used the bloc curriculum to create the application and listen to some cool tunes!</p>

<h3>Problem</h3>
<p>Blocjams had a number of problems to solve<p>
1.  The ability to navigate an album with user-friendly buttons, like a "next song" button.<br>
2.  Leveraging jQuery to limit the amount of code that needed to be written.

<h3>Solution</h3>
<p>To create a dynamic player bar we needed to play, pause, and navigate between songs.  Here is an exmpale of how I wrote a function to find the next song in the Album...</p>


{% highlight javascript %}
var nextSong = function() {
    var getLastSongNumber = function(index) {
        return index ==0 ? currentAlbum.songs.length : index;
    };
    
    var currentSongIndex = trackIndex(currentAlbum, currentSongFromAlbum);
    
    currentSongIndex++;
    
    
    if (currentSongFromAlbum >= currentAlbum.songs.length){
        currentSongIndex = 0;
    }    
  
    //set a new current song to currentSongFromAlbum
    setSong(currentSongIndex + 1);
    currentSoundFile.play();
    updateSeekBarWhileSongPlays();
    updatePlayerBarSong();
    
    //update player bar to show the new song
    $('.currently-playing .song-name').text(currentSongFromAlbum.title);
    $('.currently-playing .artist-name').text(currentAlbum.artist);
    $('.currently-playing .artist-song-mobile').text(currentSongFromAlbum + " - " + currentAlbum.title);
    $('.main-controls .play-pause').html(playerBarPauseButton);
    
    var lastSongNumber = getLastSongNumber(currentSongIndex);
    var $nextSongNumberCell = getSongNumberCell(currentlyPlayingSongNumber);
    var $lastSongNumberCell = getSongNumberCell(lastSongNumber);
    
    $nextSongNumberCell.html(pauseButtonTemplate);
    $lastSongNumberCell.html(lastSongNumber);       
};
{% endhighlight %}

<p>Here is an example of some jQuery that was used in a function</p>

{% highlight javascript %}
var setCurrentAlbum = function(album) {
    currentAlbum = album;
    var $albumTitle = $('.album-view-title');
    var $albumArtist = $('album-view-artist');
    var $albumReleaseInfo = $('album-view-release-info');
    var $albumImage = $('.album-cover-art');
    var $albumSongList = $('.album-view-song-list');
    // #2
    $albumTitle.text(album.title);
    $albumArtist.text(album.artist);
    $albumReleaseInfo.text(album.year + ' ' + album.label);
    $albumImage.attr('src', album.albumArtUrl);
    //#3
    $albumSongList.empty();
    // #4
    for (var i=0; i < album.songs.length; i++) {
        var $newRow = createSongRow(i + 1, album.songs[i].title, album.songs[i].duration);
        $albumSongList.append($newRow);
    }
};
{% endhighlight %}

<h3>Results</h3>
<p>Here is a screenshot of the finished page with the most engagement, where users listen to their favorite music!</p>
<img src="{{ site.baseurl }}/img/bloc-jams_album.png" />

<h3>Conclusion</h3>
<p>I was able to deliver a fun and lightweight application to listen to your favorite tunes by computer or mobile!  Jam on!</p>