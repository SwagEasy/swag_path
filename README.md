swag_path
=========

Get a CSS selector path to a specific element in the DOM


```javascript
window.swagPath = function (el){
  var names = [];
  while (el.parentNode){
    if (el.id){
      names.unshift('#'+el.id);
      break;
    }else{
      if (el==el.ownerDocument.documentElement) names.unshift(el.tagName);
      else{
        for (var c=1,e=el;e.previousElementSibling;e=e.previousElementSibling,c++);
        names.unshift(el.tagName+":nth-child("+c+")");
      }
      el=el.parentNode;
    }
  }
  return names.join(" > ");
}


// Try it out!
$('ul').click(function(e) {
  e.preventDefault();

  var path = swagPath( $(this)[0] );

  console.log(path);
  $(path).css({
    border: '5px solid red'
  });
});
```