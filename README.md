# Facebook remove group users
## About
Facebook remove group users is a script that can be run in FireFox scratchpad that will automatically remove users from a group.

It is a JavaScript code that does nothing more than simulate the mouse clicks. You can set it running and leave it to complete. It takes appx. 10 seconds per post (so may take a while if you have been busy).

It is not perfect and a bit hacky, but at the time of coding I could not find any other working tools. 

## Usage
* Open FireFox
* Login to facebook
* Browse to your group members page
* Keep scrolling down so all the members that you want deleted are visible
* Open the scratchpad (Menu > Developer > Scratchpad)
* Paste in the JavaScript code from below
* Click run and watch as your posts are deleted

## The Code
    
    var buttons = document.querySelectorAll('[aria-label="Member Settings"]'), i;
    for (i = 0; i < buttons.length; ++i) {
        timeout = i*10000
        doSetTimeout(i, timeout);
    }
    
    function doSetTimeout(i, timeout) {
      setTimeout(function() { 
          buttons[i].scrollIntoView( true );
          window.scrollBy(0, -200);
          buttons[i].focus();
      }, timeout);
      setTimeout(function() { 
          buttons[i].click();
      }, (timeout+1000));
      setTimeout(function() { 
          owns = buttons[i].getAttribute('aria-owns');
          link = document.querySelectorAll('#'+owns+' [href^="/ajax/groups/members/remove.php"]'), i;
    
          if(link[0]){
             link[0].click();
          }
    
      }, (timeout+2000));
      setTimeout(function() { 
            if(link[0]){
                form = document.querySelectorAll('[action^="/ajax/groups/members/remove.php"] button'), i;
                form[0].click();
            }
    
       }, (timeout+4000));
    
    } 
    
# Testing
* I have tested the module on 4th October 2015 and it worked for me
* Use at your own risk, I do not offer any guarantee or warranty

# Licence
The code is released under [GNU GPL v3](http://www.gnu.org/licenses/gpl-3.0.en.html)