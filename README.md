amara-embeds-for-wordpress
==========================

Amara Embed Plugin for WordPress.

See amara-embeds-for-wordpress.php file's inline documentation for full details. 

Using the plugin
----------------

Installing this plugin won't do anything visible at first, but will allow you to convert a normal [embed] shortcode into the Amara/Universal Subtitles embed code by adding amara="1" inside the shortcode. For example:

[embed amara="1"]http://www.youtube.com/watch?v=LbUGRcuA16E[/embed]

When the plugin is enabled, that code will load the Amara embed code for the YouTube video at that URL. Without the plugin the video will still be loaded, but not the Amara subtitles.


The Problem
------------

The Amara embed code does not work well with WordPress. In the HTML/Text editor it doesn't work by default but can be fixed by removing whitespace. In the Visual/WYSIWYG editor it doesn't work at all because it is mangled by the HTML filters. This makes it almost impossible to embed your subtitled videos inside posts.

Amara's embed code does work if it's added outside the post content, so a WordPress [shortcode] is the obvious choice for getting the embed into your posts. A pure [amara] shortcode would work, but if their service went down the entire video would be broken rather than just the subtitles. 

The Solution
----------------

The solution used by this plugin is to let you insert the original source video into your post as a normal embed URL, surrounded by an [embed amara="1"] shortcode, then replace the default embed with the Amara version at load time.

Normally a URL in a post on it's own line, or wrapped in the [embed] code (they are equivalent), is automatically replaced by the oEmbed output from the video provider (an iframe or whatever the provider uses) when the post is viewed on the frontend. This saves the author from having to deal with all the messy javascript etc. in the embed. 

All the major video hosts Amara uses offer this service, so their videos already work by default as [embed] URLs. 

The way this plugin works is to filter the output of the [embed] shortcode and, if the "amara" attribute is present, replace the output with the Amara container code outlined in their API:

https://github.com/pculture/unisubs/wiki/Embed-Code-Usage-Guide

If Amara ever stops working then you can disable this plugin and all your videos will stop working(albeit without the subtitles). Alternately, if you don't want the videos to show without their subtitles, you can edit the plugin to make it output an error. 
