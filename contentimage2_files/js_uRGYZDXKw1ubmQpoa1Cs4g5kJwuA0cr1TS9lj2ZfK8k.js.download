(function ($) { Drupal.behaviors.scsocial = { attach:function (context) {

$('.ig-wrapper').each(function(){
  var wrap = $(this),
      igs = $('.instagrams'),
      nid = wrap.attr('data-nid'),
      allIDs = new Array(),
      currentIDs = new Array(),
      num = 10;

      if($('.ig-wrapper').attr("id") == "instafeed-santa-cruz") {
        var sc = true;
      }
      else if ($('.ig-wrapper').attr("id") == "instafeed-juliana") {
        var sc = false;
        num = 18;
      }
      //news or home page
      if(nid == 0) {
         path = '/igjson';
         num = 8;
      }
      else {
         path = '/node/'+nid+'/igjson';
         alert($path);
      }
      getRandom = function(){
          var id = allIDs[Math.floor(Math.random()*allIDs.length)];
          if($.inArray(id, currentIDs) != -1) {
            return getRandom();
          } else {
            currentIDs.push(id);
            return id;
          }
      },
      makeLinkedImage = function(item) {
          if(item.link !== undefined) return '<div class="share-block"><div class="share-block__image--ratio-1x1"><a class="share-block__link" data-id="'+item.id+'" href="'+item.link+'" target="_blank" title="'+item.truncated+'"><div class="share-block__image" style="background-image:url(\''+item.image+'\');"></div></a></div></div>';
      },
      makeImage = function(item) {
          if(nid == 0) {
              if(sc) {
                return '<div><img src="'+item.image+'" alt="'+item.truncated+'" /></div><div class="msg"><h3>'+item.truncated_long+'</h3><span class="ctalink">Full Story</span></div>';
              }
              else {
                return '<div class="square-image"><img src="'+item.image+'" alt="'+item.truncated+'" /></div><div class="msg"><h3>'+item.created_date+'</h3><p>'+item.truncated_long+'</p><span class="ctalink">Read More &gt;</span></div>';
              }
              
          }
          else {
              return '<img src="'+item.image+'" alt="'+item.truncated+'" />';
          }
          
      },
      swapImage = function(){
      
      };
  
  $.getJSON(path, function(data) {
    var igs = data.instagrams;
    if(!igs.length) {
      wrap.parent().remove();
      return;
    }
    for(var i in igs) { allIDs.push(i); }
    
    for(var j = 0; j < num; j++) {
      var item = getRandom();
      igs[item].id = item;
      var img = makeLinkedImage(igs[item]);
      wrap.append(img);
    }
    
    function randomSwap() {
      var swap = wrap.find('a').eq(Math.round(Math.random()*10));
      var swap_img = swap.find('img').first();
      
      var oldID = swap.attr('data-id');
      var newID = getRandom();
      var item = igs[newID];
      item.id = newID;
      var new_img = makeImage(item);
      swap.css({position: 'relative', 'overflow':'hidden'});
      
      swap_img.css({position: 'absolute', left: 0, top: 0, right: 0, bottom: 0, 'z-index': 3});
      swap.append(new_img);
      new_img = swap.find('img').last();
      
      speed = (Math.round(Math.random()*10000))/2;
      if(speed < 1000) speed = 1000;
      if(speed > 6000) speed = 6000;
      swap_img.fadeOut(speed, function(){
        swap_img.remove();
        new_img.attr('style', '');
        swap.attr({'style': '', 'href': item.link, 'data-id': item.id, 'title': item.truncated});
        var index = currentIDs.indexOf(oldID);
        currentIDs.splice(index, 1);
        currentIDs.push(newID);
        randomSwap();
      });
      
    }
    if(nid != 0) {
    //  randomSwap();
    }
    
  });
  
});

} }; })(jQuery);;
