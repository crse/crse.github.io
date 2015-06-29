/* For the "inset" look only */
html {
    overflow: auto;
}
body {
    position: absolute;
    top: 20px;
    left: 20px;
    bottom: 20px;
    right: 20px;
    padding: 30px; 
    overflow-y: scroll;
    overflow-x: hidden;
}

/* Let's get this party started */
::-webkit-scrollbar {
    width: 12px;
}
 
/* Track */
::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3); 
    -webkit-border-radius: 10px;
    border-radius: 10px;
}
 
/* Handle */
::-webkit-scrollbar-thumb {
    -webkit-border-radius: 10px;
    border-radius: 10px;
    background: rgba(255,0,0,0.8); 
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.5); 
}
::-webkit-scrollbar-thumb:window-inactive {
	background: rgba(255,0,0,0.4); 
}








<script>
    function changeSize() {
        var width = parseInt($("#Width").val());
        var height = parseInt($("#Height").val());

        if(!width || isNaN(width)) {
            width = 600;
        }
        if(!height || isNaN(height)) {
            height = 400;
        }
        $("#Demo").width(width).height(height);

        // update perfect scrollbar
        $('#Demo').perfectScrollbar('update');
    }
    $(function() {
        $('#Demo').perfectScrollbar();
    });
</script>









HTML
Control.ScrollBar requires a very particular HTML structure. There must be a positioned outer container, with the track and scrollable container as direct children. The track must contain a single div (with any id or class name). You do not reference the outer container or handle when calling initialize(), only the scrollable content, and the track. The scrollable content must have it's overflow property set to hidden.

<div id="scrollbar_container">  
    <div id="scrollbar_track"><div id="scrollbar_handle"></div></div>  
    <div id="scrollbar_content">...</div>  
</div>  
JavaScript
var scrollbar = new Control.ScrollBar('scrollbar_content','scrollbar_track');  
  
$('scroll_down_50').observe('click',function(event){  
    scrollbar.scrollBy(-50);  
    event.stop();  
});  
  
$('scroll_up_50').observe('click',function(event){  
    scrollbar.scrollBy(50);  
    event.stop();  
});  
  
$('scroll_top').observe('click',function(event){  
    scrollbar.scrollTo('top');  
    event.stop();  
});  
  
$('scroll_bottom').observe('click',function(event){  
    //to animate a scroll operation you can pass true  
    //or a callback that will be called when scrolling is complete  
    scrollbar.scrollTo('bottom',function(){  
        if(typeof(console) != "undefined")  
            console.log('Finished scrolling to bottom.');  
    });  
    event.stop();  
});  
  
$('scroll_second').observe('click',function(event){  
    //you can pass a number or element to scroll to  
    //if you pass an element, it will be centered, unless it is  
    //near the bottom of the container  
    scrollbar.scrollTo($('second_subhead'));  
    event.stop();  
});  
  
$('scroll_third').observe('click',function(event){  
    //passing true will animate the scroll  
    scrollbar.scrollTo($('third_subhead'),true);  
    event.stop();  
});  
  
$('scroll_insert').observe('click',function(event){  
    $('scrollbar_content').insert('<p><b>Inserted: ' + $('repeat').innerHTML + '</b></p>');  
    //you only need to call this if ajax or dom operations modify the layout  
    //this is automatically called when the window resizes  
    scrollbar.recalculateLayout();  
    event.stop();  
});  
CSS
#scrollbar_container {  
    position:relative;  
    width:500px;  
} 
 
#scrollbar_track {  
    position:absolute;  
    top:0;  
    rightright:0;  
    height:100%;  
    width:10px;  
    background-color:transparent;  
    cursor:move;  
} 
 
#scrollbar_handle {  
    width:10px;  
    background-color:#5c92e7;  
    cursor:move;  
    -moz-border-radius: 5px;  
    -webkit-border-radius: 5px;  
    opacity:0.9;  
    -moz-opacity:0.9;  
} 
 
#scrollbar_content {  
    overflow:hidden;  
    width:485px;  
    height:250px;  
}  