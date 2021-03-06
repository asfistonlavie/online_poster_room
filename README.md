# Online Poster Room

The Online Poster Room is a virtual room on a web page that displays (scientific)
poster thumbnails with links to full poster and a meeting room. This application
has been initially developped for JOBIM 2020 bioinformatics conference as the
event has been turned into a virtual form due to COVID-19.

## Example Demo
[JOBIM 2020 Virtual Poster Room](https://jobim2020.sciencesconf.org/resource/page/id/23)

## Getting Started

Download or clone the project. Only 3 files are used: poster_room.js,
poster_room.css and poster_room.json. These files should be made accessible to
the clients of the poster room.
* poster_room.js: contains the Javascript code use to generate the room;
* poster_room.css: contains the CSS code used to display the room well;
* poster_room.json: contains the poster room configuration and poster data.

### Prerequisites

The Online Poster Room requires jQuery > 1.7 to generate the poster room. Then,
poster thumbnails should be generated by a third party application. Finally,
poster meeting rooms are managed by an external application such as Jitsi Meet
(https://meet.jit.si/).

### Installing

To use the online poster room, you must have the files poster_room.js,
poster_room.css and poster_room.json accessible through the web by poster room
clients and you will have to create a web page with a code similar to the
following one:

```
  ...
  <head>
    ...
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script src="poster_room.js"></script>
    <link rel="stylesheet" type="text/css" href="poster_room.css">
    ...
  </head>
  <body>
    ...
    <div id="online_poster_room_browser">&nbsp;</div>
    <script type="text/javascript">// <![CDATA[
      var opr = {poster_show: false, lang: 'en'};
      $(function () {
        $.getJSON("poster_room.json", function(json_data) {
          opr = json_data;
        })
        .fail(function (jqxhr, textStatus, error) {
          var err = textStatus + ", " + error;
          console.log('Failed to load JSON data: ' + err);
        })
        .always(function () {
          init_online_poster_room(opr);
        });
      });
    // ]]></script>
    ...
  </body>
  ...
```

If you use a CMS and have restricted access to the HTML header, you can try the
following (assuming jQuery is available):

```
<div id="online_poster_room_browser">&nbsp;</div>
<script type="text/javascript" src="https://your.site.web/path_to/poster_room.js"></script>
<script type="text/javascript">// <![CDATA[
// Add style sheet.
var css = "https://your.site.web/path_to/poster_room.css";
$.get(css, function(data) {
  $("<style type=\"text/css\">" + data + "</style>").appendTo(document.head);
});
// Init settings.
var opr = {poster_show: true, lang: 'en'};
// Get data.
$.getJSON("/path_to/poster_room.json", function(json_data) {
  opr = json_data;
});
// Start room.
$(function () {
  init_online_poster_room(opr);
});
// ]]></script>
```

## Contributing

You can contribute on GitHub: https://github.com/guignonv/online_poster_room

## Versioning

We use [SemVer](http://semver.org/) for versioning.
For the versions available, see the [tags on this repository]
(https://github.com/guignonv/online_poster_room/tags).

## Authors

* **Valentin Guignon** - *Initial work* - [guignonv](https://github.com/guignonv)

See also the list of
[contributors](https://github.com/guignonv/online_poster_room/contributors)
who participated in this project.

## License

This project is licensed under GNU GPLv3 - see the [COPYING](COPYING) file for
details

## Acknowledgments

* JOBIM Organizing Committee and Program Committee for review.
* The Alliance Bioversity International - CIAT (a CGIAR center).
