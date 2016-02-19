#Dropler

###Update:

Hello, Internet! 

This was something quickly cobbled together in an hour or so to scratch an itch on my blog's admin page. So, there's a lot of stuff it won't do, wasn't made to do, wasn't planned to do, and flat out shouldn't do (like exposing S3 keys to the wild!). With said itch having been scratched, work on this has come to an end. 

In short: _It is not supported software!_

Feel free to try it out or learn from the code. Maybe it'll work well for your needs, but if it doesn't, welp, you're on your own ^_^

--------------

Dropler is a small, lightweight (and free!) CKEditor plugin for uploading images via drag and drop.  

<p align="center">
  <img src="https://cloud.githubusercontent.com/assets/1408720/7672034/0c3de41e-fcb2-11e4-96f5-06cabfd7845d.gif" />
</p> 

It's like [SimpleUploads](http://ckeditor.com/addon/simpleuploads) but free! And with fewer features! 

Dropler currently supports Imgur and Amazon's S3 as storage locations.  

##Live Demo:

You can checkout a live demo [here](http://chriskiehl.github.io/Dropler/).


--------

##Install: 

You can install it anually straight from github. 

Clone or download this respository and then follow the Manual Installation instructions from the official [CKEditor Documentation](http://docs.ckeditor.com/#!/guide/dev_plugins). Adding to CKEditor's Add-on repository pending. 

The super short version: Copy the `dropler` folder to the `plugins` directory of ckeditor. 

##Usage Instructions

First, add the plugin name to ckeditor's `extraPlugins` property inside of `config.js`:

    CKEDITOR.editorConfig = function( config ) {
      // rest of config
      config.extraPlugins = 'dropler';    <-- add the plugin
    })
    

Next, we need to supply a few configuation options depending on the backend service we're using. This is a simple javascript object consisting of 1. The name of the backend service, and 2. the settings it needs to function. 

Currently Imgur and S3 are the two upload locations supported, but, since uploading files boils down to submitting a `POST` towards the general direction of a server, new backends are trivial to implement. 

**Imgur:**

    CKEDITOR.editorConfig = function( config ) {
      // rest of config
      config.extraPlugins = 'dropler';
      
      // configure the backend service and credentials
      config.droplerConfig = {
          backend: 'imgur',
          settings: {
              clientId: 'YourImgurClientID'
          }
      }
    });
  
**AWS S3:**

    CKEDITOR.editorConfig = function( config ) {
      // rest of config
      config.extraPlugins = 'dropler';
      
      // configure the backend service and credentials
      // aws requires a few extra.. 
      config.droplerConfig = {
          backend: 's3',
          settings: {
              bucket: 'bucketname',
              region: 'your-region',
              accessKeyId: 'key',
              secretAccessKey: 'secret-key'
          }
      };
    }); 
  
**Note:** This, of course, exposes your S3 keys to the wild. So.. probably shouldn't use this outside of testing -- or for very highly trusted users (eg. yourself). 



