# HOG-opencv
Steps to train your custom HOG descriptor


<!DOCTYPE html>
<html>
<head><meta charset="utf-8" />

<title>HOG-github</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>



<style type="text/css">
    /*!
*
* Twitter Bootstrap
*
*/
/*!
 * Bootstrap v3.3.7 (http://getbootstrap.com)
 * Copyright 2011-2016 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 */
/*! normalize.css v3.0.3 | MIT License | github.com/necolas/normalize.css */
html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
body {
  margin: 0;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
}
audio,
canvas,
progress,
video {
  display: inline-block;
  vertical-align: baseline;
}
audio:not([controls]) {
  display: none;
  height: 0;
}
[hidden],
template {
  display: none;
}
a {
  background-color: transparent;
}
a:active,
a:hover {
  outline: 0;
}
abbr[title] {
  border-bottom: 1px dotted;
}
b,
strong {
  font-weight: bold;
}
dfn {
  font-style: italic;
}
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
mark {
  background: #ff0;
  color: #000;
}
small {
  font-size: 80%;
}
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}
sup {
  top: -0.5em;
}
sub {
  bottom: -0.25em;
}
img {
  border: 0;
}
svg:not(:root) {
  overflow: hidden;
}
figure {
  margin: 1em 40px;
}
hr {
  box-sizing: content-box;
  height: 0;
}
pre {
  overflow: auto;
}
code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}
button,
input,
optgroup,
select,
textarea {
  color: inherit;
  font: inherit;
  margin: 0;
}
button {
  overflow: visible;
}
button,
select {
  text-transform: none;
}
button,
html input[type="button"],
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button;
  cursor: pointer;
}
button[disabled],
html input[disabled] {
  cursor: default;
}
button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}
input {
  line-height: normal;
}
input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box;
  padding: 0;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: textfield;
  box-sizing: content-box;
}
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}
fieldset {
  border: 1px solid #c0c0c0;
  margin: 0 2px;
  padding: 0.35em 0.625em 0.75em;
}
legend {
  border: 0;
  padding: 0;
}
textarea {
  overflow: auto;
}
optgroup {
  font-weight: bold;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
td,
th {
  padding: 0;
}
/*! Source: https://github.com/h5bp/html5-boilerplate/blob/master/src/css/main.css */
@media print {
  *,
  *:before,
  *:after {
    background: transparent !important;
    box-shadow: none !important;
    text-shadow: none !important;
  }
  a,
  a:visited {
    text-decoration: underline;
  }
  a[href]:after {
    content: " (" attr(href) ")";
  }
  abbr[title]:after {
    content: " (" attr(title) ")";
  }
  a[href^="#"]:after,
  a[href^="javascript:"]:after {
    content: "";
  }
  pre,
  blockquote {
    border: 1px solid #999;
    page-break-inside: avoid;
  }
  thead {
    display: table-header-group;
  }
  tr,
  img {
    page-break-inside: avoid;
  }
  img {
    max-width: 100% !important;
  }
  p,
  h2,
  h3 {
    orphans: 3;
    widows: 3;
  }
  h2,
  h3 {
    page-break-after: avoid;
  }
  .navbar {
    display: none;
  }
  .btn > .caret,
  .dropup > .btn > .caret {
    border-top-color: #000 !important;
  }
  .label {
    border: 1px solid #000;
  }
  .table {
    border-collapse: collapse !important;
  }
  .table td,
  .table th {
    background-color: #fff !important;
  }
  .table-bordered th,
  .table-bordered td {
    border: 1px solid #ddd !important;
  }
}
@font-face {
  font-family: 'Glyphicons Halflings';
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot');
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot?#iefix') format('embedded-opentype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff2') format('woff2'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff') format('woff'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.ttf') format('truetype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular') format('svg');
}
.glyphicon {
  position: relative;
  top: 1px;
  display: inline-block;
  font-family: 'Glyphicons Halflings';
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.glyphicon-asterisk:before {
  content: "\002a";
}
.glyphicon-plus:before {
  content: "\002b";
}
.glyphicon-euro:before,
.glyphicon-eur:before {
  content: "\20ac";
}
.glyphicon-minus:before {
  content: "\2212";
}
.glyphicon-cloud:before {
  content: "\2601";
}
.glyphicon-envelope:before {
  content: "\2709";
}
.glyphicon-pencil:before {
  content: "\270f";
}
.glyphicon-glass:before {
  content: "\e001";
}
.glyphicon-music:before {
  content: "\e002";
}
.glyphicon-search:before {
  content: "\e003";
}
.glyphicon-heart:before {
  content: "\e005";
}
.glyphicon-star:before {
  content: "\e006";
}
.glyphicon-star-empty:before {
  content: "\e007";
}
.glyphicon-user:before {
  content: "\e008";
}
.glyphicon-film:before {
  content: "\e009";
}
.glyphicon-th-large:before {
  content: "\e010";
}
.glyphicon-th:before {
  content: "\e011";
}
.glyphicon-th-list:before {
  content: "\e012";
}
.glyphicon-ok:before {
  content: "\e013";
}
.glyphicon-remove:before {
  content: "\e014";
}
.glyphicon-zoom-in:before {
  content: "\e015";
}
.glyphicon-zoom-out:before {
  content: "\e016";
}
.glyphicon-off:before {
  content: "\e017";
}
.glyphicon-signal:before {
  content: "\e018";
}
.glyphicon-cog:before {
  content: "\e019";
}
.glyphicon-trash:before {
  content: "\e020";
}
.glyphicon-home:before {
  content: "\e021";
}
.glyphicon-file:before {
  content: "\e022";
}
.glyphicon-time:before {
  content: "\e023";
}
.glyphicon-road:before {
  content: "\e024";
}
.glyphicon-download-alt:before {
  content: "\e025";
}
.glyphicon-download:before {
  content: "\e026";
}
.glyphicon-upload:before {
  content: "\e027";
}
.glyphicon-inbox:before {
  content: "\e028";
}
.glyphicon-play-circle:before {
  content: "\e029";
}
.glyphicon-repeat:before {
  content: "\e030";
}
.glyphicon-refresh:before {
  content: "\e031";
}
.glyphicon-list-alt:before {
  content: "\e032";
}
.glyphicon-lock:before {
  content: "\e033";
}
.glyphicon-flag:before {
  content: "\e034";
}
.glyphicon-headphones:before {
  content: "\e035";
}
.glyphicon-volume-off:before {
  content: "\e036";
}
.glyphicon-volume-down:before {
  content: "\e037";
}
.glyphicon-volume-up:before {
  content: "\e038";
}
.glyphicon-qrcode:before {
  content: "\e039";
}
.glyphicon-barcode:before {
  content: "\e040";
}
.glyphicon-tag:before {
  content: "\e041";
}
.glyphicon-tags:before {
  content: "\e042";
}
.glyphicon-book:before {
  content: "\e043";
}
.glyphicon-bookmark:before {
  content: "\e044";
}
.glyphicon-print:before {
  content: "\e045";
}
.glyphicon-camera:before {
  content: "\e046";
}
.glyphicon-font:before {
  content: "\e047";
}
.glyphicon-bold:before {
  content: "\e048";
}
.glyphicon-italic:before {
  content: "\e049";
}
.glyphicon-text-height:before {
  content: "\e050";
}
.glyphicon-text-width:before {
  content: "\e051";
}
.glyphicon-align-left:before {
  content: "\e052";
}
.glyphicon-align-center:before {
  content: "\e053";
}
.glyphicon-align-right:before {
  content: "\e054";
}
.glyphicon-align-justify:before {
  content: "\e055";
}
.glyphicon-list:before {
  content: "\e056";
}
.glyphicon-indent-left:before {
  content: "\e057";
}
.glyphicon-indent-right:before {
  content: "\e058";
}
.glyphicon-facetime-video:before {
  content: "\e059";
}
.glyphicon-picture:before {
  content: "\e060";
}
.glyphicon-map-marker:before {
  content: "\e062";
}
.glyphicon-adjust:before {
  content: "\e063";
}
.glyphicon-tint:before {
  content: "\e064";
}
.glyphicon-edit:before {
  content: "\e065";
}
.glyphicon-share:before {
  content: "\e066";
}
.glyphicon-check:before {
  content: "\e067";
}
.glyphicon-move:before {
  content: "\e068";
}
.glyphicon-step-backward:before {
  content: "\e069";
}
.glyphicon-fast-backward:before {
  content: "\e070";
}
.glyphicon-backward:before {
  content: "\e071";
}
.glyphicon-play:before {
  content: "\e072";
}
.glyphicon-pause:before {
  content: "\e073";
}
.glyphicon-stop:before {
  content: "\e074";
}
.glyphicon-forward:before {
  content: "\e075";
}
.glyphicon-fast-forward:before {
  content: "\e076";
}
.glyphicon-step-forward:before {
  content: "\e077";
}
.glyphicon-eject:before {
  content: "\e078";
}
.glyphicon-chevron-left:before {
  content: "\e079";
}
.glyphicon-chevron-right:before {
  content: "\e080";
}
.glyphicon-plus-sign:before {
  content: "\e081";
}
.glyphicon-minus-sign:before {
  content: "\e082";
}
.glyphicon-remove-sign:before {
  content: "\e083";
}
.glyphicon-ok-sign:before {
  content: "\e084";
}
.glyphicon-question-sign:before {
  content: "\e085";
}
.glyphicon-info-sign:before {
  content: "\e086";
}
.glyphicon-screenshot:before {
  content: "\e087";
}
.glyphicon-remove-circle:before {
  content: "\e088";
}
.glyphicon-ok-circle:before {
  content: "\e089";
}
.glyphicon-ban-circle:before {
  content: "\e090";
}
.glyphicon-arrow-left:before {
  content: "\e091";
}
.glyphicon-arrow-right:before {
  content: "\e092";
}
.glyphicon-arrow-up:before {
  content: "\e093";
}
.glyphicon-arrow-down:before {
  content: "\e094";
}
.glyphicon-share-alt:before {
  content: "\e095";
}
.glyphicon-resize-full:before {
  content: "\e096";
}
.glyphicon-resize-small:before {
  content: "\e097";
}
.glyphicon-exclamation-sign:before {
  content: "\e101";
}
.glyphicon-gift:before {
  content: "\e102";
}
.glyphicon-leaf:before {
  content: "\e103";
}
.glyphicon-fire:before {
  content: "\e104";
}
.glyphicon-eye-open:before {
  content: "\e105";
}
.glyphicon-eye-close:before {
  content: "\e106";
}
.glyphicon-warning-sign:before {
  content: "\e107";
}
.glyphicon-plane:before {
  content: "\e108";
}
.glyphicon-calendar:before {
  content: "\e109";
}
.glyphicon-random:before {
  content: "\e110";
}
.glyphicon-comment:before {
  content: "\e111";
}
.glyphicon-magnet:before {
  content: "\e112";
}
.glyphicon-chevron-up:before {
  content: "\e113";
}
.glyphicon-chevron-down:before {
  content: "\e114";
}
.glyphicon-retweet:before {
  content: "\e115";
}
.glyphicon-shopping-cart:before {
  content: "\e116";
}
.glyphicon-folder-close:before {
  content: "\e117";
}
.glyphicon-folder-open:before {
  content: "\e118";
}
.glyphicon-resize-vertical:before {
  content: "\e119";
}
.glyphicon-resize-horizontal:before {
  content: "\e120";
}
.glyphicon-hdd:before {
  content: "\e121";
}
.glyphicon-bullhorn:before {
  content: "\e122";
}
.glyphicon-bell:before {
  content: "\e123";
}
.glyphicon-certificate:before {
  content: "\e124";
}
.glyphicon-thumbs-up:before {
  content: "\e125";
}
.glyphicon-thumbs-down:before {
  content: "\e126";
}
.glyphicon-hand-right:before {
  content: "\e127";
}
.glyphicon-hand-left:before {
  content: "\e128";
}
.glyphicon-hand-up:before {
  content: "\e129";
}
.glyphicon-hand-down:before {
  content: "\e130";
}
.glyphicon-circle-arrow-right:before {
  content: "\e131";
}
.glyphicon-circle-arrow-left:before {
  content: "\e132";
}
.glyphicon-circle-arrow-up:before {
  content: "\e133";
}
.glyphicon-circle-arrow-down:before {
  content: "\e134";
}
.glyphicon-globe:before {
  content: "\e135";
}
.glyphicon-wrench:before {
  content: "\e136";
}
.glyphicon-tasks:before {
  content: "\e137";
}
.glyphicon-filter:before {
  content: "\e138";
}
.glyphicon-briefcase:before {
  content: "\e139";
}
.glyphicon-fullscreen:before {
  content: "\e140";
}
.glyphicon-dashboard:before {
  content: "\e141";
}
.glyphicon-paperclip:before {
  content: "\e142";
}
.glyphicon-heart-empty:before {
  content: "\e143";
}
.glyphicon-link:before {
  content: "\e144";
}
.glyphicon-phone:before {
  content: "\e145";
}
.glyphicon-pushpin:before {
  content: "\e146";
}
.glyphicon-usd:before {
  content: "\e148";
}
.glyphicon-gbp:before {
  content: "\e149";
}
.glyphicon-sort:before {
  content: "\e150";
}
.glyphicon-sort-by-alphabet:before {
  content: "\e151";
}
.glyphicon-sort-by-alphabet-alt:before {
  content: "\e152";
}
.glyphicon-sort-by-order:before {
  content: "\e153";
}
.glyphicon-sort-by-order-alt:before {
  content: "\e154";
}
.glyphicon-sort-by-attributes:before {
  content: "\e155";
}
.glyphicon-sort-by-attributes-alt:before {
  content: "\e156";
}
.glyphicon-unchecked:before {
  content: "\e157";
}
.glyphicon-expand:before {
  content: "\e158";
}
.glyphicon-collapse-down:before {
  content: "\e159";
}
.glyphicon-collapse-up:before {
  content: "\e160";
}
.glyphicon-log-in:before {
  content: "\e161";
}
.glyphicon-flash:before {
  content: "\e162";
}
.glyphicon-log-out:before {
  content: "\e163";
}
.glyphicon-new-window:before {
  content: "\e164";
}
.glyphicon-record:before {
  content: "\e165";
}
.glyphicon-save:before {
  content: "\e166";
}
.glyphicon-open:before {
  content: "\e167";
}
.glyphicon-saved:before {
  content: "\e168";
}
.glyphicon-import:before {
  content: "\e169";
}
.glyphicon-export:before {
  content: "\e170";
}
.glyphicon-send:before {
  content: "\e171";
}
.glyphicon-floppy-disk:before {
  content: "\e172";
}
.glyphicon-floppy-saved:before {
  content: "\e173";
}
.glyphicon-floppy-remove:before {
  content: "\e174";
}
.glyphicon-floppy-save:before {
  content: "\e175";
}
.glyphicon-floppy-open:before {
  content: "\e176";
}
.glyphicon-credit-card:before {
  content: "\e177";
}
.glyphicon-transfer:before {
  content: "\e178";
}
.glyphicon-cutlery:before {
  content: "\e179";
}
.glyphicon-header:before {
  content: "\e180";
}
.glyphicon-compressed:before {
  content: "\e181";
}
.glyphicon-earphone:before {
  content: "\e182";
}
.glyphicon-phone-alt:before {
  content: "\e183";
}
.glyphicon-tower:before {
  content: "\e184";
}
.glyphicon-stats:before {
  content: "\e185";
}
.glyphicon-sd-video:before {
  content: "\e186";
}
.glyphicon-hd-video:before {
  content: "\e187";
}
.glyphicon-subtitles:before {
  content: "\e188";
}
.glyphicon-sound-stereo:before {
  content: "\e189";
}
.glyphicon-sound-dolby:before {
  content: "\e190";
}
.glyphicon-sound-5-1:before {
  content: "\e191";
}
.glyphicon-sound-6-1:before {
  content: "\e192";
}
.glyphicon-sound-7-1:before {
  content: "\e193";
}
.glyphicon-copyright-mark:before {
  content: "\e194";
}
.glyphicon-registration-mark:before {
  content: "\e195";
}
.glyphicon-cloud-download:before {
  content: "\e197";
}
.glyphicon-cloud-upload:before {
  content: "\e198";
}
.glyphicon-tree-conifer:before {
  content: "\e199";
}
.glyphicon-tree-deciduous:before {
  content: "\e200";
}
.glyphicon-cd:before {
  content: "\e201";
}
.glyphicon-save-file:before {
  content: "\e202";
}
.glyphicon-open-file:before {
  content: "\e203";
}
.glyphicon-level-up:before {
  content: "\e204";
}
.glyphicon-copy:before {
  content: "\e205";
}
.glyphicon-paste:before {
  content: "\e206";
}
.glyphicon-alert:before {
  content: "\e209";
}
.glyphicon-equalizer:before {
  content: "\e210";
}
.glyphicon-king:before {
  content: "\e211";
}
.glyphicon-queen:before {
  content: "\e212";
}
.glyphicon-pawn:before {
  content: "\e213";
}
.glyphicon-bishop:before {
  content: "\e214";
}
.glyphicon-knight:before {
  content: "\e215";
}
.glyphicon-baby-formula:before {
  content: "\e216";
}
.glyphicon-tent:before {
  content: "\26fa";
}
.glyphicon-blackboard:before {
  content: "\e218";
}
.glyphicon-bed:before {
  content: "\e219";
}
.glyphicon-apple:before {
  content: "\f8ff";
}
.glyphicon-erase:before {
  content: "\e221";
}
.glyphicon-hourglass:before {
  content: "\231b";
}
.glyphicon-lamp:before {
  content: "\e223";
}
.glyphicon-duplicate:before {
  content: "\e224";
}
.glyphicon-piggy-bank:before {
  content: "\e225";
}
.glyphicon-scissors:before {
  content: "\e226";
}
.glyphicon-bitcoin:before {
  content: "\e227";
}
.glyphicon-btc:before {
  content: "\e227";
}
.glyphicon-xbt:before {
  content: "\e227";
}
.glyphicon-yen:before {
  content: "\00a5";
}
.glyphicon-jpy:before {
  content: "\00a5";
}
.glyphicon-ruble:before {
  content: "\20bd";
}
.glyphicon-rub:before {
  content: "\20bd";
}
.glyphicon-scale:before {
  content: "\e230";
}
.glyphicon-ice-lolly:before {
  content: "\e231";
}
.glyphicon-ice-lolly-tasted:before {
  content: "\e232";
}
.glyphicon-education:before {
  content: "\e233";
}
.glyphicon-option-horizontal:before {
  content: "\e234";
}
.glyphicon-option-vertical:before {
  content: "\e235";
}
.glyphicon-menu-hamburger:before {
  content: "\e236";
}
.glyphicon-modal-window:before {
  content: "\e237";
}
.glyphicon-oil:before {
  content: "\e238";
}
.glyphicon-grain:before {
  content: "\e239";
}
.glyphicon-sunglasses:before {
  content: "\e240";
}
.glyphicon-text-size:before {
  content: "\e241";
}
.glyphicon-text-color:before {
  content: "\e242";
}
.glyphicon-text-background:before {
  content: "\e243";
}
.glyphicon-object-align-top:before {
  content: "\e244";
}
.glyphicon-object-align-bottom:before {
  content: "\e245";
}
.glyphicon-object-align-horizontal:before {
  content: "\e246";
}
.glyphicon-object-align-left:before {
  content: "\e247";
}
.glyphicon-object-align-vertical:before {
  content: "\e248";
}
.glyphicon-object-align-right:before {
  content: "\e249";
}
.glyphicon-triangle-right:before {
  content: "\e250";
}
.glyphicon-triangle-left:before {
  content: "\e251";
}
.glyphicon-triangle-bottom:before {
  content: "\e252";
}
.glyphicon-triangle-top:before {
  content: "\e253";
}
.glyphicon-console:before {
  content: "\e254";
}
.glyphicon-superscript:before {
  content: "\e255";
}
.glyphicon-subscript:before {
  content: "\e256";
}
.glyphicon-menu-left:before {
  content: "\e257";
}
.glyphicon-menu-right:before {
  content: "\e258";
}
.glyphicon-menu-down:before {
  content: "\e259";
}
.glyphicon-menu-up:before {
  content: "\e260";
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
*:before,
*:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
html {
  font-size: 10px;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 13px;
  line-height: 1.42857143;
  color: #000;
  background-color: #fff;
}
input,
button,
select,
textarea {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
a {
  color: #337ab7;
  text-decoration: none;
}
a:hover,
a:focus {
  color: #23527c;
  text-decoration: underline;
}
a:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
figure {
  margin: 0;
}
img {
  vertical-align: middle;
}
.img-responsive,
.thumbnail > img,
.thumbnail a > img,
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  display: block;
  max-width: 100%;
  height: auto;
}
.img-rounded {
  border-radius: 3px;
}
.img-thumbnail {
  padding: 4px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
  display: inline-block;
  max-width: 100%;
  height: auto;
}
.img-circle {
  border-radius: 50%;
}
hr {
  margin-top: 18px;
  margin-bottom: 18px;
  border: 0;
  border-top: 1px solid #eeeeee;
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
[role="button"] {
  cursor: pointer;
}
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  font-family: inherit;
  font-weight: 500;
  line-height: 1.1;
  color: inherit;
}
h1 small,
h2 small,
h3 small,
h4 small,
h5 small,
h6 small,
.h1 small,
.h2 small,
.h3 small,
.h4 small,
.h5 small,
.h6 small,
h1 .small,
h2 .small,
h3 .small,
h4 .small,
h5 .small,
h6 .small,
.h1 .small,
.h2 .small,
.h3 .small,
.h4 .small,
.h5 .small,
.h6 .small {
  font-weight: normal;
  line-height: 1;
  color: #777777;
}
h1,
.h1,
h2,
.h2,
h3,
.h3 {
  margin-top: 18px;
  margin-bottom: 9px;
}
h1 small,
.h1 small,
h2 small,
.h2 small,
h3 small,
.h3 small,
h1 .small,
.h1 .small,
h2 .small,
.h2 .small,
h3 .small,
.h3 .small {
  font-size: 65%;
}
h4,
.h4,
h5,
.h5,
h6,
.h6 {
  margin-top: 9px;
  margin-bottom: 9px;
}
h4 small,
.h4 small,
h5 small,
.h5 small,
h6 small,
.h6 small,
h4 .small,
.h4 .small,
h5 .small,
.h5 .small,
h6 .small,
.h6 .small {
  font-size: 75%;
}
h1,
.h1 {
  font-size: 33px;
}
h2,
.h2 {
  font-size: 27px;
}
h3,
.h3 {
  font-size: 23px;
}
h4,
.h4 {
  font-size: 17px;
}
h5,
.h5 {
  font-size: 13px;
}
h6,
.h6 {
  font-size: 12px;
}
p {
  margin: 0 0 9px;
}
.lead {
  margin-bottom: 18px;
  font-size: 14px;
  font-weight: 300;
  line-height: 1.4;
}
@media (min-width: 768px) {
  .lead {
    font-size: 19.5px;
  }
}
small,
.small {
  font-size: 92%;
}
mark,
.mark {
  background-color: #fcf8e3;
  padding: .2em;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}
.text-nowrap {
  white-space: nowrap;
}
.text-lowercase {
  text-transform: lowercase;
}
.text-uppercase {
  text-transform: uppercase;
}
.text-capitalize {
  text-transform: capitalize;
}
.text-muted {
  color: #777777;
}
.text-primary {
  color: #337ab7;
}
a.text-primary:hover,
a.text-primary:focus {
  color: #286090;
}
.text-success {
  color: #3c763d;
}
a.text-success:hover,
a.text-success:focus {
  color: #2b542c;
}
.text-info {
  color: #31708f;
}
a.text-info:hover,
a.text-info:focus {
  color: #245269;
}
.text-warning {
  color: #8a6d3b;
}
a.text-warning:hover,
a.text-warning:focus {
  color: #66512c;
}
.text-danger {
  color: #a94442;
}
a.text-danger:hover,
a.text-danger:focus {
  color: #843534;
}
.bg-primary {
  color: #fff;
  background-color: #337ab7;
}
a.bg-primary:hover,
a.bg-primary:focus {
  background-color: #286090;
}
.bg-success {
  background-color: #dff0d8;
}
a.bg-success:hover,
a.bg-success:focus {
  background-color: #c1e2b3;
}
.bg-info {
  background-color: #d9edf7;
}
a.bg-info:hover,
a.bg-info:focus {
  background-color: #afd9ee;
}
.bg-warning {
  background-color: #fcf8e3;
}
a.bg-warning:hover,
a.bg-warning:focus {
  background-color: #f7ecb5;
}
.bg-danger {
  background-color: #f2dede;
}
a.bg-danger:hover,
a.bg-danger:focus {
  background-color: #e4b9b9;
}
.page-header {
  padding-bottom: 8px;
  margin: 36px 0 18px;
  border-bottom: 1px solid #eeeeee;
}
ul,
ol {
  margin-top: 0;
  margin-bottom: 9px;
}
ul ul,
ol ul,
ul ol,
ol ol {
  margin-bottom: 0;
}
.list-unstyled {
  padding-left: 0;
  list-style: none;
}
.list-inline {
  padding-left: 0;
  list-style: none;
  margin-left: -5px;
}
.list-inline > li {
  display: inline-block;
  padding-left: 5px;
  padding-right: 5px;
}
dl {
  margin-top: 0;
  margin-bottom: 18px;
}
dt,
dd {
  line-height: 1.42857143;
}
dt {
  font-weight: bold;
}
dd {
  margin-left: 0;
}
@media (min-width: 541px) {
  .dl-horizontal dt {
    float: left;
    width: 160px;
    clear: left;
    text-align: right;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .dl-horizontal dd {
    margin-left: 180px;
  }
}
abbr[title],
abbr[data-original-title] {
  cursor: help;
  border-bottom: 1px dotted #777777;
}
.initialism {
  font-size: 90%;
  text-transform: uppercase;
}
blockquote {
  padding: 9px 18px;
  margin: 0 0 18px;
  font-size: inherit;
  border-left: 5px solid #eeeeee;
}
blockquote p:last-child,
blockquote ul:last-child,
blockquote ol:last-child {
  margin-bottom: 0;
}
blockquote footer,
blockquote small,
blockquote .small {
  display: block;
  font-size: 80%;
  line-height: 1.42857143;
  color: #777777;
}
blockquote footer:before,
blockquote small:before,
blockquote .small:before {
  content: '\2014 \00A0';
}
.blockquote-reverse,
blockquote.pull-right {
  padding-right: 15px;
  padding-left: 0;
  border-right: 5px solid #eeeeee;
  border-left: 0;
  text-align: right;
}
.blockquote-reverse footer:before,
blockquote.pull-right footer:before,
.blockquote-reverse small:before,
blockquote.pull-right small:before,
.blockquote-reverse .small:before,
blockquote.pull-right .small:before {
  content: '';
}
.blockquote-reverse footer:after,
blockquote.pull-right footer:after,
.blockquote-reverse small:after,
blockquote.pull-right small:after,
.blockquote-reverse .small:after,
blockquote.pull-right .small:after {
  content: '\00A0 \2014';
}
address {
  margin-bottom: 18px;
  font-style: normal;
  line-height: 1.42857143;
}
code,
kbd,
pre,
samp {
  font-family: monospace;
}
code {
  padding: 2px 4px;
  font-size: 90%;
  color: #c7254e;
  background-color: #f9f2f4;
  border-radius: 2px;
}
kbd {
  padding: 2px 4px;
  font-size: 90%;
  color: #888;
  background-color: transparent;
  border-radius: 1px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}
kbd kbd {
  padding: 0;
  font-size: 100%;
  font-weight: bold;
  box-shadow: none;
}
pre {
  display: block;
  padding: 8.5px;
  margin: 0 0 9px;
  font-size: 12px;
  line-height: 1.42857143;
  word-break: break-all;
  word-wrap: break-word;
  color: #333333;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 2px;
}
pre code {
  padding: 0;
  font-size: inherit;
  color: inherit;
  white-space: pre-wrap;
  background-color: transparent;
  border-radius: 0;
}
.pre-scrollable {
  max-height: 340px;
  overflow-y: scroll;
}
.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
@media (min-width: 768px) {
  .container {
    width: 768px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 940px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
.container-fluid {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
.row {
  margin-left: 0px;
  margin-right: 0px;
}
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1, .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2, .col-xs-3, .col-sm-3, .col-md-3, .col-lg-3, .col-xs-4, .col-sm-4, .col-md-4, .col-lg-4, .col-xs-5, .col-sm-5, .col-md-5, .col-lg-5, .col-xs-6, .col-sm-6, .col-md-6, .col-lg-6, .col-xs-7, .col-sm-7, .col-md-7, .col-lg-7, .col-xs-8, .col-sm-8, .col-md-8, .col-lg-8, .col-xs-9, .col-sm-9, .col-md-9, .col-lg-9, .col-xs-10, .col-sm-10, .col-md-10, .col-lg-10, .col-xs-11, .col-sm-11, .col-md-11, .col-lg-11, .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-left: 0px;
  padding-right: 0px;
}
.col-xs-1, .col-xs-2, .col-xs-3, .col-xs-4, .col-xs-5, .col-xs-6, .col-xs-7, .col-xs-8, .col-xs-9, .col-xs-10, .col-xs-11, .col-xs-12 {
  float: left;
}
.col-xs-12 {
  width: 100%;
}
.col-xs-11 {
  width: 91.66666667%;
}
.col-xs-10 {
  width: 83.33333333%;
}
.col-xs-9 {
  width: 75%;
}
.col-xs-8 {
  width: 66.66666667%;
}
.col-xs-7 {
  width: 58.33333333%;
}
.col-xs-6 {
  width: 50%;
}
.col-xs-5 {
  width: 41.66666667%;
}
.col-xs-4 {
  width: 33.33333333%;
}
.col-xs-3 {
  width: 25%;
}
.col-xs-2 {
  width: 16.66666667%;
}
.col-xs-1 {
  width: 8.33333333%;
}
.col-xs-pull-12 {
  right: 100%;
}
.col-xs-pull-11 {
  right: 91.66666667%;
}
.col-xs-pull-10 {
  right: 83.33333333%;
}
.col-xs-pull-9 {
  right: 75%;
}
.col-xs-pull-8 {
  right: 66.66666667%;
}
.col-xs-pull-7 {
  right: 58.33333333%;
}
.col-xs-pull-6 {
  right: 50%;
}
.col-xs-pull-5 {
  right: 41.66666667%;
}
.col-xs-pull-4 {
  right: 33.33333333%;
}
.col-xs-pull-3 {
  right: 25%;
}
.col-xs-pull-2 {
  right: 16.66666667%;
}
.col-xs-pull-1 {
  right: 8.33333333%;
}
.col-xs-pull-0 {
  right: auto;
}
.col-xs-push-12 {
  left: 100%;
}
.col-xs-push-11 {
  left: 91.66666667%;
}
.col-xs-push-10 {
  left: 83.33333333%;
}
.col-xs-push-9 {
  left: 75%;
}
.col-xs-push-8 {
  left: 66.66666667%;
}
.col-xs-push-7 {
  left: 58.33333333%;
}
.col-xs-push-6 {
  left: 50%;
}
.col-xs-push-5 {
  left: 41.66666667%;
}
.col-xs-push-4 {
  left: 33.33333333%;
}
.col-xs-push-3 {
  left: 25%;
}
.col-xs-push-2 {
  left: 16.66666667%;
}
.col-xs-push-1 {
  left: 8.33333333%;
}
.col-xs-push-0 {
  left: auto;
}
.col-xs-offset-12 {
  margin-left: 100%;
}
.col-xs-offset-11 {
  margin-left: 91.66666667%;
}
.col-xs-offset-10 {
  margin-left: 83.33333333%;
}
.col-xs-offset-9 {
  margin-left: 75%;
}
.col-xs-offset-8 {
  margin-left: 66.66666667%;
}
.col-xs-offset-7 {
  margin-left: 58.33333333%;
}
.col-xs-offset-6 {
  margin-left: 50%;
}
.col-xs-offset-5 {
  margin-left: 41.66666667%;
}
.col-xs-offset-4 {
  margin-left: 33.33333333%;
}
.col-xs-offset-3 {
  margin-left: 25%;
}
.col-xs-offset-2 {
  margin-left: 16.66666667%;
}
.col-xs-offset-1 {
  margin-left: 8.33333333%;
}
.col-xs-offset-0 {
  margin-left: 0%;
}
@media (min-width: 768px) {
  .col-sm-1, .col-sm-2, .col-sm-3, .col-sm-4, .col-sm-5, .col-sm-6, .col-sm-7, .col-sm-8, .col-sm-9, .col-sm-10, .col-sm-11, .col-sm-12 {
    float: left;
  }
  .col-sm-12 {
    width: 100%;
  }
  .col-sm-11 {
    width: 91.66666667%;
  }
  .col-sm-10 {
    width: 83.33333333%;
  }
  .col-sm-9 {
    width: 75%;
  }
  .col-sm-8 {
    width: 66.66666667%;
  }
  .col-sm-7 {
    width: 58.33333333%;
  }
  .col-sm-6 {
    width: 50%;
  }
  .col-sm-5 {
    width: 41.66666667%;
  }
  .col-sm-4 {
    width: 33.33333333%;
  }
  .col-sm-3 {
    width: 25%;
  }
  .col-sm-2 {
    width: 16.66666667%;
  }
  .col-sm-1 {
    width: 8.33333333%;
  }
  .col-sm-pull-12 {
    right: 100%;
  }
  .col-sm-pull-11 {
    right: 91.66666667%;
  }
  .col-sm-pull-10 {
    right: 83.33333333%;
  }
  .col-sm-pull-9 {
    right: 75%;
  }
  .col-sm-pull-8 {
    right: 66.66666667%;
  }
  .col-sm-pull-7 {
    right: 58.33333333%;
  }
  .col-sm-pull-6 {
    right: 50%;
  }
  .col-sm-pull-5 {
    right: 41.66666667%;
  }
  .col-sm-pull-4 {
    right: 33.33333333%;
  }
  .col-sm-pull-3 {
    right: 25%;
  }
  .col-sm-pull-2 {
    right: 16.66666667%;
  }
  .col-sm-pull-1 {
    right: 8.33333333%;
  }
  .col-sm-pull-0 {
    right: auto;
  }
  .col-sm-push-12 {
    left: 100%;
  }
  .col-sm-push-11 {
    left: 91.66666667%;
  }
  .col-sm-push-10 {
    left: 83.33333333%;
  }
  .col-sm-push-9 {
    left: 75%;
  }
  .col-sm-push-8 {
    left: 66.66666667%;
  }
  .col-sm-push-7 {
    left: 58.33333333%;
  }
  .col-sm-push-6 {
    left: 50%;
  }
  .col-sm-push-5 {
    left: 41.66666667%;
  }
  .col-sm-push-4 {
    left: 33.33333333%;
  }
  .col-sm-push-3 {
    left: 25%;
  }
  .col-sm-push-2 {
    left: 16.66666667%;
  }
  .col-sm-push-1 {
    left: 8.33333333%;
  }
  .col-sm-push-0 {
    left: auto;
  }
  .col-sm-offset-12 {
    margin-left: 100%;
  }
  .col-sm-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-sm-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-sm-offset-9 {
    margin-left: 75%;
  }
  .col-sm-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-sm-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-sm-offset-6 {
    margin-left: 50%;
  }
  .col-sm-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-sm-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-sm-offset-3 {
    margin-left: 25%;
  }
  .col-sm-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-sm-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-sm-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 992px) {
  .col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6, .col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
  }
  .col-md-12 {
    width: 100%;
  }
  .col-md-11 {
    width: 91.66666667%;
  }
  .col-md-10 {
    width: 83.33333333%;
  }
  .col-md-9 {
    width: 75%;
  }
  .col-md-8 {
    width: 66.66666667%;
  }
  .col-md-7 {
    width: 58.33333333%;
  }
  .col-md-6 {
    width: 50%;
  }
  .col-md-5 {
    width: 41.66666667%;
  }
  .col-md-4 {
    width: 33.33333333%;
  }
  .col-md-3 {
    width: 25%;
  }
  .col-md-2 {
    width: 16.66666667%;
  }
  .col-md-1 {
    width: 8.33333333%;
  }
  .col-md-pull-12 {
    right: 100%;
  }
  .col-md-pull-11 {
    right: 91.66666667%;
  }
  .col-md-pull-10 {
    right: 83.33333333%;
  }
  .col-md-pull-9 {
    right: 75%;
  }
  .col-md-pull-8 {
    right: 66.66666667%;
  }
  .col-md-pull-7 {
    right: 58.33333333%;
  }
  .col-md-pull-6 {
    right: 50%;
  }
  .col-md-pull-5 {
    right: 41.66666667%;
  }
  .col-md-pull-4 {
    right: 33.33333333%;
  }
  .col-md-pull-3 {
    right: 25%;
  }
  .col-md-pull-2 {
    right: 16.66666667%;
  }
  .col-md-pull-1 {
    right: 8.33333333%;
  }
  .col-md-pull-0 {
    right: auto;
  }
  .col-md-push-12 {
    left: 100%;
  }
  .col-md-push-11 {
    left: 91.66666667%;
  }
  .col-md-push-10 {
    left: 83.33333333%;
  }
  .col-md-push-9 {
    left: 75%;
  }
  .col-md-push-8 {
    left: 66.66666667%;
  }
  .col-md-push-7 {
    left: 58.33333333%;
  }
  .col-md-push-6 {
    left: 50%;
  }
  .col-md-push-5 {
    left: 41.66666667%;
  }
  .col-md-push-4 {
    left: 33.33333333%;
  }
  .col-md-push-3 {
    left: 25%;
  }
  .col-md-push-2 {
    left: 16.66666667%;
  }
  .col-md-push-1 {
    left: 8.33333333%;
  }
  .col-md-push-0 {
    left: auto;
  }
  .col-md-offset-12 {
    margin-left: 100%;
  }
  .col-md-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-md-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-md-offset-9 {
    margin-left: 75%;
  }
  .col-md-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-md-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-md-offset-6 {
    margin-left: 50%;
  }
  .col-md-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-md-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-md-offset-3 {
    margin-left: 25%;
  }
  .col-md-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-md-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-md-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 1200px) {
  .col-lg-1, .col-lg-2, .col-lg-3, .col-lg-4, .col-lg-5, .col-lg-6, .col-lg-7, .col-lg-8, .col-lg-9, .col-lg-10, .col-lg-11, .col-lg-12 {
    float: left;
  }
  .col-lg-12 {
    width: 100%;
  }
  .col-lg-11 {
    width: 91.66666667%;
  }
  .col-lg-10 {
    width: 83.33333333%;
  }
  .col-lg-9 {
    width: 75%;
  }
  .col-lg-8 {
    width: 66.66666667%;
  }
  .col-lg-7 {
    width: 58.33333333%;
  }
  .col-lg-6 {
    width: 50%;
  }
  .col-lg-5 {
    width: 41.66666667%;
  }
  .col-lg-4 {
    width: 33.33333333%;
  }
  .col-lg-3 {
    width: 25%;
  }
  .col-lg-2 {
    width: 16.66666667%;
  }
  .col-lg-1 {
    width: 8.33333333%;
  }
  .col-lg-pull-12 {
    right: 100%;
  }
  .col-lg-pull-11 {
    right: 91.66666667%;
  }
  .col-lg-pull-10 {
    right: 83.33333333%;
  }
  .col-lg-pull-9 {
    right: 75%;
  }
  .col-lg-pull-8 {
    right: 66.66666667%;
  }
  .col-lg-pull-7 {
    right: 58.33333333%;
  }
  .col-lg-pull-6 {
    right: 50%;
  }
  .col-lg-pull-5 {
    right: 41.66666667%;
  }
  .col-lg-pull-4 {
    right: 33.33333333%;
  }
  .col-lg-pull-3 {
    right: 25%;
  }
  .col-lg-pull-2 {
    right: 16.66666667%;
  }
  .col-lg-pull-1 {
    right: 8.33333333%;
  }
  .col-lg-pull-0 {
    right: auto;
  }
  .col-lg-push-12 {
    left: 100%;
  }
  .col-lg-push-11 {
    left: 91.66666667%;
  }
  .col-lg-push-10 {
    left: 83.33333333%;
  }
  .col-lg-push-9 {
    left: 75%;
  }
  .col-lg-push-8 {
    left: 66.66666667%;
  }
  .col-lg-push-7 {
    left: 58.33333333%;
  }
  .col-lg-push-6 {
    left: 50%;
  }
  .col-lg-push-5 {
    left: 41.66666667%;
  }
  .col-lg-push-4 {
    left: 33.33333333%;
  }
  .col-lg-push-3 {
    left: 25%;
  }
  .col-lg-push-2 {
    left: 16.66666667%;
  }
  .col-lg-push-1 {
    left: 8.33333333%;
  }
  .col-lg-push-0 {
    left: auto;
  }
  .col-lg-offset-12 {
    margin-left: 100%;
  }
  .col-lg-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-lg-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-lg-offset-9 {
    margin-left: 75%;
  }
  .col-lg-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-lg-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-lg-offset-6 {
    margin-left: 50%;
  }
  .col-lg-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-lg-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-lg-offset-3 {
    margin-left: 25%;
  }
  .col-lg-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-lg-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-lg-offset-0 {
    margin-left: 0%;
  }
}
table {
  background-color: transparent;
}
caption {
  padding-top: 8px;
  padding-bottom: 8px;
  color: #777777;
  text-align: left;
}
th {
  text-align: left;
}
.table {
  width: 100%;
  max-width: 100%;
  margin-bottom: 18px;
}
.table > thead > tr > th,
.table > tbody > tr > th,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > tbody > tr > td,
.table > tfoot > tr > td {
  padding: 8px;
  line-height: 1.42857143;
  vertical-align: top;
  border-top: 1px solid #ddd;
}
.table > thead > tr > th {
  vertical-align: bottom;
  border-bottom: 2px solid #ddd;
}
.table > caption + thead > tr:first-child > th,
.table > colgroup + thead > tr:first-child > th,
.table > thead:first-child > tr:first-child > th,
.table > caption + thead > tr:first-child > td,
.table > colgroup + thead > tr:first-child > td,
.table > thead:first-child > tr:first-child > td {
  border-top: 0;
}
.table > tbody + tbody {
  border-top: 2px solid #ddd;
}
.table .table {
  background-color: #fff;
}
.table-condensed > thead > tr > th,
.table-condensed > tbody > tr > th,
.table-condensed > tfoot > tr > th,
.table-condensed > thead > tr > td,
.table-condensed > tbody > tr > td,
.table-condensed > tfoot > tr > td {
  padding: 5px;
}
.table-bordered {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > tbody > tr > th,
.table-bordered > tfoot > tr > th,
.table-bordered > thead > tr > td,
.table-bordered > tbody > tr > td,
.table-bordered > tfoot > tr > td {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > thead > tr > td {
  border-bottom-width: 2px;
}
.table-striped > tbody > tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
.table-hover > tbody > tr:hover {
  background-color: #f5f5f5;
}
table col[class*="col-"] {
  position: static;
  float: none;
  display: table-column;
}
table td[class*="col-"],
table th[class*="col-"] {
  position: static;
  float: none;
  display: table-cell;
}
.table > thead > tr > td.active,
.table > tbody > tr > td.active,
.table > tfoot > tr > td.active,
.table > thead > tr > th.active,
.table > tbody > tr > th.active,
.table > tfoot > tr > th.active,
.table > thead > tr.active > td,
.table > tbody > tr.active > td,
.table > tfoot > tr.active > td,
.table > thead > tr.active > th,
.table > tbody > tr.active > th,
.table > tfoot > tr.active > th {
  background-color: #f5f5f5;
}
.table-hover > tbody > tr > td.active:hover,
.table-hover > tbody > tr > th.active:hover,
.table-hover > tbody > tr.active:hover > td,
.table-hover > tbody > tr:hover > .active,
.table-hover > tbody > tr.active:hover > th {
  background-color: #e8e8e8;
}
.table > thead > tr > td.success,
.table > tbody > tr > td.success,
.table > tfoot > tr > td.success,
.table > thead > tr > th.success,
.table > tbody > tr > th.success,
.table > tfoot > tr > th.success,
.table > thead > tr.success > td,
.table > tbody > tr.success > td,
.table > tfoot > tr.success > td,
.table > thead > tr.success > th,
.table > tbody > tr.success > th,
.table > tfoot > tr.success > th {
  background-color: #dff0d8;
}
.table-hover > tbody > tr > td.success:hover,
.table-hover > tbody > tr > th.success:hover,
.table-hover > tbody > tr.success:hover > td,
.table-hover > tbody > tr:hover > .success,
.table-hover > tbody > tr.success:hover > th {
  background-color: #d0e9c6;
}
.table > thead > tr > td.info,
.table > tbody > tr > td.info,
.table > tfoot > tr > td.info,
.table > thead > tr > th.info,
.table > tbody > tr > th.info,
.table > tfoot > tr > th.info,
.table > thead > tr.info > td,
.table > tbody > tr.info > td,
.table > tfoot > tr.info > td,
.table > thead > tr.info > th,
.table > tbody > tr.info > th,
.table > tfoot > tr.info > th {
  background-color: #d9edf7;
}
.table-hover > tbody > tr > td.info:hover,
.table-hover > tbody > tr > th.info:hover,
.table-hover > tbody > tr.info:hover > td,
.table-hover > tbody > tr:hover > .info,
.table-hover > tbody > tr.info:hover > th {
  background-color: #c4e3f3;
}
.table > thead > tr > td.warning,
.table > tbody > tr > td.warning,
.table > tfoot > tr > td.warning,
.table > thead > tr > th.warning,
.table > tbody > tr > th.warning,
.table > tfoot > tr > th.warning,
.table > thead > tr.warning > td,
.table > tbody > tr.warning > td,
.table > tfoot > tr.warning > td,
.table > thead > tr.warning > th,
.table > tbody > tr.warning > th,
.table > tfoot > tr.warning > th {
  background-color: #fcf8e3;
}
.table-hover > tbody > tr > td.warning:hover,
.table-hover > tbody > tr > th.warning:hover,
.table-hover > tbody > tr.warning:hover > td,
.table-hover > tbody > tr:hover > .warning,
.table-hover > tbody > tr.warning:hover > th {
  background-color: #faf2cc;
}
.table > thead > tr > td.danger,
.table > tbody > tr > td.danger,
.table > tfoot > tr > td.danger,
.table > thead > tr > th.danger,
.table > tbody > tr > th.danger,
.table > tfoot > tr > th.danger,
.table > thead > tr.danger > td,
.table > tbody > tr.danger > td,
.table > tfoot > tr.danger > td,
.table > thead > tr.danger > th,
.table > tbody > tr.danger > th,
.table > tfoot > tr.danger > th {
  background-color: #f2dede;
}
.table-hover > tbody > tr > td.danger:hover,
.table-hover > tbody > tr > th.danger:hover,
.table-hover > tbody > tr.danger:hover > td,
.table-hover > tbody > tr:hover > .danger,
.table-hover > tbody > tr.danger:hover > th {
  background-color: #ebcccc;
}
.table-responsive {
  overflow-x: auto;
  min-height: 0.01%;
}
@media screen and (max-width: 767px) {
  .table-responsive {
    width: 100%;
    margin-bottom: 13.5px;
    overflow-y: hidden;
    -ms-overflow-style: -ms-autohiding-scrollbar;
    border: 1px solid #ddd;
  }
  .table-responsive > .table {
    margin-bottom: 0;
  }
  .table-responsive > .table > thead > tr > th,
  .table-responsive > .table > tbody > tr > th,
  .table-responsive > .table > tfoot > tr > th,
  .table-responsive > .table > thead > tr > td,
  .table-responsive > .table > tbody > tr > td,
  .table-responsive > .table > tfoot > tr > td {
    white-space: nowrap;
  }
  .table-responsive > .table-bordered {
    border: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:first-child,
  .table-responsive > .table-bordered > tbody > tr > th:first-child,
  .table-responsive > .table-bordered > tfoot > tr > th:first-child,
  .table-responsive > .table-bordered > thead > tr > td:first-child,
  .table-responsive > .table-bordered > tbody > tr > td:first-child,
  .table-responsive > .table-bordered > tfoot > tr > td:first-child {
    border-left: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:last-child,
  .table-responsive > .table-bordered > tbody > tr > th:last-child,
  .table-responsive > .table-bordered > tfoot > tr > th:last-child,
  .table-responsive > .table-bordered > thead > tr > td:last-child,
  .table-responsive > .table-bordered > tbody > tr > td:last-child,
  .table-responsive > .table-bordered > tfoot > tr > td:last-child {
    border-right: 0;
  }
  .table-responsive > .table-bordered > tbody > tr:last-child > th,
  .table-responsive > .table-bordered > tfoot > tr:last-child > th,
  .table-responsive > .table-bordered > tbody > tr:last-child > td,
  .table-responsive > .table-bordered > tfoot > tr:last-child > td {
    border-bottom: 0;
  }
}
fieldset {
  padding: 0;
  margin: 0;
  border: 0;
  min-width: 0;
}
legend {
  display: block;
  width: 100%;
  padding: 0;
  margin-bottom: 18px;
  font-size: 19.5px;
  line-height: inherit;
  color: #333333;
  border: 0;
  border-bottom: 1px solid #e5e5e5;
}
label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-weight: bold;
}
input[type="search"] {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
input[type="radio"],
input[type="checkbox"] {
  margin: 4px 0 0;
  margin-top: 1px \9;
  line-height: normal;
}
input[type="file"] {
  display: block;
}
input[type="range"] {
  display: block;
  width: 100%;
}
select[multiple],
select[size] {
  height: auto;
}
input[type="file"]:focus,
input[type="radio"]:focus,
input[type="checkbox"]:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
output {
  display: block;
  padding-top: 7px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
}
.form-control {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
}
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.form-control::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.form-control:-ms-input-placeholder {
  color: #999;
}
.form-control::-webkit-input-placeholder {
  color: #999;
}
.form-control::-ms-expand {
  border: 0;
  background-color: transparent;
}
.form-control[disabled],
.form-control[readonly],
fieldset[disabled] .form-control {
  background-color: #eeeeee;
  opacity: 1;
}
.form-control[disabled],
fieldset[disabled] .form-control {
  cursor: not-allowed;
}
textarea.form-control {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: none;
}
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  input[type="date"].form-control,
  input[type="time"].form-control,
  input[type="datetime-local"].form-control,
  input[type="month"].form-control {
    line-height: 32px;
  }
  input[type="date"].input-sm,
  input[type="time"].input-sm,
  input[type="datetime-local"].input-sm,
  input[type="month"].input-sm,
  .input-group-sm input[type="date"],
  .input-group-sm input[type="time"],
  .input-group-sm input[type="datetime-local"],
  .input-group-sm input[type="month"] {
    line-height: 30px;
  }
  input[type="date"].input-lg,
  input[type="time"].input-lg,
  input[type="datetime-local"].input-lg,
  input[type="month"].input-lg,
  .input-group-lg input[type="date"],
  .input-group-lg input[type="time"],
  .input-group-lg input[type="datetime-local"],
  .input-group-lg input[type="month"] {
    line-height: 45px;
  }
}
.form-group {
  margin-bottom: 15px;
}
.radio,
.checkbox {
  position: relative;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
.radio label,
.checkbox label {
  min-height: 18px;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  cursor: pointer;
}
.radio input[type="radio"],
.radio-inline input[type="radio"],
.checkbox input[type="checkbox"],
.checkbox-inline input[type="checkbox"] {
  position: absolute;
  margin-left: -20px;
  margin-top: 4px \9;
}
.radio + .radio,
.checkbox + .checkbox {
  margin-top: -5px;
}
.radio-inline,
.checkbox-inline {
  position: relative;
  display: inline-block;
  padding-left: 20px;
  margin-bottom: 0;
  vertical-align: middle;
  font-weight: normal;
  cursor: pointer;
}
.radio-inline + .radio-inline,
.checkbox-inline + .checkbox-inline {
  margin-top: 0;
  margin-left: 10px;
}
input[type="radio"][disabled],
input[type="checkbox"][disabled],
input[type="radio"].disabled,
input[type="checkbox"].disabled,
fieldset[disabled] input[type="radio"],
fieldset[disabled] input[type="checkbox"] {
  cursor: not-allowed;
}
.radio-inline.disabled,
.checkbox-inline.disabled,
fieldset[disabled] .radio-inline,
fieldset[disabled] .checkbox-inline {
  cursor: not-allowed;
}
.radio.disabled label,
.checkbox.disabled label,
fieldset[disabled] .radio label,
fieldset[disabled] .checkbox label {
  cursor: not-allowed;
}
.form-control-static {
  padding-top: 7px;
  padding-bottom: 7px;
  margin-bottom: 0;
  min-height: 31px;
}
.form-control-static.input-lg,
.form-control-static.input-sm {
  padding-left: 0;
  padding-right: 0;
}
.input-sm {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-sm {
  height: 30px;
  line-height: 30px;
}
textarea.input-sm,
select[multiple].input-sm {
  height: auto;
}
.form-group-sm .form-control {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.form-group-sm select.form-control {
  height: 30px;
  line-height: 30px;
}
.form-group-sm textarea.form-control,
.form-group-sm select[multiple].form-control {
  height: auto;
}
.form-group-sm .form-control-static {
  height: 30px;
  min-height: 30px;
  padding: 6px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.input-lg {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-lg {
  height: 45px;
  line-height: 45px;
}
textarea.input-lg,
select[multiple].input-lg {
  height: auto;
}
.form-group-lg .form-control {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.form-group-lg select.form-control {
  height: 45px;
  line-height: 45px;
}
.form-group-lg textarea.form-control,
.form-group-lg select[multiple].form-control {
  height: auto;
}
.form-group-lg .form-control-static {
  height: 45px;
  min-height: 35px;
  padding: 11px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.has-feedback {
  position: relative;
}
.has-feedback .form-control {
  padding-right: 40px;
}
.form-control-feedback {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
  display: block;
  width: 32px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  pointer-events: none;
}
.input-lg + .form-control-feedback,
.input-group-lg + .form-control-feedback,
.form-group-lg .form-control + .form-control-feedback {
  width: 45px;
  height: 45px;
  line-height: 45px;
}
.input-sm + .form-control-feedback,
.input-group-sm + .form-control-feedback,
.form-group-sm .form-control + .form-control-feedback {
  width: 30px;
  height: 30px;
  line-height: 30px;
}
.has-success .help-block,
.has-success .control-label,
.has-success .radio,
.has-success .checkbox,
.has-success .radio-inline,
.has-success .checkbox-inline,
.has-success.radio label,
.has-success.checkbox label,
.has-success.radio-inline label,
.has-success.checkbox-inline label {
  color: #3c763d;
}
.has-success .form-control {
  border-color: #3c763d;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-success .form-control:focus {
  border-color: #2b542c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
}
.has-success .input-group-addon {
  color: #3c763d;
  border-color: #3c763d;
  background-color: #dff0d8;
}
.has-success .form-control-feedback {
  color: #3c763d;
}
.has-warning .help-block,
.has-warning .control-label,
.has-warning .radio,
.has-warning .checkbox,
.has-warning .radio-inline,
.has-warning .checkbox-inline,
.has-warning.radio label,
.has-warning.checkbox label,
.has-warning.radio-inline label,
.has-warning.checkbox-inline label {
  color: #8a6d3b;
}
.has-warning .form-control {
  border-color: #8a6d3b;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-warning .form-control:focus {
  border-color: #66512c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
}
.has-warning .input-group-addon {
  color: #8a6d3b;
  border-color: #8a6d3b;
  background-color: #fcf8e3;
}
.has-warning .form-control-feedback {
  color: #8a6d3b;
}
.has-error .help-block,
.has-error .control-label,
.has-error .radio,
.has-error .checkbox,
.has-error .radio-inline,
.has-error .checkbox-inline,
.has-error.radio label,
.has-error.checkbox label,
.has-error.radio-inline label,
.has-error.checkbox-inline label {
  color: #a94442;
}
.has-error .form-control {
  border-color: #a94442;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-error .form-control:focus {
  border-color: #843534;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
}
.has-error .input-group-addon {
  color: #a94442;
  border-color: #a94442;
  background-color: #f2dede;
}
.has-error .form-control-feedback {
  color: #a94442;
}
.has-feedback label ~ .form-control-feedback {
  top: 23px;
}
.has-feedback label.sr-only ~ .form-control-feedback {
  top: 0;
}
.help-block {
  display: block;
  margin-top: 5px;
  margin-bottom: 10px;
  color: #404040;
}
@media (min-width: 768px) {
  .form-inline .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .form-inline .form-control-static {
    display: inline-block;
  }
  .form-inline .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .form-inline .input-group .input-group-addon,
  .form-inline .input-group .input-group-btn,
  .form-inline .input-group .form-control {
    width: auto;
  }
  .form-inline .input-group > .form-control {
    width: 100%;
  }
  .form-inline .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio,
  .form-inline .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio label,
  .form-inline .checkbox label {
    padding-left: 0;
  }
  .form-inline .radio input[type="radio"],
  .form-inline .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .form-inline .has-feedback .form-control-feedback {
    top: 0;
  }
}
.form-horizontal .radio,
.form-horizontal .checkbox,
.form-horizontal .radio-inline,
.form-horizontal .checkbox-inline {
  margin-top: 0;
  margin-bottom: 0;
  padding-top: 7px;
}
.form-horizontal .radio,
.form-horizontal .checkbox {
  min-height: 25px;
}
.form-horizontal .form-group {
  margin-left: 0px;
  margin-right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .control-label {
    text-align: right;
    margin-bottom: 0;
    padding-top: 7px;
  }
}
.form-horizontal .has-feedback .form-control-feedback {
  right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .form-group-lg .control-label {
    padding-top: 11px;
    font-size: 17px;
  }
}
@media (min-width: 768px) {
  .form-horizontal .form-group-sm .control-label {
    padding-top: 6px;
    font-size: 12px;
  }
}
.btn {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  border-radius: 2px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  outline: 0;
  background-image: none;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  opacity: 0.65;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
  box-shadow: none;
}
a.btn.disabled,
fieldset[disabled] a.btn {
  pointer-events: none;
}
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.btn-default:focus,
.btn-default.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.btn-default:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active:hover,
.btn-default.active:hover,
.open > .dropdown-toggle.btn-default:hover,
.btn-default:active:focus,
.btn-default.active:focus,
.open > .dropdown-toggle.btn-default:focus,
.btn-default:active.focus,
.btn-default.active.focus,
.open > .dropdown-toggle.btn-default.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  background-image: none;
}
.btn-default.disabled:hover,
.btn-default[disabled]:hover,
fieldset[disabled] .btn-default:hover,
.btn-default.disabled:focus,
.btn-default[disabled]:focus,
fieldset[disabled] .btn-default:focus,
.btn-default.disabled.focus,
.btn-default[disabled].focus,
fieldset[disabled] .btn-default.focus {
  background-color: #fff;
  border-color: #ccc;
}
.btn-default .badge {
  color: #fff;
  background-color: #333;
}
.btn-primary {
  color: #fff;
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary:focus,
.btn-primary.focus {
  color: #fff;
  background-color: #286090;
  border-color: #122b40;
}
.btn-primary:hover {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active:hover,
.btn-primary.active:hover,
.open > .dropdown-toggle.btn-primary:hover,
.btn-primary:active:focus,
.btn-primary.active:focus,
.open > .dropdown-toggle.btn-primary:focus,
.btn-primary:active.focus,
.btn-primary.active.focus,
.open > .dropdown-toggle.btn-primary.focus {
  color: #fff;
  background-color: #204d74;
  border-color: #122b40;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  background-image: none;
}
.btn-primary.disabled:hover,
.btn-primary[disabled]:hover,
fieldset[disabled] .btn-primary:hover,
.btn-primary.disabled:focus,
.btn-primary[disabled]:focus,
fieldset[disabled] .btn-primary:focus,
.btn-primary.disabled.focus,
.btn-primary[disabled].focus,
fieldset[disabled] .btn-primary.focus {
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary .badge {
  color: #337ab7;
  background-color: #fff;
}
.btn-success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success:focus,
.btn-success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.btn-success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active:hover,
.btn-success.active:hover,
.open > .dropdown-toggle.btn-success:hover,
.btn-success:active:focus,
.btn-success.active:focus,
.open > .dropdown-toggle.btn-success:focus,
.btn-success:active.focus,
.btn-success.active.focus,
.open > .dropdown-toggle.btn-success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  background-image: none;
}
.btn-success.disabled:hover,
.btn-success[disabled]:hover,
fieldset[disabled] .btn-success:hover,
.btn-success.disabled:focus,
.btn-success[disabled]:focus,
fieldset[disabled] .btn-success:focus,
.btn-success.disabled.focus,
.btn-success[disabled].focus,
fieldset[disabled] .btn-success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.btn-info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info:focus,
.btn-info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.btn-info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active:hover,
.btn-info.active:hover,
.open > .dropdown-toggle.btn-info:hover,
.btn-info:active:focus,
.btn-info.active:focus,
.open > .dropdown-toggle.btn-info:focus,
.btn-info:active.focus,
.btn-info.active.focus,
.open > .dropdown-toggle.btn-info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  background-image: none;
}
.btn-info.disabled:hover,
.btn-info[disabled]:hover,
fieldset[disabled] .btn-info:hover,
.btn-info.disabled:focus,
.btn-info[disabled]:focus,
fieldset[disabled] .btn-info:focus,
.btn-info.disabled.focus,
.btn-info[disabled].focus,
fieldset[disabled] .btn-info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.btn-warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning:focus,
.btn-warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.btn-warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active:hover,
.btn-warning.active:hover,
.open > .dropdown-toggle.btn-warning:hover,
.btn-warning:active:focus,
.btn-warning.active:focus,
.open > .dropdown-toggle.btn-warning:focus,
.btn-warning:active.focus,
.btn-warning.active.focus,
.open > .dropdown-toggle.btn-warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  background-image: none;
}
.btn-warning.disabled:hover,
.btn-warning[disabled]:hover,
fieldset[disabled] .btn-warning:hover,
.btn-warning.disabled:focus,
.btn-warning[disabled]:focus,
fieldset[disabled] .btn-warning:focus,
.btn-warning.disabled.focus,
.btn-warning[disabled].focus,
fieldset[disabled] .btn-warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.btn-danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger:focus,
.btn-danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.btn-danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active:hover,
.btn-danger.active:hover,
.open > .dropdown-toggle.btn-danger:hover,
.btn-danger:active:focus,
.btn-danger.active:focus,
.open > .dropdown-toggle.btn-danger:focus,
.btn-danger:active.focus,
.btn-danger.active.focus,
.open > .dropdown-toggle.btn-danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  background-image: none;
}
.btn-danger.disabled:hover,
.btn-danger[disabled]:hover,
fieldset[disabled] .btn-danger:hover,
.btn-danger.disabled:focus,
.btn-danger[disabled]:focus,
fieldset[disabled] .btn-danger:focus,
.btn-danger.disabled.focus,
.btn-danger[disabled].focus,
fieldset[disabled] .btn-danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger .badge {
  color: #d9534f;
  background-color: #fff;
}
.btn-link {
  color: #337ab7;
  font-weight: normal;
  border-radius: 0;
}
.btn-link,
.btn-link:active,
.btn-link.active,
.btn-link[disabled],
fieldset[disabled] .btn-link {
  background-color: transparent;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn-link,
.btn-link:hover,
.btn-link:focus,
.btn-link:active {
  border-color: transparent;
}
.btn-link:hover,
.btn-link:focus {
  color: #23527c;
  text-decoration: underline;
  background-color: transparent;
}
.btn-link[disabled]:hover,
fieldset[disabled] .btn-link:hover,
.btn-link[disabled]:focus,
fieldset[disabled] .btn-link:focus {
  color: #777777;
  text-decoration: none;
}
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-block {
  display: block;
  width: 100%;
}
.btn-block + .btn-block {
  margin-top: 5px;
}
input[type="submit"].btn-block,
input[type="reset"].btn-block,
input[type="button"].btn-block {
  width: 100%;
}
.fade {
  opacity: 0;
  -webkit-transition: opacity 0.15s linear;
  -o-transition: opacity 0.15s linear;
  transition: opacity 0.15s linear;
}
.fade.in {
  opacity: 1;
}
.collapse {
  display: none;
}
.collapse.in {
  display: block;
}
tr.collapse.in {
  display: table-row;
}
tbody.collapse.in {
  display: table-row-group;
}
.collapsing {
  position: relative;
  height: 0;
  overflow: hidden;
  -webkit-transition-property: height, visibility;
  transition-property: height, visibility;
  -webkit-transition-duration: 0.35s;
  transition-duration: 0.35s;
  -webkit-transition-timing-function: ease;
  transition-timing-function: ease;
}
.caret {
  display: inline-block;
  width: 0;
  height: 0;
  margin-left: 2px;
  vertical-align: middle;
  border-top: 4px dashed;
  border-top: 4px solid \9;
  border-right: 4px solid transparent;
  border-left: 4px solid transparent;
}
.dropup,
.dropdown {
  position: relative;
}
.dropdown-toggle:focus {
  outline: 0;
}
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  display: none;
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  list-style: none;
  font-size: 13px;
  text-align: left;
  background-color: #fff;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.15);
  border-radius: 2px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  background-clip: padding-box;
}
.dropdown-menu.pull-right {
  right: 0;
  left: auto;
}
.dropdown-menu .divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.dropdown-menu > li > a {
  display: block;
  padding: 3px 20px;
  clear: both;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333333;
  white-space: nowrap;
}
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  text-decoration: none;
  color: #262626;
  background-color: #f5f5f5;
}
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  outline: 0;
  background-color: #337ab7;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
  cursor: not-allowed;
}
.open > .dropdown-menu {
  display: block;
}
.open > a {
  outline: 0;
}
.dropdown-menu-right {
  left: auto;
  right: 0;
}
.dropdown-menu-left {
  left: 0;
  right: auto;
}
.dropdown-header {
  display: block;
  padding: 3px 20px;
  font-size: 12px;
  line-height: 1.42857143;
  color: #777777;
  white-space: nowrap;
}
.dropdown-backdrop {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  z-index: 990;
}
.pull-right > .dropdown-menu {
  right: 0;
  left: auto;
}
.dropup .caret,
.navbar-fixed-bottom .dropdown .caret {
  border-top: 0;
  border-bottom: 4px dashed;
  border-bottom: 4px solid \9;
  content: "";
}
.dropup .dropdown-menu,
.navbar-fixed-bottom .dropdown .dropdown-menu {
  top: auto;
  bottom: 100%;
  margin-bottom: 2px;
}
@media (min-width: 541px) {
  .navbar-right .dropdown-menu {
    left: auto;
    right: 0;
  }
  .navbar-right .dropdown-menu-left {
    left: 0;
    right: auto;
  }
}
.btn-group,
.btn-group-vertical {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.btn-group > .btn,
.btn-group-vertical > .btn {
  position: relative;
  float: left;
}
.btn-group > .btn:hover,
.btn-group-vertical > .btn:hover,
.btn-group > .btn:focus,
.btn-group-vertical > .btn:focus,
.btn-group > .btn:active,
.btn-group-vertical > .btn:active,
.btn-group > .btn.active,
.btn-group-vertical > .btn.active {
  z-index: 2;
}
.btn-group .btn + .btn,
.btn-group .btn + .btn-group,
.btn-group .btn-group + .btn,
.btn-group .btn-group + .btn-group {
  margin-left: -1px;
}
.btn-toolbar {
  margin-left: -5px;
}
.btn-toolbar .btn,
.btn-toolbar .btn-group,
.btn-toolbar .input-group {
  float: left;
}
.btn-toolbar > .btn,
.btn-toolbar > .btn-group,
.btn-toolbar > .input-group {
  margin-left: 5px;
}
.btn-group > .btn:not(:first-child):not(:last-child):not(.dropdown-toggle) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  margin-left: 0;
}
.btn-group > .btn:first-child:not(:last-child):not(.dropdown-toggle) {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn:last-child:not(:first-child),
.btn-group > .dropdown-toggle:not(:first-child) {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group .dropdown-toggle:active,
.btn-group.open .dropdown-toggle {
  outline: 0;
}
.btn-group > .btn + .dropdown-toggle {
  padding-left: 8px;
  padding-right: 8px;
}
.btn-group > .btn-lg + .dropdown-toggle {
  padding-left: 12px;
  padding-right: 12px;
}
.btn-group.open .dropdown-toggle {
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn-group.open .dropdown-toggle.btn-link {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn .caret {
  margin-left: 0;
}
.btn-lg .caret {
  border-width: 5px 5px 0;
  border-bottom-width: 0;
}
.dropup .btn-lg .caret {
  border-width: 0 5px 5px;
}
.btn-group-vertical > .btn,
.btn-group-vertical > .btn-group,
.btn-group-vertical > .btn-group > .btn {
  display: block;
  float: none;
  width: 100%;
  max-width: 100%;
}
.btn-group-vertical > .btn-group > .btn {
  float: none;
}
.btn-group-vertical > .btn + .btn,
.btn-group-vertical > .btn + .btn-group,
.btn-group-vertical > .btn-group + .btn,
.btn-group-vertical > .btn-group + .btn-group {
  margin-top: -1px;
  margin-left: 0;
}
.btn-group-vertical > .btn:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.btn-group-vertical > .btn:first-child:not(:last-child) {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn:last-child:not(:first-child) {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
.btn-group-vertical > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.btn-group-justified {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-collapse: separate;
}
.btn-group-justified > .btn,
.btn-group-justified > .btn-group {
  float: none;
  display: table-cell;
  width: 1%;
}
.btn-group-justified > .btn-group .btn {
  width: 100%;
}
.btn-group-justified > .btn-group .dropdown-menu {
  left: auto;
}
[data-toggle="buttons"] > .btn input[type="radio"],
[data-toggle="buttons"] > .btn-group > .btn input[type="radio"],
[data-toggle="buttons"] > .btn input[type="checkbox"],
[data-toggle="buttons"] > .btn-group > .btn input[type="checkbox"] {
  position: absolute;
  clip: rect(0, 0, 0, 0);
  pointer-events: none;
}
.input-group {
  position: relative;
  display: table;
  border-collapse: separate;
}
.input-group[class*="col-"] {
  float: none;
  padding-left: 0;
  padding-right: 0;
}
.input-group .form-control {
  position: relative;
  z-index: 2;
  float: left;
  width: 100%;
  margin-bottom: 0;
}
.input-group .form-control:focus {
  z-index: 3;
}
.input-group-lg > .form-control,
.input-group-lg > .input-group-addon,
.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-group-lg > .form-control,
select.input-group-lg > .input-group-addon,
select.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  line-height: 45px;
}
textarea.input-group-lg > .form-control,
textarea.input-group-lg > .input-group-addon,
textarea.input-group-lg > .input-group-btn > .btn,
select[multiple].input-group-lg > .form-control,
select[multiple].input-group-lg > .input-group-addon,
select[multiple].input-group-lg > .input-group-btn > .btn {
  height: auto;
}
.input-group-sm > .form-control,
.input-group-sm > .input-group-addon,
.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-group-sm > .form-control,
select.input-group-sm > .input-group-addon,
select.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  line-height: 30px;
}
textarea.input-group-sm > .form-control,
textarea.input-group-sm > .input-group-addon,
textarea.input-group-sm > .input-group-btn > .btn,
select[multiple].input-group-sm > .form-control,
select[multiple].input-group-sm > .input-group-addon,
select[multiple].input-group-sm > .input-group-btn > .btn {
  height: auto;
}
.input-group-addon,
.input-group-btn,
.input-group .form-control {
  display: table-cell;
}
.input-group-addon:not(:first-child):not(:last-child),
.input-group-btn:not(:first-child):not(:last-child),
.input-group .form-control:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.input-group-addon,
.input-group-btn {
  width: 1%;
  white-space: nowrap;
  vertical-align: middle;
}
.input-group-addon {
  padding: 6px 12px;
  font-size: 13px;
  font-weight: normal;
  line-height: 1;
  color: #555555;
  text-align: center;
  background-color: #eeeeee;
  border: 1px solid #ccc;
  border-radius: 2px;
}
.input-group-addon.input-sm {
  padding: 5px 10px;
  font-size: 12px;
  border-radius: 1px;
}
.input-group-addon.input-lg {
  padding: 10px 16px;
  font-size: 17px;
  border-radius: 3px;
}
.input-group-addon input[type="radio"],
.input-group-addon input[type="checkbox"] {
  margin-top: 0;
}
.input-group .form-control:first-child,
.input-group-addon:first-child,
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group > .btn,
.input-group-btn:first-child > .dropdown-toggle,
.input-group-btn:last-child > .btn:not(:last-child):not(.dropdown-toggle),
.input-group-btn:last-child > .btn-group:not(:last-child) > .btn {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.input-group-addon:first-child {
  border-right: 0;
}
.input-group .form-control:last-child,
.input-group-addon:last-child,
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group > .btn,
.input-group-btn:last-child > .dropdown-toggle,
.input-group-btn:first-child > .btn:not(:first-child),
.input-group-btn:first-child > .btn-group:not(:first-child) > .btn {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.input-group-addon:last-child {
  border-left: 0;
}
.input-group-btn {
  position: relative;
  font-size: 0;
  white-space: nowrap;
}
.input-group-btn > .btn {
  position: relative;
}
.input-group-btn > .btn + .btn {
  margin-left: -1px;
}
.input-group-btn > .btn:hover,
.input-group-btn > .btn:focus,
.input-group-btn > .btn:active {
  z-index: 2;
}
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group {
  margin-right: -1px;
}
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group {
  z-index: 2;
  margin-left: -1px;
}
.nav {
  margin-bottom: 0;
  padding-left: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.nav > li.disabled > a {
  color: #777777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777777;
  text-decoration: none;
  background-color: transparent;
  cursor: not-allowed;
}
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eeeeee;
  border-color: #337ab7;
}
.nav .nav-divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.nav > li > a > img {
  max-width: none;
}
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 2px 2px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eeeeee #eeeeee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555555;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
  cursor: default;
}
.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 2px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
.nav-stacked > li {
  float: none;
}
.nav-stacked > li + li {
  margin-top: 2px;
  margin-left: 0;
}
.nav-justified {
  width: 100%;
}
.nav-justified > li {
  float: none;
}
.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs-justified {
  border-bottom: 0;
}
.nav-tabs-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs-justified > .active > a,
.nav-tabs-justified > .active > a:hover,
.nav-tabs-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs-justified > .active > a,
  .nav-tabs-justified > .active > a:hover,
  .nav-tabs-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.tab-content > .tab-pane {
  display: none;
}
.tab-content > .active {
  display: block;
}
.nav-tabs .dropdown-menu {
  margin-top: -1px;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar {
  position: relative;
  min-height: 30px;
  margin-bottom: 18px;
  border: 1px solid transparent;
}
@media (min-width: 541px) {
  .navbar {
    border-radius: 2px;
  }
}
@media (min-width: 541px) {
  .navbar-header {
    float: left;
  }
}
.navbar-collapse {
  overflow-x: visible;
  padding-right: 0px;
  padding-left: 0px;
  border-top: 1px solid transparent;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  -webkit-overflow-scrolling: touch;
}
.navbar-collapse.in {
  overflow-y: auto;
}
@media (min-width: 541px) {
  .navbar-collapse {
    width: auto;
    border-top: 0;
    box-shadow: none;
  }
  .navbar-collapse.collapse {
    display: block !important;
    height: auto !important;
    padding-bottom: 0;
    overflow: visible !important;
  }
  .navbar-collapse.in {
    overflow-y: visible;
  }
  .navbar-fixed-top .navbar-collapse,
  .navbar-static-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    padding-left: 0;
    padding-right: 0;
  }
}
.navbar-fixed-top .navbar-collapse,
.navbar-fixed-bottom .navbar-collapse {
  max-height: 340px;
}
@media (max-device-width: 540px) and (orientation: landscape) {
  .navbar-fixed-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    max-height: 200px;
  }
}
.container > .navbar-header,
.container-fluid > .navbar-header,
.container > .navbar-collapse,
.container-fluid > .navbar-collapse {
  margin-right: 0px;
  margin-left: 0px;
}
@media (min-width: 541px) {
  .container > .navbar-header,
  .container-fluid > .navbar-header,
  .container > .navbar-collapse,
  .container-fluid > .navbar-collapse {
    margin-right: 0;
    margin-left: 0;
  }
}
.navbar-static-top {
  z-index: 1000;
  border-width: 0 0 1px;
}
@media (min-width: 541px) {
  .navbar-static-top {
    border-radius: 0;
  }
}
.navbar-fixed-top,
.navbar-fixed-bottom {
  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
}
@media (min-width: 541px) {
  .navbar-fixed-top,
  .navbar-fixed-bottom {
    border-radius: 0;
  }
}
.navbar-fixed-top {
  top: 0;
  border-width: 0 0 1px;
}
.navbar-fixed-bottom {
  bottom: 0;
  margin-bottom: 0;
  border-width: 1px 0 0;
}
.navbar-brand {
  float: left;
  padding: 6px 0px;
  font-size: 17px;
  line-height: 18px;
  height: 30px;
}
.navbar-brand:hover,
.navbar-brand:focus {
  text-decoration: none;
}
.navbar-brand > img {
  display: block;
}
@media (min-width: 541px) {
  .navbar > .container .navbar-brand,
  .navbar > .container-fluid .navbar-brand {
    margin-left: 0px;
  }
}
.navbar-toggle {
  position: relative;
  float: right;
  margin-right: 0px;
  padding: 9px 10px;
  margin-top: -2px;
  margin-bottom: -2px;
  background-color: transparent;
  background-image: none;
  border: 1px solid transparent;
  border-radius: 2px;
}
.navbar-toggle:focus {
  outline: 0;
}
.navbar-toggle .icon-bar {
  display: block;
  width: 22px;
  height: 2px;
  border-radius: 1px;
}
.navbar-toggle .icon-bar + .icon-bar {
  margin-top: 4px;
}
@media (min-width: 541px) {
  .navbar-toggle {
    display: none;
  }
}
.navbar-nav {
  margin: 3px 0px;
}
.navbar-nav > li > a {
  padding-top: 10px;
  padding-bottom: 10px;
  line-height: 18px;
}
@media (max-width: 540px) {
  .navbar-nav .open .dropdown-menu {
    position: static;
    float: none;
    width: auto;
    margin-top: 0;
    background-color: transparent;
    border: 0;
    box-shadow: none;
  }
  .navbar-nav .open .dropdown-menu > li > a,
  .navbar-nav .open .dropdown-menu .dropdown-header {
    padding: 5px 15px 5px 25px;
  }
  .navbar-nav .open .dropdown-menu > li > a {
    line-height: 18px;
  }
  .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-nav .open .dropdown-menu > li > a:focus {
    background-image: none;
  }
}
@media (min-width: 541px) {
  .navbar-nav {
    float: left;
    margin: 0;
  }
  .navbar-nav > li {
    float: left;
  }
  .navbar-nav > li > a {
    padding-top: 6px;
    padding-bottom: 6px;
  }
}
.navbar-form {
  margin-left: 0px;
  margin-right: 0px;
  padding: 10px 0px;
  border-top: 1px solid transparent;
  border-bottom: 1px solid transparent;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  margin-top: -1px;
  margin-bottom: -1px;
}
@media (min-width: 768px) {
  .navbar-form .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .navbar-form .form-control-static {
    display: inline-block;
  }
  .navbar-form .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .navbar-form .input-group .input-group-addon,
  .navbar-form .input-group .input-group-btn,
  .navbar-form .input-group .form-control {
    width: auto;
  }
  .navbar-form .input-group > .form-control {
    width: 100%;
  }
  .navbar-form .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio,
  .navbar-form .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio label,
  .navbar-form .checkbox label {
    padding-left: 0;
  }
  .navbar-form .radio input[type="radio"],
  .navbar-form .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .navbar-form .has-feedback .form-control-feedback {
    top: 0;
  }
}
@media (max-width: 540px) {
  .navbar-form .form-group {
    margin-bottom: 5px;
  }
  .navbar-form .form-group:last-child {
    margin-bottom: 0;
  }
}
@media (min-width: 541px) {
  .navbar-form {
    width: auto;
    border: 0;
    margin-left: 0;
    margin-right: 0;
    padding-top: 0;
    padding-bottom: 0;
    -webkit-box-shadow: none;
    box-shadow: none;
  }
}
.navbar-nav > li > .dropdown-menu {
  margin-top: 0;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar-fixed-bottom .navbar-nav > li > .dropdown-menu {
  margin-bottom: 0;
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.navbar-btn {
  margin-top: -1px;
  margin-bottom: -1px;
}
.navbar-btn.btn-sm {
  margin-top: 0px;
  margin-bottom: 0px;
}
.navbar-btn.btn-xs {
  margin-top: 4px;
  margin-bottom: 4px;
}
.navbar-text {
  margin-top: 6px;
  margin-bottom: 6px;
}
@media (min-width: 541px) {
  .navbar-text {
    float: left;
    margin-left: 0px;
    margin-right: 0px;
  }
}
@media (min-width: 541px) {
  .navbar-left {
    float: left !important;
    float: left;
  }
  .navbar-right {
    float: right !important;
    float: right;
    margin-right: 0px;
  }
  .navbar-right ~ .navbar-right {
    margin-right: 0;
  }
}
.navbar-default {
  background-color: #f8f8f8;
  border-color: #e7e7e7;
}
.navbar-default .navbar-brand {
  color: #777;
}
.navbar-default .navbar-brand:hover,
.navbar-default .navbar-brand:focus {
  color: #5e5e5e;
  background-color: transparent;
}
.navbar-default .navbar-text {
  color: #777;
}
.navbar-default .navbar-nav > li > a {
  color: #777;
}
.navbar-default .navbar-nav > li > a:hover,
.navbar-default .navbar-nav > li > a:focus {
  color: #333;
  background-color: transparent;
}
.navbar-default .navbar-nav > .active > a,
.navbar-default .navbar-nav > .active > a:hover,
.navbar-default .navbar-nav > .active > a:focus {
  color: #555;
  background-color: #e7e7e7;
}
.navbar-default .navbar-nav > .disabled > a,
.navbar-default .navbar-nav > .disabled > a:hover,
.navbar-default .navbar-nav > .disabled > a:focus {
  color: #ccc;
  background-color: transparent;
}
.navbar-default .navbar-toggle {
  border-color: #ddd;
}
.navbar-default .navbar-toggle:hover,
.navbar-default .navbar-toggle:focus {
  background-color: #ddd;
}
.navbar-default .navbar-toggle .icon-bar {
  background-color: #888;
}
.navbar-default .navbar-collapse,
.navbar-default .navbar-form {
  border-color: #e7e7e7;
}
.navbar-default .navbar-nav > .open > a,
.navbar-default .navbar-nav > .open > a:hover,
.navbar-default .navbar-nav > .open > a:focus {
  background-color: #e7e7e7;
  color: #555;
}
@media (max-width: 540px) {
  .navbar-default .navbar-nav .open .dropdown-menu > li > a {
    color: #777;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #333;
    background-color: transparent;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #555;
    background-color: #e7e7e7;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #ccc;
    background-color: transparent;
  }
}
.navbar-default .navbar-link {
  color: #777;
}
.navbar-default .navbar-link:hover {
  color: #333;
}
.navbar-default .btn-link {
  color: #777;
}
.navbar-default .btn-link:hover,
.navbar-default .btn-link:focus {
  color: #333;
}
.navbar-default .btn-link[disabled]:hover,
fieldset[disabled] .navbar-default .btn-link:hover,
.navbar-default .btn-link[disabled]:focus,
fieldset[disabled] .navbar-default .btn-link:focus {
  color: #ccc;
}
.navbar-inverse {
  background-color: #222;
  border-color: #080808;
}
.navbar-inverse .navbar-brand {
  color: #9d9d9d;
}
.navbar-inverse .navbar-brand:hover,
.navbar-inverse .navbar-brand:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-text {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a:hover,
.navbar-inverse .navbar-nav > li > a:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-nav > .active > a,
.navbar-inverse .navbar-nav > .active > a:hover,
.navbar-inverse .navbar-nav > .active > a:focus {
  color: #fff;
  background-color: #080808;
}
.navbar-inverse .navbar-nav > .disabled > a,
.navbar-inverse .navbar-nav > .disabled > a:hover,
.navbar-inverse .navbar-nav > .disabled > a:focus {
  color: #444;
  background-color: transparent;
}
.navbar-inverse .navbar-toggle {
  border-color: #333;
}
.navbar-inverse .navbar-toggle:hover,
.navbar-inverse .navbar-toggle:focus {
  background-color: #333;
}
.navbar-inverse .navbar-toggle .icon-bar {
  background-color: #fff;
}
.navbar-inverse .navbar-collapse,
.navbar-inverse .navbar-form {
  border-color: #101010;
}
.navbar-inverse .navbar-nav > .open > a,
.navbar-inverse .navbar-nav > .open > a:hover,
.navbar-inverse .navbar-nav > .open > a:focus {
  background-color: #080808;
  color: #fff;
}
@media (max-width: 540px) {
  .navbar-inverse .navbar-nav .open .dropdown-menu > .dropdown-header {
    border-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu .divider {
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a {
    color: #9d9d9d;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #fff;
    background-color: transparent;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #fff;
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #444;
    background-color: transparent;
  }
}
.navbar-inverse .navbar-link {
  color: #9d9d9d;
}
.navbar-inverse .navbar-link:hover {
  color: #fff;
}
.navbar-inverse .btn-link {
  color: #9d9d9d;
}
.navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link:focus {
  color: #fff;
}
.navbar-inverse .btn-link[disabled]:hover,
fieldset[disabled] .navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link[disabled]:focus,
fieldset[disabled] .navbar-inverse .btn-link:focus {
  color: #444;
}
.breadcrumb {
  padding: 8px 15px;
  margin-bottom: 18px;
  list-style: none;
  background-color: #f5f5f5;
  border-radius: 2px;
}
.breadcrumb > li {
  display: inline-block;
}
.breadcrumb > li + li:before {
  content: "/\00a0";
  padding: 0 5px;
  color: #5e5e5e;
}
.breadcrumb > .active {
  color: #777777;
}
.pagination {
  display: inline-block;
  padding-left: 0;
  margin: 18px 0;
  border-radius: 2px;
}
.pagination > li {
  display: inline;
}
.pagination > li > a,
.pagination > li > span {
  position: relative;
  float: left;
  padding: 6px 12px;
  line-height: 1.42857143;
  text-decoration: none;
  color: #337ab7;
  background-color: #fff;
  border: 1px solid #ddd;
  margin-left: -1px;
}
.pagination > li:first-child > a,
.pagination > li:first-child > span {
  margin-left: 0;
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.pagination > li:last-child > a,
.pagination > li:last-child > span {
  border-bottom-right-radius: 2px;
  border-top-right-radius: 2px;
}
.pagination > li > a:hover,
.pagination > li > span:hover,
.pagination > li > a:focus,
.pagination > li > span:focus {
  z-index: 2;
  color: #23527c;
  background-color: #eeeeee;
  border-color: #ddd;
}
.pagination > .active > a,
.pagination > .active > span,
.pagination > .active > a:hover,
.pagination > .active > span:hover,
.pagination > .active > a:focus,
.pagination > .active > span:focus {
  z-index: 3;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
  cursor: default;
}
.pagination > .disabled > span,
.pagination > .disabled > span:hover,
.pagination > .disabled > span:focus,
.pagination > .disabled > a,
.pagination > .disabled > a:hover,
.pagination > .disabled > a:focus {
  color: #777777;
  background-color: #fff;
  border-color: #ddd;
  cursor: not-allowed;
}
.pagination-lg > li > a,
.pagination-lg > li > span {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.pagination-lg > li:first-child > a,
.pagination-lg > li:first-child > span {
  border-bottom-left-radius: 3px;
  border-top-left-radius: 3px;
}
.pagination-lg > li:last-child > a,
.pagination-lg > li:last-child > span {
  border-bottom-right-radius: 3px;
  border-top-right-radius: 3px;
}
.pagination-sm > li > a,
.pagination-sm > li > span {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.pagination-sm > li:first-child > a,
.pagination-sm > li:first-child > span {
  border-bottom-left-radius: 1px;
  border-top-left-radius: 1px;
}
.pagination-sm > li:last-child > a,
.pagination-sm > li:last-child > span {
  border-bottom-right-radius: 1px;
  border-top-right-radius: 1px;
}
.pager {
  padding-left: 0;
  margin: 18px 0;
  list-style: none;
  text-align: center;
}
.pager li {
  display: inline;
}
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 5px 14px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 15px;
}
.pager li > a:hover,
.pager li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.pager .next > a,
.pager .next > span {
  float: right;
}
.pager .previous > a,
.pager .previous > span {
  float: left;
}
.pager .disabled > a,
.pager .disabled > a:hover,
.pager .disabled > a:focus,
.pager .disabled > span {
  color: #777777;
  background-color: #fff;
  cursor: not-allowed;
}
.label {
  display: inline;
  padding: .2em .6em .3em;
  font-size: 75%;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: .25em;
}
a.label:hover,
a.label:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.label:empty {
  display: none;
}
.btn .label {
  position: relative;
  top: -1px;
}
.label-default {
  background-color: #777777;
}
.label-default[href]:hover,
.label-default[href]:focus {
  background-color: #5e5e5e;
}
.label-primary {
  background-color: #337ab7;
}
.label-primary[href]:hover,
.label-primary[href]:focus {
  background-color: #286090;
}
.label-success {
  background-color: #5cb85c;
}
.label-success[href]:hover,
.label-success[href]:focus {
  background-color: #449d44;
}
.label-info {
  background-color: #5bc0de;
}
.label-info[href]:hover,
.label-info[href]:focus {
  background-color: #31b0d5;
}
.label-warning {
  background-color: #f0ad4e;
}
.label-warning[href]:hover,
.label-warning[href]:focus {
  background-color: #ec971f;
}
.label-danger {
  background-color: #d9534f;
}
.label-danger[href]:hover,
.label-danger[href]:focus {
  background-color: #c9302c;
}
.badge {
  display: inline-block;
  min-width: 10px;
  padding: 3px 7px;
  font-size: 12px;
  font-weight: bold;
  color: #fff;
  line-height: 1;
  vertical-align: middle;
  white-space: nowrap;
  text-align: center;
  background-color: #777777;
  border-radius: 10px;
}
.badge:empty {
  display: none;
}
.btn .badge {
  position: relative;
  top: -1px;
}
.btn-xs .badge,
.btn-group-xs > .btn .badge {
  top: 0;
  padding: 1px 5px;
}
a.badge:hover,
a.badge:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.list-group-item.active > .badge,
.nav-pills > .active > a > .badge {
  color: #337ab7;
  background-color: #fff;
}
.list-group-item > .badge {
  float: right;
}
.list-group-item > .badge + .badge {
  margin-right: 5px;
}
.nav-pills > li > a > .badge {
  margin-left: 3px;
}
.jumbotron {
  padding-top: 30px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  color: inherit;
  background-color: #eeeeee;
}
.jumbotron h1,
.jumbotron .h1 {
  color: inherit;
}
.jumbotron p {
  margin-bottom: 15px;
  font-size: 20px;
  font-weight: 200;
}
.jumbotron > hr {
  border-top-color: #d5d5d5;
}
.container .jumbotron,
.container-fluid .jumbotron {
  border-radius: 3px;
  padding-left: 0px;
  padding-right: 0px;
}
.jumbotron .container {
  max-width: 100%;
}
@media screen and (min-width: 768px) {
  .jumbotron {
    padding-top: 48px;
    padding-bottom: 48px;
  }
  .container .jumbotron,
  .container-fluid .jumbotron {
    padding-left: 60px;
    padding-right: 60px;
  }
  .jumbotron h1,
  .jumbotron .h1 {
    font-size: 59px;
  }
}
.thumbnail {
  display: block;
  padding: 4px;
  margin-bottom: 18px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: border 0.2s ease-in-out;
  -o-transition: border 0.2s ease-in-out;
  transition: border 0.2s ease-in-out;
}
.thumbnail > img,
.thumbnail a > img {
  margin-left: auto;
  margin-right: auto;
}
a.thumbnail:hover,
a.thumbnail:focus,
a.thumbnail.active {
  border-color: #337ab7;
}
.thumbnail .caption {
  padding: 9px;
  color: #000;
}
.alert {
  padding: 15px;
  margin-bottom: 18px;
  border: 1px solid transparent;
  border-radius: 2px;
}
.alert h4 {
  margin-top: 0;
  color: inherit;
}
.alert .alert-link {
  font-weight: bold;
}
.alert > p,
.alert > ul {
  margin-bottom: 0;
}
.alert > p + p {
  margin-top: 5px;
}
.alert-dismissable,
.alert-dismissible {
  padding-right: 35px;
}
.alert-dismissable .close,
.alert-dismissible .close {
  position: relative;
  top: -2px;
  right: -21px;
  color: inherit;
}
.alert-success {
  background-color: #dff0d8;
  border-color: #d6e9c6;
  color: #3c763d;
}
.alert-success hr {
  border-top-color: #c9e2b3;
}
.alert-success .alert-link {
  color: #2b542c;
}
.alert-info {
  background-color: #d9edf7;
  border-color: #bce8f1;
  color: #31708f;
}
.alert-info hr {
  border-top-color: #a6e1ec;
}
.alert-info .alert-link {
  color: #245269;
}
.alert-warning {
  background-color: #fcf8e3;
  border-color: #faebcc;
  color: #8a6d3b;
}
.alert-warning hr {
  border-top-color: #f7e1b5;
}
.alert-warning .alert-link {
  color: #66512c;
}
.alert-danger {
  background-color: #f2dede;
  border-color: #ebccd1;
  color: #a94442;
}
.alert-danger hr {
  border-top-color: #e4b9c0;
}
.alert-danger .alert-link {
  color: #843534;
}
@-webkit-keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
@keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
.progress {
  overflow: hidden;
  height: 18px;
  margin-bottom: 18px;
  background-color: #f5f5f5;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}
.progress-bar {
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 18px;
  color: #fff;
  text-align: center;
  background-color: #337ab7;
  -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  -webkit-transition: width 0.6s ease;
  -o-transition: width 0.6s ease;
  transition: width 0.6s ease;
}
.progress-striped .progress-bar,
.progress-bar-striped {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-size: 40px 40px;
}
.progress.active .progress-bar,
.progress-bar.active {
  -webkit-animation: progress-bar-stripes 2s linear infinite;
  -o-animation: progress-bar-stripes 2s linear infinite;
  animation: progress-bar-stripes 2s linear infinite;
}
.progress-bar-success {
  background-color: #5cb85c;
}
.progress-striped .progress-bar-success {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-info {
  background-color: #5bc0de;
}
.progress-striped .progress-bar-info {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-warning {
  background-color: #f0ad4e;
}
.progress-striped .progress-bar-warning {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-danger {
  background-color: #d9534f;
}
.progress-striped .progress-bar-danger {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.media {
  margin-top: 15px;
}
.media:first-child {
  margin-top: 0;
}
.media,
.media-body {
  zoom: 1;
  overflow: hidden;
}
.media-body {
  width: 10000px;
}
.media-object {
  display: block;
}
.media-object.img-thumbnail {
  max-width: none;
}
.media-right,
.media > .pull-right {
  padding-left: 10px;
}
.media-left,
.media > .pull-left {
  padding-right: 10px;
}
.media-left,
.media-right,
.media-body {
  display: table-cell;
  vertical-align: top;
}
.media-middle {
  vertical-align: middle;
}
.media-bottom {
  vertical-align: bottom;
}
.media-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.media-list {
  padding-left: 0;
  list-style: none;
}
.list-group {
  margin-bottom: 20px;
  padding-left: 0;
}
.list-group-item {
  position: relative;
  display: block;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
}
.list-group-item:first-child {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
}
.list-group-item:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
a.list-group-item,
button.list-group-item {
  color: #555;
}
a.list-group-item .list-group-item-heading,
button.list-group-item .list-group-item-heading {
  color: #333;
}
a.list-group-item:hover,
button.list-group-item:hover,
a.list-group-item:focus,
button.list-group-item:focus {
  text-decoration: none;
  color: #555;
  background-color: #f5f5f5;
}
button.list-group-item {
  width: 100%;
  text-align: left;
}
.list-group-item.disabled,
.list-group-item.disabled:hover,
.list-group-item.disabled:focus {
  background-color: #eeeeee;
  color: #777777;
  cursor: not-allowed;
}
.list-group-item.disabled .list-group-item-heading,
.list-group-item.disabled:hover .list-group-item-heading,
.list-group-item.disabled:focus .list-group-item-heading {
  color: inherit;
}
.list-group-item.disabled .list-group-item-text,
.list-group-item.disabled:hover .list-group-item-text,
.list-group-item.disabled:focus .list-group-item-text {
  color: #777777;
}
.list-group-item.active,
.list-group-item.active:hover,
.list-group-item.active:focus {
  z-index: 2;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.list-group-item.active .list-group-item-heading,
.list-group-item.active:hover .list-group-item-heading,
.list-group-item.active:focus .list-group-item-heading,
.list-group-item.active .list-group-item-heading > small,
.list-group-item.active:hover .list-group-item-heading > small,
.list-group-item.active:focus .list-group-item-heading > small,
.list-group-item.active .list-group-item-heading > .small,
.list-group-item.active:hover .list-group-item-heading > .small,
.list-group-item.active:focus .list-group-item-heading > .small {
  color: inherit;
}
.list-group-item.active .list-group-item-text,
.list-group-item.active:hover .list-group-item-text,
.list-group-item.active:focus .list-group-item-text {
  color: #c7ddef;
}
.list-group-item-success {
  color: #3c763d;
  background-color: #dff0d8;
}
a.list-group-item-success,
button.list-group-item-success {
  color: #3c763d;
}
a.list-group-item-success .list-group-item-heading,
button.list-group-item-success .list-group-item-heading {
  color: inherit;
}
a.list-group-item-success:hover,
button.list-group-item-success:hover,
a.list-group-item-success:focus,
button.list-group-item-success:focus {
  color: #3c763d;
  background-color: #d0e9c6;
}
a.list-group-item-success.active,
button.list-group-item-success.active,
a.list-group-item-success.active:hover,
button.list-group-item-success.active:hover,
a.list-group-item-success.active:focus,
button.list-group-item-success.active:focus {
  color: #fff;
  background-color: #3c763d;
  border-color: #3c763d;
}
.list-group-item-info {
  color: #31708f;
  background-color: #d9edf7;
}
a.list-group-item-info,
button.list-group-item-info {
  color: #31708f;
}
a.list-group-item-info .list-group-item-heading,
button.list-group-item-info .list-group-item-heading {
  color: inherit;
}
a.list-group-item-info:hover,
button.list-group-item-info:hover,
a.list-group-item-info:focus,
button.list-group-item-info:focus {
  color: #31708f;
  background-color: #c4e3f3;
}
a.list-group-item-info.active,
button.list-group-item-info.active,
a.list-group-item-info.active:hover,
button.list-group-item-info.active:hover,
a.list-group-item-info.active:focus,
button.list-group-item-info.active:focus {
  color: #fff;
  background-color: #31708f;
  border-color: #31708f;
}
.list-group-item-warning {
  color: #8a6d3b;
  background-color: #fcf8e3;
}
a.list-group-item-warning,
button.list-group-item-warning {
  color: #8a6d3b;
}
a.list-group-item-warning .list-group-item-heading,
button.list-group-item-warning .list-group-item-heading {
  color: inherit;
}
a.list-group-item-warning:hover,
button.list-group-item-warning:hover,
a.list-group-item-warning:focus,
button.list-group-item-warning:focus {
  color: #8a6d3b;
  background-color: #faf2cc;
}
a.list-group-item-warning.active,
button.list-group-item-warning.active,
a.list-group-item-warning.active:hover,
button.list-group-item-warning.active:hover,
a.list-group-item-warning.active:focus,
button.list-group-item-warning.active:focus {
  color: #fff;
  background-color: #8a6d3b;
  border-color: #8a6d3b;
}
.list-group-item-danger {
  color: #a94442;
  background-color: #f2dede;
}
a.list-group-item-danger,
button.list-group-item-danger {
  color: #a94442;
}
a.list-group-item-danger .list-group-item-heading,
button.list-group-item-danger .list-group-item-heading {
  color: inherit;
}
a.list-group-item-danger:hover,
button.list-group-item-danger:hover,
a.list-group-item-danger:focus,
button.list-group-item-danger:focus {
  color: #a94442;
  background-color: #ebcccc;
}
a.list-group-item-danger.active,
button.list-group-item-danger.active,
a.list-group-item-danger.active:hover,
button.list-group-item-danger.active:hover,
a.list-group-item-danger.active:focus,
button.list-group-item-danger.active:focus {
  color: #fff;
  background-color: #a94442;
  border-color: #a94442;
}
.list-group-item-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.list-group-item-text {
  margin-bottom: 0;
  line-height: 1.3;
}
.panel {
  margin-bottom: 18px;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
}
.panel-body {
  padding: 15px;
}
.panel-heading {
  padding: 10px 15px;
  border-bottom: 1px solid transparent;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel-heading > .dropdown .dropdown-toggle {
  color: inherit;
}
.panel-title {
  margin-top: 0;
  margin-bottom: 0;
  font-size: 15px;
  color: inherit;
}
.panel-title > a,
.panel-title > small,
.panel-title > .small,
.panel-title > small > a,
.panel-title > .small > a {
  color: inherit;
}
.panel-footer {
  padding: 10px 15px;
  background-color: #f5f5f5;
  border-top: 1px solid #ddd;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .list-group,
.panel > .panel-collapse > .list-group {
  margin-bottom: 0;
}
.panel > .list-group .list-group-item,
.panel > .panel-collapse > .list-group .list-group-item {
  border-width: 1px 0;
  border-radius: 0;
}
.panel > .list-group:first-child .list-group-item:first-child,
.panel > .panel-collapse > .list-group:first-child .list-group-item:first-child {
  border-top: 0;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .list-group:last-child .list-group-item:last-child,
.panel > .panel-collapse > .list-group:last-child .list-group-item:last-child {
  border-bottom: 0;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .panel-heading + .panel-collapse > .list-group .list-group-item:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.panel-heading + .list-group .list-group-item:first-child {
  border-top-width: 0;
}
.list-group + .panel-footer {
  border-top-width: 0;
}
.panel > .table,
.panel > .table-responsive > .table,
.panel > .panel-collapse > .table {
  margin-bottom: 0;
}
.panel > .table caption,
.panel > .table-responsive > .table caption,
.panel > .panel-collapse > .table caption {
  padding-left: 15px;
  padding-right: 15px;
}
.panel > .table:first-child,
.panel > .table-responsive:first-child > .table:first-child {
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child {
  border-top-left-radius: 1px;
  border-top-right-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:first-child {
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:last-child {
  border-top-right-radius: 1px;
}
.panel > .table:last-child,
.panel > .table-responsive:last-child > .table:last-child {
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child {
  border-bottom-left-radius: 1px;
  border-bottom-right-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:first-child {
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:last-child {
  border-bottom-right-radius: 1px;
}
.panel > .panel-body + .table,
.panel > .panel-body + .table-responsive,
.panel > .table + .panel-body,
.panel > .table-responsive + .panel-body {
  border-top: 1px solid #ddd;
}
.panel > .table > tbody:first-child > tr:first-child th,
.panel > .table > tbody:first-child > tr:first-child td {
  border-top: 0;
}
.panel > .table-bordered,
.panel > .table-responsive > .table-bordered {
  border: 0;
}
.panel > .table-bordered > thead > tr > th:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:first-child,
.panel > .table-bordered > tbody > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:first-child,
.panel > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-bordered > thead > tr > td:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:first-child,
.panel > .table-bordered > tbody > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:first-child,
.panel > .table-bordered > tfoot > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:first-child {
  border-left: 0;
}
.panel > .table-bordered > thead > tr > th:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:last-child,
.panel > .table-bordered > tbody > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:last-child,
.panel > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-bordered > thead > tr > td:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:last-child,
.panel > .table-bordered > tbody > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:last-child,
.panel > .table-bordered > tfoot > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:last-child {
  border-right: 0;
}
.panel > .table-bordered > thead > tr:first-child > td,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > td,
.panel > .table-bordered > tbody > tr:first-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > td,
.panel > .table-bordered > thead > tr:first-child > th,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > th,
.panel > .table-bordered > tbody > tr:first-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > th {
  border-bottom: 0;
}
.panel > .table-bordered > tbody > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > td,
.panel > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-bordered > tbody > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > th,
.panel > .table-bordered > tfoot > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > th {
  border-bottom: 0;
}
.panel > .table-responsive {
  border: 0;
  margin-bottom: 0;
}
.panel-group {
  margin-bottom: 18px;
}
.panel-group .panel {
  margin-bottom: 0;
  border-radius: 2px;
}
.panel-group .panel + .panel {
  margin-top: 5px;
}
.panel-group .panel-heading {
  border-bottom: 0;
}
.panel-group .panel-heading + .panel-collapse > .panel-body,
.panel-group .panel-heading + .panel-collapse > .list-group {
  border-top: 1px solid #ddd;
}
.panel-group .panel-footer {
  border-top: 0;
}
.panel-group .panel-footer + .panel-collapse .panel-body {
  border-bottom: 1px solid #ddd;
}
.panel-default {
  border-color: #ddd;
}
.panel-default > .panel-heading {
  color: #333333;
  background-color: #f5f5f5;
  border-color: #ddd;
}
.panel-default > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ddd;
}
.panel-default > .panel-heading .badge {
  color: #f5f5f5;
  background-color: #333333;
}
.panel-default > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ddd;
}
.panel-primary {
  border-color: #337ab7;
}
.panel-primary > .panel-heading {
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.panel-primary > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #337ab7;
}
.panel-primary > .panel-heading .badge {
  color: #337ab7;
  background-color: #fff;
}
.panel-primary > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #337ab7;
}
.panel-success {
  border-color: #d6e9c6;
}
.panel-success > .panel-heading {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
.panel-success > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #d6e9c6;
}
.panel-success > .panel-heading .badge {
  color: #dff0d8;
  background-color: #3c763d;
}
.panel-success > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #d6e9c6;
}
.panel-info {
  border-color: #bce8f1;
}
.panel-info > .panel-heading {
  color: #31708f;
  background-color: #d9edf7;
  border-color: #bce8f1;
}
.panel-info > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #bce8f1;
}
.panel-info > .panel-heading .badge {
  color: #d9edf7;
  background-color: #31708f;
}
.panel-info > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #bce8f1;
}
.panel-warning {
  border-color: #faebcc;
}
.panel-warning > .panel-heading {
  color: #8a6d3b;
  background-color: #fcf8e3;
  border-color: #faebcc;
}
.panel-warning > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #faebcc;
}
.panel-warning > .panel-heading .badge {
  color: #fcf8e3;
  background-color: #8a6d3b;
}
.panel-warning > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #faebcc;
}
.panel-danger {
  border-color: #ebccd1;
}
.panel-danger > .panel-heading {
  color: #a94442;
  background-color: #f2dede;
  border-color: #ebccd1;
}
.panel-danger > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ebccd1;
}
.panel-danger > .panel-heading .badge {
  color: #f2dede;
  background-color: #a94442;
}
.panel-danger > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ebccd1;
}
.embed-responsive {
  position: relative;
  display: block;
  height: 0;
  padding: 0;
  overflow: hidden;
}
.embed-responsive .embed-responsive-item,
.embed-responsive iframe,
.embed-responsive embed,
.embed-responsive object,
.embed-responsive video {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  border: 0;
}
.embed-responsive-16by9 {
  padding-bottom: 56.25%;
}
.embed-responsive-4by3 {
  padding-bottom: 75%;
}
.well {
  min-height: 20px;
  padding: 19px;
  margin-bottom: 20px;
  background-color: #f5f5f5;
  border: 1px solid #e3e3e3;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
}
.well blockquote {
  border-color: #ddd;
  border-color: rgba(0, 0, 0, 0.15);
}
.well-lg {
  padding: 24px;
  border-radius: 3px;
}
.well-sm {
  padding: 9px;
  border-radius: 1px;
}
.close {
  float: right;
  font-size: 19.5px;
  font-weight: bold;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.2;
  filter: alpha(opacity=20);
}
.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
  opacity: 0.5;
  filter: alpha(opacity=50);
}
button.close {
  padding: 0;
  cursor: pointer;
  background: transparent;
  border: 0;
  -webkit-appearance: none;
}
.modal-open {
  overflow: hidden;
}
.modal {
  display: none;
  overflow: hidden;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1050;
  -webkit-overflow-scrolling: touch;
  outline: 0;
}
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, -25%);
  -ms-transform: translate(0, -25%);
  -o-transform: translate(0, -25%);
  transform: translate(0, -25%);
  -webkit-transition: -webkit-transform 0.3s ease-out;
  -moz-transition: -moz-transform 0.3s ease-out;
  -o-transition: -o-transform 0.3s ease-out;
  transition: transform 0.3s ease-out;
}
.modal.in .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
.modal-open .modal {
  overflow-x: hidden;
  overflow-y: auto;
}
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}
.modal-content {
  position: relative;
  background-color: #fff;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  background-clip: padding-box;
  outline: 0;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #000;
}
.modal-backdrop.fade {
  opacity: 0;
  filter: alpha(opacity=0);
}
.modal-backdrop.in {
  opacity: 0.5;
  filter: alpha(opacity=50);
}
.modal-header {
  padding: 15px;
  border-bottom: 1px solid #e5e5e5;
}
.modal-header .close {
  margin-top: -2px;
}
.modal-title {
  margin: 0;
  line-height: 1.42857143;
}
.modal-body {
  position: relative;
  padding: 15px;
}
.modal-footer {
  padding: 15px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
}
.modal-footer .btn + .btn {
  margin-left: 5px;
  margin-bottom: 0;
}
.modal-footer .btn-group .btn + .btn {
  margin-left: -1px;
}
.modal-footer .btn-block + .btn-block {
  margin-left: 0;
}
.modal-scrollbar-measure {
  position: absolute;
  top: -9999px;
  width: 50px;
  height: 50px;
  overflow: scroll;
}
@media (min-width: 768px) {
  .modal-dialog {
    width: 600px;
    margin: 30px auto;
  }
  .modal-content {
    -webkit-box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  }
  .modal-sm {
    width: 300px;
  }
}
@media (min-width: 992px) {
  .modal-lg {
    width: 900px;
  }
}
.tooltip {
  position: absolute;
  z-index: 1070;
  display: block;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 12px;
  opacity: 0;
  filter: alpha(opacity=0);
}
.tooltip.in {
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.tooltip.top {
  margin-top: -3px;
  padding: 5px 0;
}
.tooltip.right {
  margin-left: 3px;
  padding: 0 5px;
}
.tooltip.bottom {
  margin-top: 3px;
  padding: 5px 0;
}
.tooltip.left {
  margin-left: -3px;
  padding: 0 5px;
}
.tooltip-inner {
  max-width: 200px;
  padding: 3px 8px;
  color: #fff;
  text-align: center;
  background-color: #000;
  border-radius: 2px;
}
.tooltip-arrow {
  position: absolute;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.tooltip.top .tooltip-arrow {
  bottom: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-left .tooltip-arrow {
  bottom: 0;
  right: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-right .tooltip-arrow {
  bottom: 0;
  left: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.right .tooltip-arrow {
  top: 50%;
  left: 0;
  margin-top: -5px;
  border-width: 5px 5px 5px 0;
  border-right-color: #000;
}
.tooltip.left .tooltip-arrow {
  top: 50%;
  right: 0;
  margin-top: -5px;
  border-width: 5px 0 5px 5px;
  border-left-color: #000;
}
.tooltip.bottom .tooltip-arrow {
  top: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-left .tooltip-arrow {
  top: 0;
  right: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-right .tooltip-arrow {
  top: 0;
  left: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.popover {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1060;
  display: none;
  max-width: 276px;
  padding: 1px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 13px;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}
.popover.top {
  margin-top: -10px;
}
.popover.right {
  margin-left: 10px;
}
.popover.bottom {
  margin-top: 10px;
}
.popover.left {
  margin-left: -10px;
}
.popover-title {
  margin: 0;
  padding: 8px 14px;
  font-size: 13px;
  background-color: #f7f7f7;
  border-bottom: 1px solid #ebebeb;
  border-radius: 2px 2px 0 0;
}
.popover-content {
  padding: 9px 14px;
}
.popover > .arrow,
.popover > .arrow:after {
  position: absolute;
  display: block;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.popover > .arrow {
  border-width: 11px;
}
.popover > .arrow:after {
  border-width: 10px;
  content: "";
}
.popover.top > .arrow {
  left: 50%;
  margin-left: -11px;
  border-bottom-width: 0;
  border-top-color: #999999;
  border-top-color: rgba(0, 0, 0, 0.25);
  bottom: -11px;
}
.popover.top > .arrow:after {
  content: " ";
  bottom: 1px;
  margin-left: -10px;
  border-bottom-width: 0;
  border-top-color: #fff;
}
.popover.right > .arrow {
  top: 50%;
  left: -11px;
  margin-top: -11px;
  border-left-width: 0;
  border-right-color: #999999;
  border-right-color: rgba(0, 0, 0, 0.25);
}
.popover.right > .arrow:after {
  content: " ";
  left: 1px;
  bottom: -10px;
  border-left-width: 0;
  border-right-color: #fff;
}
.popover.bottom > .arrow {
  left: 50%;
  margin-left: -11px;
  border-top-width: 0;
  border-bottom-color: #999999;
  border-bottom-color: rgba(0, 0, 0, 0.25);
  top: -11px;
}
.popover.bottom > .arrow:after {
  content: " ";
  top: 1px;
  margin-left: -10px;
  border-top-width: 0;
  border-bottom-color: #fff;
}
.popover.left > .arrow {
  top: 50%;
  right: -11px;
  margin-top: -11px;
  border-right-width: 0;
  border-left-color: #999999;
  border-left-color: rgba(0, 0, 0, 0.25);
}
.popover.left > .arrow:after {
  content: " ";
  right: 1px;
  border-right-width: 0;
  border-left-color: #fff;
  bottom: -10px;
}
.carousel {
  position: relative;
}
.carousel-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
}
.carousel-inner > .item {
  display: none;
  position: relative;
  -webkit-transition: 0.6s ease-in-out left;
  -o-transition: 0.6s ease-in-out left;
  transition: 0.6s ease-in-out left;
}
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  line-height: 1;
}
@media all and (transform-3d), (-webkit-transform-3d) {
  .carousel-inner > .item {
    -webkit-transition: -webkit-transform 0.6s ease-in-out;
    -moz-transition: -moz-transform 0.6s ease-in-out;
    -o-transition: -o-transform 0.6s ease-in-out;
    transition: transform 0.6s ease-in-out;
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-perspective: 1000px;
    -moz-perspective: 1000px;
    perspective: 1000px;
  }
  .carousel-inner > .item.next,
  .carousel-inner > .item.active.right {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.prev,
  .carousel-inner > .item.active.left {
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.next.left,
  .carousel-inner > .item.prev.right,
  .carousel-inner > .item.active {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
    left: 0;
  }
}
.carousel-inner > .active,
.carousel-inner > .next,
.carousel-inner > .prev {
  display: block;
}
.carousel-inner > .active {
  left: 0;
}
.carousel-inner > .next,
.carousel-inner > .prev {
  position: absolute;
  top: 0;
  width: 100%;
}
.carousel-inner > .next {
  left: 100%;
}
.carousel-inner > .prev {
  left: -100%;
}
.carousel-inner > .next.left,
.carousel-inner > .prev.right {
  left: 0;
}
.carousel-inner > .active.left {
  left: -100%;
}
.carousel-inner > .active.right {
  left: 100%;
}
.carousel-control {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 15%;
  opacity: 0.5;
  filter: alpha(opacity=50);
  font-size: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
  background-color: rgba(0, 0, 0, 0);
}
.carousel-control.left {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#80000000', endColorstr='#00000000', GradientType=1);
}
.carousel-control.right {
  left: auto;
  right: 0;
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#00000000', endColorstr='#80000000', GradientType=1);
}
.carousel-control:hover,
.carousel-control:focus {
  outline: 0;
  color: #fff;
  text-decoration: none;
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.carousel-control .icon-prev,
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-left,
.carousel-control .glyphicon-chevron-right {
  position: absolute;
  top: 50%;
  margin-top: -10px;
  z-index: 5;
  display: inline-block;
}
.carousel-control .icon-prev,
.carousel-control .glyphicon-chevron-left {
  left: 50%;
  margin-left: -10px;
}
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-right {
  right: 50%;
  margin-right: -10px;
}
.carousel-control .icon-prev,
.carousel-control .icon-next {
  width: 20px;
  height: 20px;
  line-height: 1;
  font-family: serif;
}
.carousel-control .icon-prev:before {
  content: '\2039';
}
.carousel-control .icon-next:before {
  content: '\203a';
}
.carousel-indicators {
  position: absolute;
  bottom: 10px;
  left: 50%;
  z-index: 15;
  width: 60%;
  margin-left: -30%;
  padding-left: 0;
  list-style: none;
  text-align: center;
}
.carousel-indicators li {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 1px;
  text-indent: -999px;
  border: 1px solid #fff;
  border-radius: 10px;
  cursor: pointer;
  background-color: #000 \9;
  background-color: rgba(0, 0, 0, 0);
}
.carousel-indicators .active {
  margin: 0;
  width: 12px;
  height: 12px;
  background-color: #fff;
}
.carousel-caption {
  position: absolute;
  left: 15%;
  right: 15%;
  bottom: 20px;
  z-index: 10;
  padding-top: 20px;
  padding-bottom: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
}
.carousel-caption .btn {
  text-shadow: none;
}
@media screen and (min-width: 768px) {
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-prev,
  .carousel-control .icon-next {
    width: 30px;
    height: 30px;
    margin-top: -10px;
    font-size: 30px;
  }
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .icon-prev {
    margin-left: -10px;
  }
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-next {
    margin-right: -10px;
  }
  .carousel-caption {
    left: 20%;
    right: 20%;
    padding-bottom: 30px;
  }
  .carousel-indicators {
    bottom: 20px;
  }
}
.clearfix:before,
.clearfix:after,
.dl-horizontal dd:before,
.dl-horizontal dd:after,
.container:before,
.container:after,
.container-fluid:before,
.container-fluid:after,
.row:before,
.row:after,
.form-horizontal .form-group:before,
.form-horizontal .form-group:after,
.btn-toolbar:before,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:before,
.btn-group-vertical > .btn-group:after,
.nav:before,
.nav:after,
.navbar:before,
.navbar:after,
.navbar-header:before,
.navbar-header:after,
.navbar-collapse:before,
.navbar-collapse:after,
.pager:before,
.pager:after,
.panel-body:before,
.panel-body:after,
.modal-header:before,
.modal-header:after,
.modal-footer:before,
.modal-footer:after,
.item_buttons:before,
.item_buttons:after {
  content: " ";
  display: table;
}
.clearfix:after,
.dl-horizontal dd:after,
.container:after,
.container-fluid:after,
.row:after,
.form-horizontal .form-group:after,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:after,
.nav:after,
.navbar:after,
.navbar-header:after,
.navbar-collapse:after,
.pager:after,
.panel-body:after,
.modal-header:after,
.modal-footer:after,
.item_buttons:after {
  clear: both;
}
.center-block {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.pull-right {
  float: right !important;
}
.pull-left {
  float: left !important;
}
.hide {
  display: none !important;
}
.show {
  display: block !important;
}
.invisible {
  visibility: hidden;
}
.text-hide {
  font: 0/0 a;
  color: transparent;
  text-shadow: none;
  background-color: transparent;
  border: 0;
}
.hidden {
  display: none !important;
}
.affix {
  position: fixed;
}
@-ms-viewport {
  width: device-width;
}
.visible-xs,
.visible-sm,
.visible-md,
.visible-lg {
  display: none !important;
}
.visible-xs-block,
.visible-xs-inline,
.visible-xs-inline-block,
.visible-sm-block,
.visible-sm-inline,
.visible-sm-inline-block,
.visible-md-block,
.visible-md-inline,
.visible-md-inline-block,
.visible-lg-block,
.visible-lg-inline,
.visible-lg-inline-block {
  display: none !important;
}
@media (max-width: 767px) {
  .visible-xs {
    display: block !important;
  }
  table.visible-xs {
    display: table !important;
  }
  tr.visible-xs {
    display: table-row !important;
  }
  th.visible-xs,
  td.visible-xs {
    display: table-cell !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-block {
    display: block !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline {
    display: inline !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm {
    display: block !important;
  }
  table.visible-sm {
    display: table !important;
  }
  tr.visible-sm {
    display: table-row !important;
  }
  th.visible-sm,
  td.visible-sm {
    display: table-cell !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-block {
    display: block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline {
    display: inline !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md {
    display: block !important;
  }
  table.visible-md {
    display: table !important;
  }
  tr.visible-md {
    display: table-row !important;
  }
  th.visible-md,
  td.visible-md {
    display: table-cell !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-block {
    display: block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline {
    display: inline !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg {
    display: block !important;
  }
  table.visible-lg {
    display: table !important;
  }
  tr.visible-lg {
    display: table-row !important;
  }
  th.visible-lg,
  td.visible-lg {
    display: table-cell !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-block {
    display: block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline {
    display: inline !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline-block {
    display: inline-block !important;
  }
}
@media (max-width: 767px) {
  .hidden-xs {
    display: none !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .hidden-sm {
    display: none !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .hidden-md {
    display: none !important;
  }
}
@media (min-width: 1200px) {
  .hidden-lg {
    display: none !important;
  }
}
.visible-print {
  display: none !important;
}
@media print {
  .visible-print {
    display: block !important;
  }
  table.visible-print {
    display: table !important;
  }
  tr.visible-print {
    display: table-row !important;
  }
  th.visible-print,
  td.visible-print {
    display: table-cell !important;
  }
}
.visible-print-block {
  display: none !important;
}
@media print {
  .visible-print-block {
    display: block !important;
  }
}
.visible-print-inline {
  display: none !important;
}
@media print {
  .visible-print-inline {
    display: inline !important;
  }
}
.visible-print-inline-block {
  display: none !important;
}
@media print {
  .visible-print-inline-block {
    display: inline-block !important;
  }
}
@media print {
  .hidden-print {
    display: none !important;
  }
}
/*!
*
* Font Awesome
*
*/
/*!
 *  Font Awesome 4.7.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */
/* FONT PATH
 * -------------------------- */
@font-face {
  font-family: 'FontAwesome';
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.7.0');
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.7.0') format('embedded-opentype'), url('../components/font-awesome/fonts/fontawesome-webfont.woff2?v=4.7.0') format('woff2'), url('../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.7.0') format('woff'), url('../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.7.0') format('truetype'), url('../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.7.0#fontawesomeregular') format('svg');
  font-weight: normal;
  font-style: normal;
}
.fa {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* makes the font 33% larger relative to the icon container */
.fa-lg {
  font-size: 1.33333333em;
  line-height: 0.75em;
  vertical-align: -15%;
}
.fa-2x {
  font-size: 2em;
}
.fa-3x {
  font-size: 3em;
}
.fa-4x {
  font-size: 4em;
}
.fa-5x {
  font-size: 5em;
}
.fa-fw {
  width: 1.28571429em;
  text-align: center;
}
.fa-ul {
  padding-left: 0;
  margin-left: 2.14285714em;
  list-style-type: none;
}
.fa-ul > li {
  position: relative;
}
.fa-li {
  position: absolute;
  left: -2.14285714em;
  width: 2.14285714em;
  top: 0.14285714em;
  text-align: center;
}
.fa-li.fa-lg {
  left: -1.85714286em;
}
.fa-border {
  padding: .2em .25em .15em;
  border: solid 0.08em #eee;
  border-radius: .1em;
}
.fa-pull-left {
  float: left;
}
.fa-pull-right {
  float: right;
}
.fa.fa-pull-left {
  margin-right: .3em;
}
.fa.fa-pull-right {
  margin-left: .3em;
}
/* Deprecated as of 4.4.0 */
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
.fa.pull-left {
  margin-right: .3em;
}
.fa.pull-right {
  margin-left: .3em;
}
.fa-spin {
  -webkit-animation: fa-spin 2s infinite linear;
  animation: fa-spin 2s infinite linear;
}
.fa-pulse {
  -webkit-animation: fa-spin 1s infinite steps(8);
  animation: fa-spin 1s infinite steps(8);
}
@-webkit-keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
@keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
.fa-rotate-90 {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=1)";
  -webkit-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
}
.fa-rotate-180 {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=2)";
  -webkit-transform: rotate(180deg);
  -ms-transform: rotate(180deg);
  transform: rotate(180deg);
}
.fa-rotate-270 {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=3)";
  -webkit-transform: rotate(270deg);
  -ms-transform: rotate(270deg);
  transform: rotate(270deg);
}
.fa-flip-horizontal {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1)";
  -webkit-transform: scale(-1, 1);
  -ms-transform: scale(-1, 1);
  transform: scale(-1, 1);
}
.fa-flip-vertical {
  -ms-filter: "progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1)";
  -webkit-transform: scale(1, -1);
  -ms-transform: scale(1, -1);
  transform: scale(1, -1);
}
:root .fa-rotate-90,
:root .fa-rotate-180,
:root .fa-rotate-270,
:root .fa-flip-horizontal,
:root .fa-flip-vertical {
  filter: none;
}
.fa-stack {
  position: relative;
  display: inline-block;
  width: 2em;
  height: 2em;
  line-height: 2em;
  vertical-align: middle;
}
.fa-stack-1x,
.fa-stack-2x {
  position: absolute;
  left: 0;
  width: 100%;
  text-align: center;
}
.fa-stack-1x {
  line-height: inherit;
}
.fa-stack-2x {
  font-size: 2em;
}
.fa-inverse {
  color: #fff;
}
/* Font Awesome uses the Unicode Private Use Area (PUA) to ensure screen
   readers do not read off random characters that represent icons */
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}
.fa-star:before {
  content: "\f005";
}
.fa-star-o:before {
  content: "\f006";
}
.fa-user:before {
  content: "\f007";
}
.fa-film:before {
  content: "\f008";
}
.fa-th-large:before {
  content: "\f009";
}
.fa-th:before {
  content: "\f00a";
}
.fa-th-list:before {
  content: "\f00b";
}
.fa-check:before {
  content: "\f00c";
}
.fa-remove:before,
.fa-close:before,
.fa-times:before {
  content: "\f00d";
}
.fa-search-plus:before {
  content: "\f00e";
}
.fa-search-minus:before {
  content: "\f010";
}
.fa-power-off:before {
  content: "\f011";
}
.fa-signal:before {
  content: "\f012";
}
.fa-gear:before,
.fa-cog:before {
  content: "\f013";
}
.fa-trash-o:before {
  content: "\f014";
}
.fa-home:before {
  content: "\f015";
}
.fa-file-o:before {
  content: "\f016";
}
.fa-clock-o:before {
  content: "\f017";
}
.fa-road:before {
  content: "\f018";
}
.fa-download:before {
  content: "\f019";
}
.fa-arrow-circle-o-down:before {
  content: "\f01a";
}
.fa-arrow-circle-o-up:before {
  content: "\f01b";
}
.fa-inbox:before {
  content: "\f01c";
}
.fa-play-circle-o:before {
  content: "\f01d";
}
.fa-rotate-right:before,
.fa-repeat:before {
  content: "\f01e";
}
.fa-refresh:before {
  content: "\f021";
}
.fa-list-alt:before {
  content: "\f022";
}
.fa-lock:before {
  content: "\f023";
}
.fa-flag:before {
  content: "\f024";
}
.fa-headphones:before {
  content: "\f025";
}
.fa-volume-off:before {
  content: "\f026";
}
.fa-volume-down:before {
  content: "\f027";
}
.fa-volume-up:before {
  content: "\f028";
}
.fa-qrcode:before {
  content: "\f029";
}
.fa-barcode:before {
  content: "\f02a";
}
.fa-tag:before {
  content: "\f02b";
}
.fa-tags:before {
  content: "\f02c";
}
.fa-book:before {
  content: "\f02d";
}
.fa-bookmark:before {
  content: "\f02e";
}
.fa-print:before {
  content: "\f02f";
}
.fa-camera:before {
  content: "\f030";
}
.fa-font:before {
  content: "\f031";
}
.fa-bold:before {
  content: "\f032";
}
.fa-italic:before {
  content: "\f033";
}
.fa-text-height:before {
  content: "\f034";
}
.fa-text-width:before {
  content: "\f035";
}
.fa-align-left:before {
  content: "\f036";
}
.fa-align-center:before {
  content: "\f037";
}
.fa-align-right:before {
  content: "\f038";
}
.fa-align-justify:before {
  content: "\f039";
}
.fa-list:before {
  content: "\f03a";
}
.fa-dedent:before,
.fa-outdent:before {
  content: "\f03b";
}
.fa-indent:before {
  content: "\f03c";
}
.fa-video-camera:before {
  content: "\f03d";
}
.fa-photo:before,
.fa-image:before,
.fa-picture-o:before {
  content: "\f03e";
}
.fa-pencil:before {
  content: "\f040";
}
.fa-map-marker:before {
  content: "\f041";
}
.fa-adjust:before {
  content: "\f042";
}
.fa-tint:before {
  content: "\f043";
}
.fa-edit:before,
.fa-pencil-square-o:before {
  content: "\f044";
}
.fa-share-square-o:before {
  content: "\f045";
}
.fa-check-square-o:before {
  content: "\f046";
}
.fa-arrows:before {
  content: "\f047";
}
.fa-step-backward:before {
  content: "\f048";
}
.fa-fast-backward:before {
  content: "\f049";
}
.fa-backward:before {
  content: "\f04a";
}
.fa-play:before {
  content: "\f04b";
}
.fa-pause:before {
  content: "\f04c";
}
.fa-stop:before {
  content: "\f04d";
}
.fa-forward:before {
  content: "\f04e";
}
.fa-fast-forward:before {
  content: "\f050";
}
.fa-step-forward:before {
  content: "\f051";
}
.fa-eject:before {
  content: "\f052";
}
.fa-chevron-left:before {
  content: "\f053";
}
.fa-chevron-right:before {
  content: "\f054";
}
.fa-plus-circle:before {
  content: "\f055";
}
.fa-minus-circle:before {
  content: "\f056";
}
.fa-times-circle:before {
  content: "\f057";
}
.fa-check-circle:before {
  content: "\f058";
}
.fa-question-circle:before {
  content: "\f059";
}
.fa-info-circle:before {
  content: "\f05a";
}
.fa-crosshairs:before {
  content: "\f05b";
}
.fa-times-circle-o:before {
  content: "\f05c";
}
.fa-check-circle-o:before {
  content: "\f05d";
}
.fa-ban:before {
  content: "\f05e";
}
.fa-arrow-left:before {
  content: "\f060";
}
.fa-arrow-right:before {
  content: "\f061";
}
.fa-arrow-up:before {
  content: "\f062";
}
.fa-arrow-down:before {
  content: "\f063";
}
.fa-mail-forward:before,
.fa-share:before {
  content: "\f064";
}
.fa-expand:before {
  content: "\f065";
}
.fa-compress:before {
  content: "\f066";
}
.fa-plus:before {
  content: "\f067";
}
.fa-minus:before {
  content: "\f068";
}
.fa-asterisk:before {
  content: "\f069";
}
.fa-exclamation-circle:before {
  content: "\f06a";
}
.fa-gift:before {
  content: "\f06b";
}
.fa-leaf:before {
  content: "\f06c";
}
.fa-fire:before {
  content: "\f06d";
}
.fa-eye:before {
  content: "\f06e";
}
.fa-eye-slash:before {
  content: "\f070";
}
.fa-warning:before,
.fa-exclamation-triangle:before {
  content: "\f071";
}
.fa-plane:before {
  content: "\f072";
}
.fa-calendar:before {
  content: "\f073";
}
.fa-random:before {
  content: "\f074";
}
.fa-comment:before {
  content: "\f075";
}
.fa-magnet:before {
  content: "\f076";
}
.fa-chevron-up:before {
  content: "\f077";
}
.fa-chevron-down:before {
  content: "\f078";
}
.fa-retweet:before {
  content: "\f079";
}
.fa-shopping-cart:before {
  content: "\f07a";
}
.fa-folder:before {
  content: "\f07b";
}
.fa-folder-open:before {
  content: "\f07c";
}
.fa-arrows-v:before {
  content: "\f07d";
}
.fa-arrows-h:before {
  content: "\f07e";
}
.fa-bar-chart-o:before,
.fa-bar-chart:before {
  content: "\f080";
}
.fa-twitter-square:before {
  content: "\f081";
}
.fa-facebook-square:before {
  content: "\f082";
}
.fa-camera-retro:before {
  content: "\f083";
}
.fa-key:before {
  content: "\f084";
}
.fa-gears:before,
.fa-cogs:before {
  content: "\f085";
}
.fa-comments:before {
  content: "\f086";
}
.fa-thumbs-o-up:before {
  content: "\f087";
}
.fa-thumbs-o-down:before {
  content: "\f088";
}
.fa-star-half:before {
  content: "\f089";
}
.fa-heart-o:before {
  content: "\f08a";
}
.fa-sign-out:before {
  content: "\f08b";
}
.fa-linkedin-square:before {
  content: "\f08c";
}
.fa-thumb-tack:before {
  content: "\f08d";
}
.fa-external-link:before {
  content: "\f08e";
}
.fa-sign-in:before {
  content: "\f090";
}
.fa-trophy:before {
  content: "\f091";
}
.fa-github-square:before {
  content: "\f092";
}
.fa-upload:before {
  content: "\f093";
}
.fa-lemon-o:before {
  content: "\f094";
}
.fa-phone:before {
  content: "\f095";
}
.fa-square-o:before {
  content: "\f096";
}
.fa-bookmark-o:before {
  content: "\f097";
}
.fa-phone-square:before {
  content: "\f098";
}
.fa-twitter:before {
  content: "\f099";
}
.fa-facebook-f:before,
.fa-facebook:before {
  content: "\f09a";
}
.fa-github:before {
  content: "\f09b";
}
.fa-unlock:before {
  content: "\f09c";
}
.fa-credit-card:before {
  content: "\f09d";
}
.fa-feed:before,
.fa-rss:before {
  content: "\f09e";
}
.fa-hdd-o:before {
  content: "\f0a0";
}
.fa-bullhorn:before {
  content: "\f0a1";
}
.fa-bell:before {
  content: "\f0f3";
}
.fa-certificate:before {
  content: "\f0a3";
}
.fa-hand-o-right:before {
  content: "\f0a4";
}
.fa-hand-o-left:before {
  content: "\f0a5";
}
.fa-hand-o-up:before {
  content: "\f0a6";
}
.fa-hand-o-down:before {
  content: "\f0a7";
}
.fa-arrow-circle-left:before {
  content: "\f0a8";
}
.fa-arrow-circle-right:before {
  content: "\f0a9";
}
.fa-arrow-circle-up:before {
  content: "\f0aa";
}
.fa-arrow-circle-down:before {
  content: "\f0ab";
}
.fa-globe:before {
  content: "\f0ac";
}
.fa-wrench:before {
  content: "\f0ad";
}
.fa-tasks:before {
  content: "\f0ae";
}
.fa-filter:before {
  content: "\f0b0";
}
.fa-briefcase:before {
  content: "\f0b1";
}
.fa-arrows-alt:before {
  content: "\f0b2";
}
.fa-group:before,
.fa-users:before {
  content: "\f0c0";
}
.fa-chain:before,
.fa-link:before {
  content: "\f0c1";
}
.fa-cloud:before {
  content: "\f0c2";
}
.fa-flask:before {
  content: "\f0c3";
}
.fa-cut:before,
.fa-scissors:before {
  content: "\f0c4";
}
.fa-copy:before,
.fa-files-o:before {
  content: "\f0c5";
}
.fa-paperclip:before {
  content: "\f0c6";
}
.fa-save:before,
.fa-floppy-o:before {
  content: "\f0c7";
}
.fa-square:before {
  content: "\f0c8";
}
.fa-navicon:before,
.fa-reorder:before,
.fa-bars:before {
  content: "\f0c9";
}
.fa-list-ul:before {
  content: "\f0ca";
}
.fa-list-ol:before {
  content: "\f0cb";
}
.fa-strikethrough:before {
  content: "\f0cc";
}
.fa-underline:before {
  content: "\f0cd";
}
.fa-table:before {
  content: "\f0ce";
}
.fa-magic:before {
  content: "\f0d0";
}
.fa-truck:before {
  content: "\f0d1";
}
.fa-pinterest:before {
  content: "\f0d2";
}
.fa-pinterest-square:before {
  content: "\f0d3";
}
.fa-google-plus-square:before {
  content: "\f0d4";
}
.fa-google-plus:before {
  content: "\f0d5";
}
.fa-money:before {
  content: "\f0d6";
}
.fa-caret-down:before {
  content: "\f0d7";
}
.fa-caret-up:before {
  content: "\f0d8";
}
.fa-caret-left:before {
  content: "\f0d9";
}
.fa-caret-right:before {
  content: "\f0da";
}
.fa-columns:before {
  content: "\f0db";
}
.fa-unsorted:before,
.fa-sort:before {
  content: "\f0dc";
}
.fa-sort-down:before,
.fa-sort-desc:before {
  content: "\f0dd";
}
.fa-sort-up:before,
.fa-sort-asc:before {
  content: "\f0de";
}
.fa-envelope:before {
  content: "\f0e0";
}
.fa-linkedin:before {
  content: "\f0e1";
}
.fa-rotate-left:before,
.fa-undo:before {
  content: "\f0e2";
}
.fa-legal:before,
.fa-gavel:before {
  content: "\f0e3";
}
.fa-dashboard:before,
.fa-tachometer:before {
  content: "\f0e4";
}
.fa-comment-o:before {
  content: "\f0e5";
}
.fa-comments-o:before {
  content: "\f0e6";
}
.fa-flash:before,
.fa-bolt:before {
  content: "\f0e7";
}
.fa-sitemap:before {
  content: "\f0e8";
}
.fa-umbrella:before {
  content: "\f0e9";
}
.fa-paste:before,
.fa-clipboard:before {
  content: "\f0ea";
}
.fa-lightbulb-o:before {
  content: "\f0eb";
}
.fa-exchange:before {
  content: "\f0ec";
}
.fa-cloud-download:before {
  content: "\f0ed";
}
.fa-cloud-upload:before {
  content: "\f0ee";
}
.fa-user-md:before {
  content: "\f0f0";
}
.fa-stethoscope:before {
  content: "\f0f1";
}
.fa-suitcase:before {
  content: "\f0f2";
}
.fa-bell-o:before {
  content: "\f0a2";
}
.fa-coffee:before {
  content: "\f0f4";
}
.fa-cutlery:before {
  content: "\f0f5";
}
.fa-file-text-o:before {
  content: "\f0f6";
}
.fa-building-o:before {
  content: "\f0f7";
}
.fa-hospital-o:before {
  content: "\f0f8";
}
.fa-ambulance:before {
  content: "\f0f9";
}
.fa-medkit:before {
  content: "\f0fa";
}
.fa-fighter-jet:before {
  content: "\f0fb";
}
.fa-beer:before {
  content: "\f0fc";
}
.fa-h-square:before {
  content: "\f0fd";
}
.fa-plus-square:before {
  content: "\f0fe";
}
.fa-angle-double-left:before {
  content: "\f100";
}
.fa-angle-double-right:before {
  content: "\f101";
}
.fa-angle-double-up:before {
  content: "\f102";
}
.fa-angle-double-down:before {
  content: "\f103";
}
.fa-angle-left:before {
  content: "\f104";
}
.fa-angle-right:before {
  content: "\f105";
}
.fa-angle-up:before {
  content: "\f106";
}
.fa-angle-down:before {
  content: "\f107";
}
.fa-desktop:before {
  content: "\f108";
}
.fa-laptop:before {
  content: "\f109";
}
.fa-tablet:before {
  content: "\f10a";
}
.fa-mobile-phone:before,
.fa-mobile:before {
  content: "\f10b";
}
.fa-circle-o:before {
  content: "\f10c";
}
.fa-quote-left:before {
  content: "\f10d";
}
.fa-quote-right:before {
  content: "\f10e";
}
.fa-spinner:before {
  content: "\f110";
}
.fa-circle:before {
  content: "\f111";
}
.fa-mail-reply:before,
.fa-reply:before {
  content: "\f112";
}
.fa-github-alt:before {
  content: "\f113";
}
.fa-folder-o:before {
  content: "\f114";
}
.fa-folder-open-o:before {
  content: "\f115";
}
.fa-smile-o:before {
  content: "\f118";
}
.fa-frown-o:before {
  content: "\f119";
}
.fa-meh-o:before {
  content: "\f11a";
}
.fa-gamepad:before {
  content: "\f11b";
}
.fa-keyboard-o:before {
  content: "\f11c";
}
.fa-flag-o:before {
  content: "\f11d";
}
.fa-flag-checkered:before {
  content: "\f11e";
}
.fa-terminal:before {
  content: "\f120";
}
.fa-code:before {
  content: "\f121";
}
.fa-mail-reply-all:before,
.fa-reply-all:before {
  content: "\f122";
}
.fa-star-half-empty:before,
.fa-star-half-full:before,
.fa-star-half-o:before {
  content: "\f123";
}
.fa-location-arrow:before {
  content: "\f124";
}
.fa-crop:before {
  content: "\f125";
}
.fa-code-fork:before {
  content: "\f126";
}
.fa-unlink:before,
.fa-chain-broken:before {
  content: "\f127";
}
.fa-question:before {
  content: "\f128";
}
.fa-info:before {
  content: "\f129";
}
.fa-exclamation:before {
  content: "\f12a";
}
.fa-superscript:before {
  content: "\f12b";
}
.fa-subscript:before {
  content: "\f12c";
}
.fa-eraser:before {
  content: "\f12d";
}
.fa-puzzle-piece:before {
  content: "\f12e";
}
.fa-microphone:before {
  content: "\f130";
}
.fa-microphone-slash:before {
  content: "\f131";
}
.fa-shield:before {
  content: "\f132";
}
.fa-calendar-o:before {
  content: "\f133";
}
.fa-fire-extinguisher:before {
  content: "\f134";
}
.fa-rocket:before {
  content: "\f135";
}
.fa-maxcdn:before {
  content: "\f136";
}
.fa-chevron-circle-left:before {
  content: "\f137";
}
.fa-chevron-circle-right:before {
  content: "\f138";
}
.fa-chevron-circle-up:before {
  content: "\f139";
}
.fa-chevron-circle-down:before {
  content: "\f13a";
}
.fa-html5:before {
  content: "\f13b";
}
.fa-css3:before {
  content: "\f13c";
}
.fa-anchor:before {
  content: "\f13d";
}
.fa-unlock-alt:before {
  content: "\f13e";
}
.fa-bullseye:before {
  content: "\f140";
}
.fa-ellipsis-h:before {
  content: "\f141";
}
.fa-ellipsis-v:before {
  content: "\f142";
}
.fa-rss-square:before {
  content: "\f143";
}
.fa-play-circle:before {
  content: "\f144";
}
.fa-ticket:before {
  content: "\f145";
}
.fa-minus-square:before {
  content: "\f146";
}
.fa-minus-square-o:before {
  content: "\f147";
}
.fa-level-up:before {
  content: "\f148";
}
.fa-level-down:before {
  content: "\f149";
}
.fa-check-square:before {
  content: "\f14a";
}
.fa-pencil-square:before {
  content: "\f14b";
}
.fa-external-link-square:before {
  content: "\f14c";
}
.fa-share-square:before {
  content: "\f14d";
}
.fa-compass:before {
  content: "\f14e";
}
.fa-toggle-down:before,
.fa-caret-square-o-down:before {
  content: "\f150";
}
.fa-toggle-up:before,
.fa-caret-square-o-up:before {
  content: "\f151";
}
.fa-toggle-right:before,
.fa-caret-square-o-right:before {
  content: "\f152";
}
.fa-euro:before,
.fa-eur:before {
  content: "\f153";
}
.fa-gbp:before {
  content: "\f154";
}
.fa-dollar:before,
.fa-usd:before {
  content: "\f155";
}
.fa-rupee:before,
.fa-inr:before {
  content: "\f156";
}
.fa-cny:before,
.fa-rmb:before,
.fa-yen:before,
.fa-jpy:before {
  content: "\f157";
}
.fa-ruble:before,
.fa-rouble:before,
.fa-rub:before {
  content: "\f158";
}
.fa-won:before,
.fa-krw:before {
  content: "\f159";
}
.fa-bitcoin:before,
.fa-btc:before {
  content: "\f15a";
}
.fa-file:before {
  content: "\f15b";
}
.fa-file-text:before {
  content: "\f15c";
}
.fa-sort-alpha-asc:before {
  content: "\f15d";
}
.fa-sort-alpha-desc:before {
  content: "\f15e";
}
.fa-sort-amount-asc:before {
  content: "\f160";
}
.fa-sort-amount-desc:before {
  content: "\f161";
}
.fa-sort-numeric-asc:before {
  content: "\f162";
}
.fa-sort-numeric-desc:before {
  content: "\f163";
}
.fa-thumbs-up:before {
  content: "\f164";
}
.fa-thumbs-down:before {
  content: "\f165";
}
.fa-youtube-square:before {
  content: "\f166";
}
.fa-youtube:before {
  content: "\f167";
}
.fa-xing:before {
  content: "\f168";
}
.fa-xing-square:before {
  content: "\f169";
}
.fa-youtube-play:before {
  content: "\f16a";
}
.fa-dropbox:before {
  content: "\f16b";
}
.fa-stack-overflow:before {
  content: "\f16c";
}
.fa-instagram:before {
  content: "\f16d";
}
.fa-flickr:before {
  content: "\f16e";
}
.fa-adn:before {
  content: "\f170";
}
.fa-bitbucket:before {
  content: "\f171";
}
.fa-bitbucket-square:before {
  content: "\f172";
}
.fa-tumblr:before {
  content: "\f173";
}
.fa-tumblr-square:before {
  content: "\f174";
}
.fa-long-arrow-down:before {
  content: "\f175";
}
.fa-long-arrow-up:before {
  content: "\f176";
}
.fa-long-arrow-left:before {
  content: "\f177";
}
.fa-long-arrow-right:before {
  content: "\f178";
}
.fa-apple:before {
  content: "\f179";
}
.fa-windows:before {
  content: "\f17a";
}
.fa-android:before {
  content: "\f17b";
}
.fa-linux:before {
  content: "\f17c";
}
.fa-dribbble:before {
  content: "\f17d";
}
.fa-skype:before {
  content: "\f17e";
}
.fa-foursquare:before {
  content: "\f180";
}
.fa-trello:before {
  content: "\f181";
}
.fa-female:before {
  content: "\f182";
}
.fa-male:before {
  content: "\f183";
}
.fa-gittip:before,
.fa-gratipay:before {
  content: "\f184";
}
.fa-sun-o:before {
  content: "\f185";
}
.fa-moon-o:before {
  content: "\f186";
}
.fa-archive:before {
  content: "\f187";
}
.fa-bug:before {
  content: "\f188";
}
.fa-vk:before {
  content: "\f189";
}
.fa-weibo:before {
  content: "\f18a";
}
.fa-renren:before {
  content: "\f18b";
}
.fa-pagelines:before {
  content: "\f18c";
}
.fa-stack-exchange:before {
  content: "\f18d";
}
.fa-arrow-circle-o-right:before {
  content: "\f18e";
}
.fa-arrow-circle-o-left:before {
  content: "\f190";
}
.fa-toggle-left:before,
.fa-caret-square-o-left:before {
  content: "\f191";
}
.fa-dot-circle-o:before {
  content: "\f192";
}
.fa-wheelchair:before {
  content: "\f193";
}
.fa-vimeo-square:before {
  content: "\f194";
}
.fa-turkish-lira:before,
.fa-try:before {
  content: "\f195";
}
.fa-plus-square-o:before {
  content: "\f196";
}
.fa-space-shuttle:before {
  content: "\f197";
}
.fa-slack:before {
  content: "\f198";
}
.fa-envelope-square:before {
  content: "\f199";
}
.fa-wordpress:before {
  content: "\f19a";
}
.fa-openid:before {
  content: "\f19b";
}
.fa-institution:before,
.fa-bank:before,
.fa-university:before {
  content: "\f19c";
}
.fa-mortar-board:before,
.fa-graduation-cap:before {
  content: "\f19d";
}
.fa-yahoo:before {
  content: "\f19e";
}
.fa-google:before {
  content: "\f1a0";
}
.fa-reddit:before {
  content: "\f1a1";
}
.fa-reddit-square:before {
  content: "\f1a2";
}
.fa-stumbleupon-circle:before {
  content: "\f1a3";
}
.fa-stumbleupon:before {
  content: "\f1a4";
}
.fa-delicious:before {
  content: "\f1a5";
}
.fa-digg:before {
  content: "\f1a6";
}
.fa-pied-piper-pp:before {
  content: "\f1a7";
}
.fa-pied-piper-alt:before {
  content: "\f1a8";
}
.fa-drupal:before {
  content: "\f1a9";
}
.fa-joomla:before {
  content: "\f1aa";
}
.fa-language:before {
  content: "\f1ab";
}
.fa-fax:before {
  content: "\f1ac";
}
.fa-building:before {
  content: "\f1ad";
}
.fa-child:before {
  content: "\f1ae";
}
.fa-paw:before {
  content: "\f1b0";
}
.fa-spoon:before {
  content: "\f1b1";
}
.fa-cube:before {
  content: "\f1b2";
}
.fa-cubes:before {
  content: "\f1b3";
}
.fa-behance:before {
  content: "\f1b4";
}
.fa-behance-square:before {
  content: "\f1b5";
}
.fa-steam:before {
  content: "\f1b6";
}
.fa-steam-square:before {
  content: "\f1b7";
}
.fa-recycle:before {
  content: "\f1b8";
}
.fa-automobile:before,
.fa-car:before {
  content: "\f1b9";
}
.fa-cab:before,
.fa-taxi:before {
  content: "\f1ba";
}
.fa-tree:before {
  content: "\f1bb";
}
.fa-spotify:before {
  content: "\f1bc";
}
.fa-deviantart:before {
  content: "\f1bd";
}
.fa-soundcloud:before {
  content: "\f1be";
}
.fa-database:before {
  content: "\f1c0";
}
.fa-file-pdf-o:before {
  content: "\f1c1";
}
.fa-file-word-o:before {
  content: "\f1c2";
}
.fa-file-excel-o:before {
  content: "\f1c3";
}
.fa-file-powerpoint-o:before {
  content: "\f1c4";
}
.fa-file-photo-o:before,
.fa-file-picture-o:before,
.fa-file-image-o:before {
  content: "\f1c5";
}
.fa-file-zip-o:before,
.fa-file-archive-o:before {
  content: "\f1c6";
}
.fa-file-sound-o:before,
.fa-file-audio-o:before {
  content: "\f1c7";
}
.fa-file-movie-o:before,
.fa-file-video-o:before {
  content: "\f1c8";
}
.fa-file-code-o:before {
  content: "\f1c9";
}
.fa-vine:before {
  content: "\f1ca";
}
.fa-codepen:before {
  content: "\f1cb";
}
.fa-jsfiddle:before {
  content: "\f1cc";
}
.fa-life-bouy:before,
.fa-life-buoy:before,
.fa-life-saver:before,
.fa-support:before,
.fa-life-ring:before {
  content: "\f1cd";
}
.fa-circle-o-notch:before {
  content: "\f1ce";
}
.fa-ra:before,
.fa-resistance:before,
.fa-rebel:before {
  content: "\f1d0";
}
.fa-ge:before,
.fa-empire:before {
  content: "\f1d1";
}
.fa-git-square:before {
  content: "\f1d2";
}
.fa-git:before {
  content: "\f1d3";
}
.fa-y-combinator-square:before,
.fa-yc-square:before,
.fa-hacker-news:before {
  content: "\f1d4";
}
.fa-tencent-weibo:before {
  content: "\f1d5";
}
.fa-qq:before {
  content: "\f1d6";
}
.fa-wechat:before,
.fa-weixin:before {
  content: "\f1d7";
}
.fa-send:before,
.fa-paper-plane:before {
  content: "\f1d8";
}
.fa-send-o:before,
.fa-paper-plane-o:before {
  content: "\f1d9";
}
.fa-history:before {
  content: "\f1da";
}
.fa-circle-thin:before {
  content: "\f1db";
}
.fa-header:before {
  content: "\f1dc";
}
.fa-paragraph:before {
  content: "\f1dd";
}
.fa-sliders:before {
  content: "\f1de";
}
.fa-share-alt:before {
  content: "\f1e0";
}
.fa-share-alt-square:before {
  content: "\f1e1";
}
.fa-bomb:before {
  content: "\f1e2";
}
.fa-soccer-ball-o:before,
.fa-futbol-o:before {
  content: "\f1e3";
}
.fa-tty:before {
  content: "\f1e4";
}
.fa-binoculars:before {
  content: "\f1e5";
}
.fa-plug:before {
  content: "\f1e6";
}
.fa-slideshare:before {
  content: "\f1e7";
}
.fa-twitch:before {
  content: "\f1e8";
}
.fa-yelp:before {
  content: "\f1e9";
}
.fa-newspaper-o:before {
  content: "\f1ea";
}
.fa-wifi:before {
  content: "\f1eb";
}
.fa-calculator:before {
  content: "\f1ec";
}
.fa-paypal:before {
  content: "\f1ed";
}
.fa-google-wallet:before {
  content: "\f1ee";
}
.fa-cc-visa:before {
  content: "\f1f0";
}
.fa-cc-mastercard:before {
  content: "\f1f1";
}
.fa-cc-discover:before {
  content: "\f1f2";
}
.fa-cc-amex:before {
  content: "\f1f3";
}
.fa-cc-paypal:before {
  content: "\f1f4";
}
.fa-cc-stripe:before {
  content: "\f1f5";
}
.fa-bell-slash:before {
  content: "\f1f6";
}
.fa-bell-slash-o:before {
  content: "\f1f7";
}
.fa-trash:before {
  content: "\f1f8";
}
.fa-copyright:before {
  content: "\f1f9";
}
.fa-at:before {
  content: "\f1fa";
}
.fa-eyedropper:before {
  content: "\f1fb";
}
.fa-paint-brush:before {
  content: "\f1fc";
}
.fa-birthday-cake:before {
  content: "\f1fd";
}
.fa-area-chart:before {
  content: "\f1fe";
}
.fa-pie-chart:before {
  content: "\f200";
}
.fa-line-chart:before {
  content: "\f201";
}
.fa-lastfm:before {
  content: "\f202";
}
.fa-lastfm-square:before {
  content: "\f203";
}
.fa-toggle-off:before {
  content: "\f204";
}
.fa-toggle-on:before {
  content: "\f205";
}
.fa-bicycle:before {
  content: "\f206";
}
.fa-bus:before {
  content: "\f207";
}
.fa-ioxhost:before {
  content: "\f208";
}
.fa-angellist:before {
  content: "\f209";
}
.fa-cc:before {
  content: "\f20a";
}
.fa-shekel:before,
.fa-sheqel:before,
.fa-ils:before {
  content: "\f20b";
}
.fa-meanpath:before {
  content: "\f20c";
}
.fa-buysellads:before {
  content: "\f20d";
}
.fa-connectdevelop:before {
  content: "\f20e";
}
.fa-dashcube:before {
  content: "\f210";
}
.fa-forumbee:before {
  content: "\f211";
}
.fa-leanpub:before {
  content: "\f212";
}
.fa-sellsy:before {
  content: "\f213";
}
.fa-shirtsinbulk:before {
  content: "\f214";
}
.fa-simplybuilt:before {
  content: "\f215";
}
.fa-skyatlas:before {
  content: "\f216";
}
.fa-cart-plus:before {
  content: "\f217";
}
.fa-cart-arrow-down:before {
  content: "\f218";
}
.fa-diamond:before {
  content: "\f219";
}
.fa-ship:before {
  content: "\f21a";
}
.fa-user-secret:before {
  content: "\f21b";
}
.fa-motorcycle:before {
  content: "\f21c";
}
.fa-street-view:before {
  content: "\f21d";
}
.fa-heartbeat:before {
  content: "\f21e";
}
.fa-venus:before {
  content: "\f221";
}
.fa-mars:before {
  content: "\f222";
}
.fa-mercury:before {
  content: "\f223";
}
.fa-intersex:before,
.fa-transgender:before {
  content: "\f224";
}
.fa-transgender-alt:before {
  content: "\f225";
}
.fa-venus-double:before {
  content: "\f226";
}
.fa-mars-double:before {
  content: "\f227";
}
.fa-venus-mars:before {
  content: "\f228";
}
.fa-mars-stroke:before {
  content: "\f229";
}
.fa-mars-stroke-v:before {
  content: "\f22a";
}
.fa-mars-stroke-h:before {
  content: "\f22b";
}
.fa-neuter:before {
  content: "\f22c";
}
.fa-genderless:before {
  content: "\f22d";
}
.fa-facebook-official:before {
  content: "\f230";
}
.fa-pinterest-p:before {
  content: "\f231";
}
.fa-whatsapp:before {
  content: "\f232";
}
.fa-server:before {
  content: "\f233";
}
.fa-user-plus:before {
  content: "\f234";
}
.fa-user-times:before {
  content: "\f235";
}
.fa-hotel:before,
.fa-bed:before {
  content: "\f236";
}
.fa-viacoin:before {
  content: "\f237";
}
.fa-train:before {
  content: "\f238";
}
.fa-subway:before {
  content: "\f239";
}
.fa-medium:before {
  content: "\f23a";
}
.fa-yc:before,
.fa-y-combinator:before {
  content: "\f23b";
}
.fa-optin-monster:before {
  content: "\f23c";
}
.fa-opencart:before {
  content: "\f23d";
}
.fa-expeditedssl:before {
  content: "\f23e";
}
.fa-battery-4:before,
.fa-battery:before,
.fa-battery-full:before {
  content: "\f240";
}
.fa-battery-3:before,
.fa-battery-three-quarters:before {
  content: "\f241";
}
.fa-battery-2:before,
.fa-battery-half:before {
  content: "\f242";
}
.fa-battery-1:before,
.fa-battery-quarter:before {
  content: "\f243";
}
.fa-battery-0:before,
.fa-battery-empty:before {
  content: "\f244";
}
.fa-mouse-pointer:before {
  content: "\f245";
}
.fa-i-cursor:before {
  content: "\f246";
}
.fa-object-group:before {
  content: "\f247";
}
.fa-object-ungroup:before {
  content: "\f248";
}
.fa-sticky-note:before {
  content: "\f249";
}
.fa-sticky-note-o:before {
  content: "\f24a";
}
.fa-cc-jcb:before {
  content: "\f24b";
}
.fa-cc-diners-club:before {
  content: "\f24c";
}
.fa-clone:before {
  content: "\f24d";
}
.fa-balance-scale:before {
  content: "\f24e";
}
.fa-hourglass-o:before {
  content: "\f250";
}
.fa-hourglass-1:before,
.fa-hourglass-start:before {
  content: "\f251";
}
.fa-hourglass-2:before,
.fa-hourglass-half:before {
  content: "\f252";
}
.fa-hourglass-3:before,
.fa-hourglass-end:before {
  content: "\f253";
}
.fa-hourglass:before {
  content: "\f254";
}
.fa-hand-grab-o:before,
.fa-hand-rock-o:before {
  content: "\f255";
}
.fa-hand-stop-o:before,
.fa-hand-paper-o:before {
  content: "\f256";
}
.fa-hand-scissors-o:before {
  content: "\f257";
}
.fa-hand-lizard-o:before {
  content: "\f258";
}
.fa-hand-spock-o:before {
  content: "\f259";
}
.fa-hand-pointer-o:before {
  content: "\f25a";
}
.fa-hand-peace-o:before {
  content: "\f25b";
}
.fa-trademark:before {
  content: "\f25c";
}
.fa-registered:before {
  content: "\f25d";
}
.fa-creative-commons:before {
  content: "\f25e";
}
.fa-gg:before {
  content: "\f260";
}
.fa-gg-circle:before {
  content: "\f261";
}
.fa-tripadvisor:before {
  content: "\f262";
}
.fa-odnoklassniki:before {
  content: "\f263";
}
.fa-odnoklassniki-square:before {
  content: "\f264";
}
.fa-get-pocket:before {
  content: "\f265";
}
.fa-wikipedia-w:before {
  content: "\f266";
}
.fa-safari:before {
  content: "\f267";
}
.fa-chrome:before {
  content: "\f268";
}
.fa-firefox:before {
  content: "\f269";
}
.fa-opera:before {
  content: "\f26a";
}
.fa-internet-explorer:before {
  content: "\f26b";
}
.fa-tv:before,
.fa-television:before {
  content: "\f26c";
}
.fa-contao:before {
  content: "\f26d";
}
.fa-500px:before {
  content: "\f26e";
}
.fa-amazon:before {
  content: "\f270";
}
.fa-calendar-plus-o:before {
  content: "\f271";
}
.fa-calendar-minus-o:before {
  content: "\f272";
}
.fa-calendar-times-o:before {
  content: "\f273";
}
.fa-calendar-check-o:before {
  content: "\f274";
}
.fa-industry:before {
  content: "\f275";
}
.fa-map-pin:before {
  content: "\f276";
}
.fa-map-signs:before {
  content: "\f277";
}
.fa-map-o:before {
  content: "\f278";
}
.fa-map:before {
  content: "\f279";
}
.fa-commenting:before {
  content: "\f27a";
}
.fa-commenting-o:before {
  content: "\f27b";
}
.fa-houzz:before {
  content: "\f27c";
}
.fa-vimeo:before {
  content: "\f27d";
}
.fa-black-tie:before {
  content: "\f27e";
}
.fa-fonticons:before {
  content: "\f280";
}
.fa-reddit-alien:before {
  content: "\f281";
}
.fa-edge:before {
  content: "\f282";
}
.fa-credit-card-alt:before {
  content: "\f283";
}
.fa-codiepie:before {
  content: "\f284";
}
.fa-modx:before {
  content: "\f285";
}
.fa-fort-awesome:before {
  content: "\f286";
}
.fa-usb:before {
  content: "\f287";
}
.fa-product-hunt:before {
  content: "\f288";
}
.fa-mixcloud:before {
  content: "\f289";
}
.fa-scribd:before {
  content: "\f28a";
}
.fa-pause-circle:before {
  content: "\f28b";
}
.fa-pause-circle-o:before {
  content: "\f28c";
}
.fa-stop-circle:before {
  content: "\f28d";
}
.fa-stop-circle-o:before {
  content: "\f28e";
}
.fa-shopping-bag:before {
  content: "\f290";
}
.fa-shopping-basket:before {
  content: "\f291";
}
.fa-hashtag:before {
  content: "\f292";
}
.fa-bluetooth:before {
  content: "\f293";
}
.fa-bluetooth-b:before {
  content: "\f294";
}
.fa-percent:before {
  content: "\f295";
}
.fa-gitlab:before {
  content: "\f296";
}
.fa-wpbeginner:before {
  content: "\f297";
}
.fa-wpforms:before {
  content: "\f298";
}
.fa-envira:before {
  content: "\f299";
}
.fa-universal-access:before {
  content: "\f29a";
}
.fa-wheelchair-alt:before {
  content: "\f29b";
}
.fa-question-circle-o:before {
  content: "\f29c";
}
.fa-blind:before {
  content: "\f29d";
}
.fa-audio-description:before {
  content: "\f29e";
}
.fa-volume-control-phone:before {
  content: "\f2a0";
}
.fa-braille:before {
  content: "\f2a1";
}
.fa-assistive-listening-systems:before {
  content: "\f2a2";
}
.fa-asl-interpreting:before,
.fa-american-sign-language-interpreting:before {
  content: "\f2a3";
}
.fa-deafness:before,
.fa-hard-of-hearing:before,
.fa-deaf:before {
  content: "\f2a4";
}
.fa-glide:before {
  content: "\f2a5";
}
.fa-glide-g:before {
  content: "\f2a6";
}
.fa-signing:before,
.fa-sign-language:before {
  content: "\f2a7";
}
.fa-low-vision:before {
  content: "\f2a8";
}
.fa-viadeo:before {
  content: "\f2a9";
}
.fa-viadeo-square:before {
  content: "\f2aa";
}
.fa-snapchat:before {
  content: "\f2ab";
}
.fa-snapchat-ghost:before {
  content: "\f2ac";
}
.fa-snapchat-square:before {
  content: "\f2ad";
}
.fa-pied-piper:before {
  content: "\f2ae";
}
.fa-first-order:before {
  content: "\f2b0";
}
.fa-yoast:before {
  content: "\f2b1";
}
.fa-themeisle:before {
  content: "\f2b2";
}
.fa-google-plus-circle:before,
.fa-google-plus-official:before {
  content: "\f2b3";
}
.fa-fa:before,
.fa-font-awesome:before {
  content: "\f2b4";
}
.fa-handshake-o:before {
  content: "\f2b5";
}
.fa-envelope-open:before {
  content: "\f2b6";
}
.fa-envelope-open-o:before {
  content: "\f2b7";
}
.fa-linode:before {
  content: "\f2b8";
}
.fa-address-book:before {
  content: "\f2b9";
}
.fa-address-book-o:before {
  content: "\f2ba";
}
.fa-vcard:before,
.fa-address-card:before {
  content: "\f2bb";
}
.fa-vcard-o:before,
.fa-address-card-o:before {
  content: "\f2bc";
}
.fa-user-circle:before {
  content: "\f2bd";
}
.fa-user-circle-o:before {
  content: "\f2be";
}
.fa-user-o:before {
  content: "\f2c0";
}
.fa-id-badge:before {
  content: "\f2c1";
}
.fa-drivers-license:before,
.fa-id-card:before {
  content: "\f2c2";
}
.fa-drivers-license-o:before,
.fa-id-card-o:before {
  content: "\f2c3";
}
.fa-quora:before {
  content: "\f2c4";
}
.fa-free-code-camp:before {
  content: "\f2c5";
}
.fa-telegram:before {
  content: "\f2c6";
}
.fa-thermometer-4:before,
.fa-thermometer:before,
.fa-thermometer-full:before {
  content: "\f2c7";
}
.fa-thermometer-3:before,
.fa-thermometer-three-quarters:before {
  content: "\f2c8";
}
.fa-thermometer-2:before,
.fa-thermometer-half:before {
  content: "\f2c9";
}
.fa-thermometer-1:before,
.fa-thermometer-quarter:before {
  content: "\f2ca";
}
.fa-thermometer-0:before,
.fa-thermometer-empty:before {
  content: "\f2cb";
}
.fa-shower:before {
  content: "\f2cc";
}
.fa-bathtub:before,
.fa-s15:before,
.fa-bath:before {
  content: "\f2cd";
}
.fa-podcast:before {
  content: "\f2ce";
}
.fa-window-maximize:before {
  content: "\f2d0";
}
.fa-window-minimize:before {
  content: "\f2d1";
}
.fa-window-restore:before {
  content: "\f2d2";
}
.fa-times-rectangle:before,
.fa-window-close:before {
  content: "\f2d3";
}
.fa-times-rectangle-o:before,
.fa-window-close-o:before {
  content: "\f2d4";
}
.fa-bandcamp:before {
  content: "\f2d5";
}
.fa-grav:before {
  content: "\f2d6";
}
.fa-etsy:before {
  content: "\f2d7";
}
.fa-imdb:before {
  content: "\f2d8";
}
.fa-ravelry:before {
  content: "\f2d9";
}
.fa-eercast:before {
  content: "\f2da";
}
.fa-microchip:before {
  content: "\f2db";
}
.fa-snowflake-o:before {
  content: "\f2dc";
}
.fa-superpowers:before {
  content: "\f2dd";
}
.fa-wpexplorer:before {
  content: "\f2de";
}
.fa-meetup:before {
  content: "\f2e0";
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
/*!
*
* IPython base
*
*/
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
code {
  color: #000;
}
pre {
  font-size: inherit;
  line-height: inherit;
}
label {
  font-weight: normal;
}
/* Make the page background atleast 100% the height of the view port */
/* Make the page itself atleast 70% the height of the view port */
.border-box-sizing {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.corner-all {
  border-radius: 2px;
}
.no-padding {
  padding: 0px;
}
/* Flexible box model classes */
/* Taken from Alex Russell http://infrequently.org/2009/08/css-3-progress/ */
/* This file is a compatability layer.  It allows the usage of flexible box 
model layouts accross multiple browsers, including older browsers.  The newest,
universal implementation of the flexible box model is used when available (see
`Modern browsers` comments below).  Browsers that are known to implement this 
new spec completely include:

    Firefox 28.0+
    Chrome 29.0+
    Internet Explorer 11+ 
    Opera 17.0+

Browsers not listed, including Safari, are supported via the styling under the
`Old browsers` comments below.
*/
.hbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
.hbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.vbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
.vbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.hbox.reverse,
.vbox.reverse,
.reverse {
  /* Old browsers */
  -webkit-box-direction: reverse;
  -moz-box-direction: reverse;
  box-direction: reverse;
  /* Modern browsers */
  flex-direction: row-reverse;
}
.hbox.box-flex0,
.vbox.box-flex0,
.box-flex0 {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
  width: auto;
}
.hbox.box-flex1,
.vbox.box-flex1,
.box-flex1 {
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex,
.vbox.box-flex,
.box-flex {
  /* Old browsers */
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex2,
.vbox.box-flex2,
.box-flex2 {
  /* Old browsers */
  -webkit-box-flex: 2;
  -moz-box-flex: 2;
  box-flex: 2;
  /* Modern browsers */
  flex: 2;
}
.box-group1 {
  /*  Deprecated */
  -webkit-box-flex-group: 1;
  -moz-box-flex-group: 1;
  box-flex-group: 1;
}
.box-group2 {
  /* Deprecated */
  -webkit-box-flex-group: 2;
  -moz-box-flex-group: 2;
  box-flex-group: 2;
}
.hbox.start,
.vbox.start,
.start {
  /* Old browsers */
  -webkit-box-pack: start;
  -moz-box-pack: start;
  box-pack: start;
  /* Modern browsers */
  justify-content: flex-start;
}
.hbox.end,
.vbox.end,
.end {
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
}
.hbox.center,
.vbox.center,
.center {
  /* Old browsers */
  -webkit-box-pack: center;
  -moz-box-pack: center;
  box-pack: center;
  /* Modern browsers */
  justify-content: center;
}
.hbox.baseline,
.vbox.baseline,
.baseline {
  /* Old browsers */
  -webkit-box-pack: baseline;
  -moz-box-pack: baseline;
  box-pack: baseline;
  /* Modern browsers */
  justify-content: baseline;
}
.hbox.stretch,
.vbox.stretch,
.stretch {
  /* Old browsers */
  -webkit-box-pack: stretch;
  -moz-box-pack: stretch;
  box-pack: stretch;
  /* Modern browsers */
  justify-content: stretch;
}
.hbox.align-start,
.vbox.align-start,
.align-start {
  /* Old browsers */
  -webkit-box-align: start;
  -moz-box-align: start;
  box-align: start;
  /* Modern browsers */
  align-items: flex-start;
}
.hbox.align-end,
.vbox.align-end,
.align-end {
  /* Old browsers */
  -webkit-box-align: end;
  -moz-box-align: end;
  box-align: end;
  /* Modern browsers */
  align-items: flex-end;
}
.hbox.align-center,
.vbox.align-center,
.align-center {
  /* Old browsers */
  -webkit-box-align: center;
  -moz-box-align: center;
  box-align: center;
  /* Modern browsers */
  align-items: center;
}
.hbox.align-baseline,
.vbox.align-baseline,
.align-baseline {
  /* Old browsers */
  -webkit-box-align: baseline;
  -moz-box-align: baseline;
  box-align: baseline;
  /* Modern browsers */
  align-items: baseline;
}
.hbox.align-stretch,
.vbox.align-stretch,
.align-stretch {
  /* Old browsers */
  -webkit-box-align: stretch;
  -moz-box-align: stretch;
  box-align: stretch;
  /* Modern browsers */
  align-items: stretch;
}
div.error {
  margin: 2em;
  text-align: center;
}
div.error > h1 {
  font-size: 500%;
  line-height: normal;
}
div.error > p {
  font-size: 200%;
  line-height: normal;
}
div.traceback-wrapper {
  text-align: left;
  max-width: 800px;
  margin: auto;
}
div.traceback-wrapper pre.traceback {
  max-height: 600px;
  overflow: auto;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
body {
  background-color: #fff;
  /* This makes sure that the body covers the entire window and needs to
       be in a different element than the display: box in wrapper below */
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  overflow: visible;
}
body > #header {
  /* Initially hidden to prevent FLOUC */
  display: none;
  background-color: #fff;
  /* Display over codemirror */
  position: relative;
  z-index: 100;
}
body > #header #header-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 5px;
  padding-bottom: 5px;
  padding-top: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
body > #header .header-bar {
  width: 100%;
  height: 1px;
  background: #e7e7e7;
  margin-bottom: -1px;
}
@media print {
  body > #header {
    display: none !important;
  }
}
#header-spacer {
  width: 100%;
  visibility: hidden;
}
@media print {
  #header-spacer {
    display: none;
  }
}
#ipython_notebook {
  padding-left: 0px;
  padding-top: 1px;
  padding-bottom: 1px;
}
[dir="rtl"] #ipython_notebook {
  margin-right: 10px;
  margin-left: 0;
}
[dir="rtl"] #ipython_notebook.pull-left {
  float: right !important;
  float: right;
}
.flex-spacer {
  flex: 1;
}
#noscript {
  width: auto;
  padding-top: 16px;
  padding-bottom: 16px;
  text-align: center;
  font-size: 22px;
  color: red;
  font-weight: bold;
}
#ipython_notebook img {
  height: 28px;
}
#site {
  width: 100%;
  display: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: auto;
}
@media print {
  #site {
    height: auto !important;
  }
}
/* Smaller buttons */
.ui-button .ui-button-text {
  padding: 0.2em 0.8em;
  font-size: 77%;
}
input.ui-button {
  padding: 0.3em 0.9em;
}
span#kernel_logo_widget {
  margin: 0 10px;
}
span#login_widget {
  float: right;
}
[dir="rtl"] span#login_widget {
  float: left;
}
span#login_widget > .button,
#logout {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button:focus,
#logout:focus,
span#login_widget > .button.focus,
#logout.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
span#login_widget > .button:hover,
#logout:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active:hover,
#logout:active:hover,
span#login_widget > .button.active:hover,
#logout.active:hover,
.open > .dropdown-togglespan#login_widget > .button:hover,
.open > .dropdown-toggle#logout:hover,
span#login_widget > .button:active:focus,
#logout:active:focus,
span#login_widget > .button.active:focus,
#logout.active:focus,
.open > .dropdown-togglespan#login_widget > .button:focus,
.open > .dropdown-toggle#logout:focus,
span#login_widget > .button:active.focus,
#logout:active.focus,
span#login_widget > .button.active.focus,
#logout.active.focus,
.open > .dropdown-togglespan#login_widget > .button.focus,
.open > .dropdown-toggle#logout.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  background-image: none;
}
span#login_widget > .button.disabled:hover,
#logout.disabled:hover,
span#login_widget > .button[disabled]:hover,
#logout[disabled]:hover,
fieldset[disabled] span#login_widget > .button:hover,
fieldset[disabled] #logout:hover,
span#login_widget > .button.disabled:focus,
#logout.disabled:focus,
span#login_widget > .button[disabled]:focus,
#logout[disabled]:focus,
fieldset[disabled] span#login_widget > .button:focus,
fieldset[disabled] #logout:focus,
span#login_widget > .button.disabled.focus,
#logout.disabled.focus,
span#login_widget > .button[disabled].focus,
#logout[disabled].focus,
fieldset[disabled] span#login_widget > .button.focus,
fieldset[disabled] #logout.focus {
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button .badge,
#logout .badge {
  color: #fff;
  background-color: #333;
}
.nav-header {
  text-transform: none;
}
#header > span {
  margin-top: 10px;
}
.modal_stretch .modal-dialog {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  min-height: 80vh;
}
.modal_stretch .modal-dialog .modal-body {
  max-height: calc(100vh - 200px);
  overflow: auto;
  flex: 1;
}
.modal-header {
  cursor: move;
}
@media (min-width: 768px) {
  .modal .modal-dialog {
    width: 700px;
  }
}
@media (min-width: 768px) {
  select.form-control {
    margin-left: 12px;
    margin-right: 12px;
  }
}
/*!
*
* IPython auth
*
*/
.center-nav {
  display: inline-block;
  margin-bottom: -4px;
}
[dir="rtl"] .center-nav form.pull-left {
  float: right !important;
  float: right;
}
[dir="rtl"] .center-nav .navbar-text {
  float: right;
}
[dir="rtl"] .navbar-inner {
  text-align: right;
}
[dir="rtl"] div.text-left {
  text-align: right;
}
/*!
*
* IPython tree view
*
*/
/* We need an invisible input field on top of the sentense*/
/* "Drag file onto the list ..." */
.alternate_upload {
  background-color: none;
  display: inline;
}
.alternate_upload.form {
  padding: 0;
  margin: 0;
}
.alternate_upload input.fileinput {
  position: absolute;
  display: block;
  width: 100%;
  height: 100%;
  overflow: hidden;
  cursor: pointer;
  opacity: 0;
  z-index: 2;
}
.alternate_upload .btn-xs > input.fileinput {
  margin: -1px -5px;
}
.alternate_upload .btn-upload {
  position: relative;
  height: 22px;
}
::-webkit-file-upload-button {
  cursor: pointer;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
ul#tabs {
  margin-bottom: 4px;
}
ul#tabs a {
  padding-top: 6px;
  padding-bottom: 4px;
}
[dir="rtl"] ul#tabs.nav-tabs > li {
  float: right;
}
[dir="rtl"] ul#tabs.nav.nav-tabs {
  padding-right: 0;
}
ul.breadcrumb a:focus,
ul.breadcrumb a:hover {
  text-decoration: none;
}
ul.breadcrumb i.icon-home {
  font-size: 16px;
  margin-right: 4px;
}
ul.breadcrumb span {
  color: #5e5e5e;
}
.list_toolbar {
  padding: 4px 0 4px 0;
  vertical-align: middle;
}
.list_toolbar .tree-buttons {
  padding-top: 1px;
}
[dir="rtl"] .list_toolbar .tree-buttons .pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .list_toolbar .col-sm-4,
[dir="rtl"] .list_toolbar .col-sm-8 {
  float: right;
}
.dynamic-buttons {
  padding-top: 3px;
  display: inline-block;
}
.list_toolbar [class*="span"] {
  min-height: 24px;
}
.list_header {
  font-weight: bold;
  background-color: #EEE;
}
.list_placeholder {
  font-weight: bold;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
}
.list_container {
  margin-top: 4px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 2px;
}
.list_container > div {
  border-bottom: 1px solid #ddd;
}
.list_container > div:hover .list-item {
  background-color: red;
}
.list_container > div:last-child {
  border: none;
}
.list_item:hover .list_item {
  background-color: #ddd;
}
.list_item a {
  text-decoration: none;
}
.list_item:hover {
  background-color: #fafafa;
}
.list_header > div,
.list_item > div {
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
.list_header > div input,
.list_item > div input {
  margin-right: 7px;
  margin-left: 14px;
  vertical-align: text-bottom;
  line-height: 22px;
  position: relative;
  top: -1px;
}
.list_header > div .item_link,
.list_item > div .item_link {
  margin-left: -1px;
  vertical-align: baseline;
  line-height: 22px;
}
[dir="rtl"] .list_item > div input {
  margin-right: 0;
}
.new-file input[type=checkbox] {
  visibility: hidden;
}
.item_name {
  line-height: 22px;
  height: 24px;
}
.item_icon {
  font-size: 14px;
  color: #5e5e5e;
  margin-right: 7px;
  margin-left: 7px;
  line-height: 22px;
  vertical-align: baseline;
}
.item_modified {
  margin-right: 7px;
  margin-left: 7px;
}
[dir="rtl"] .item_modified.pull-right {
  float: left !important;
  float: left;
}
.item_buttons {
  line-height: 1em;
  margin-left: -5px;
}
.item_buttons .btn,
.item_buttons .btn-group,
.item_buttons .input-group {
  float: left;
}
.item_buttons > .btn,
.item_buttons > .btn-group,
.item_buttons > .input-group {
  margin-left: 5px;
}
.item_buttons .btn {
  min-width: 13ex;
}
.item_buttons .running-indicator {
  padding-top: 4px;
  color: #5cb85c;
}
.item_buttons .kernel-name {
  padding-top: 4px;
  color: #5bc0de;
  margin-right: 7px;
  float: left;
}
[dir="rtl"] .item_buttons.pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .item_buttons .kernel-name {
  margin-left: 7px;
  float: right;
}
.toolbar_info {
  height: 24px;
  line-height: 24px;
}
.list_item input:not([type=checkbox]) {
  padding-top: 3px;
  padding-bottom: 3px;
  height: 22px;
  line-height: 14px;
  margin: 0px;
}
.highlight_text {
  color: blue;
}
#project_name {
  display: inline-block;
  padding-left: 7px;
  margin-left: -2px;
}
#project_name > .breadcrumb {
  padding: 0px;
  margin-bottom: 0px;
  background-color: transparent;
  font-weight: bold;
}
.sort_button {
  display: inline-block;
  padding-left: 7px;
}
[dir="rtl"] .sort_button.pull-right {
  float: left !important;
  float: left;
}
#tree-selector {
  padding-right: 0px;
}
#button-select-all {
  min-width: 50px;
}
[dir="rtl"] #button-select-all.btn {
  float: right ;
}
#select-all {
  margin-left: 7px;
  margin-right: 2px;
  margin-top: 2px;
  height: 16px;
}
[dir="rtl"] #select-all.pull-left {
  float: right !important;
  float: right;
}
.menu_icon {
  margin-right: 2px;
}
.tab-content .row {
  margin-left: 0px;
  margin-right: 0px;
}
.folder_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f114";
}
.folder_icon:before.fa-pull-left {
  margin-right: .3em;
}
.folder_icon:before.fa-pull-right {
  margin-left: .3em;
}
.folder_icon:before.pull-left {
  margin-right: .3em;
}
.folder_icon:before.pull-right {
  margin-left: .3em;
}
.notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
}
.notebook_icon:before.fa-pull-left {
  margin-right: .3em;
}
.notebook_icon:before.fa-pull-right {
  margin-left: .3em;
}
.notebook_icon:before.pull-left {
  margin-right: .3em;
}
.notebook_icon:before.pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
  color: #5cb85c;
}
.running_notebook_icon:before.fa-pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.fa-pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before.pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.pull-right {
  margin-left: .3em;
}
.file_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f016";
  position: relative;
  top: -2px;
}
.file_icon:before.fa-pull-left {
  margin-right: .3em;
}
.file_icon:before.fa-pull-right {
  margin-left: .3em;
}
.file_icon:before.pull-left {
  margin-right: .3em;
}
.file_icon:before.pull-right {
  margin-left: .3em;
}
#notebook_toolbar .pull-right {
  padding-top: 0px;
  margin-right: -1px;
}
ul#new-menu {
  left: auto;
  right: 0;
}
#new-menu .dropdown-header {
  font-size: 10px;
  border-bottom: 1px solid #e5e5e5;
  padding: 0 0 3px;
  margin: -3px 20px 0;
}
.kernel-menu-icon {
  padding-right: 12px;
  width: 24px;
  content: "\f096";
}
.kernel-menu-icon:before {
  content: "\f096";
}
.kernel-menu-icon-current:before {
  content: "\f00c";
}
#tab_content {
  padding-top: 20px;
}
#running .panel-group .panel {
  margin-top: 3px;
  margin-bottom: 1em;
}
#running .panel-group .panel .panel-heading {
  background-color: #EEE;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
#running .panel-group .panel .panel-heading a:focus,
#running .panel-group .panel .panel-heading a:hover {
  text-decoration: none;
}
#running .panel-group .panel .panel-body {
  padding: 0px;
}
#running .panel-group .panel .panel-body .list_container {
  margin-top: 0px;
  margin-bottom: 0px;
  border: 0px;
  border-radius: 0px;
}
#running .panel-group .panel .panel-body .list_container .list_item {
  border-bottom: 1px solid #ddd;
}
#running .panel-group .panel .panel-body .list_container .list_item:last-child {
  border-bottom: 0px;
}
.delete-button {
  display: none;
}
.duplicate-button {
  display: none;
}
.rename-button {
  display: none;
}
.move-button {
  display: none;
}
.download-button {
  display: none;
}
.shutdown-button {
  display: none;
}
.dynamic-instructions {
  display: inline-block;
  padding-top: 4px;
}
/*!
*
* IPython text editor webapp
*
*/
.selected-keymap i.fa {
  padding: 0px 5px;
}
.selected-keymap i.fa:before {
  content: "\f00c";
}
#mode-menu {
  overflow: auto;
  max-height: 20em;
}
.edit_app #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.edit_app #menubar .navbar {
  /* Use a negative 1 bottom margin, so the border overlaps the border of the
    header */
  margin-bottom: -1px;
}
.dirty-indicator {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator.pull-left {
  margin-right: .3em;
}
.dirty-indicator.pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-dirty.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty.pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-clean.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f00c";
}
.dirty-indicator-clean:before.fa-pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.fa-pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.pull-right {
  margin-left: .3em;
}
#filename {
  font-size: 16pt;
  display: table;
  padding: 0px 5px;
}
#current-mode {
  padding-left: 5px;
  padding-right: 5px;
}
#texteditor-backdrop {
  padding-top: 20px;
  padding-bottom: 20px;
}
@media not print {
  #texteditor-backdrop {
    background-color: #EEE;
  }
}
@media print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container {
    padding: 0px;
    background-color: #fff;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
.CodeMirror-dialog {
  background-color: #fff;
}
/*!
*
* IPython notebook
*
*/
/* CSS font colors for translated ANSI escape sequences */
/* The color values are a mix of
   http://www.xcolors.net/dl/baskerville-ivorylight and
   http://www.xcolors.net/dl/euphrasia */
.ansi-black-fg {
  color: #3E424D;
}
.ansi-black-bg {
  background-color: #3E424D;
}
.ansi-black-intense-fg {
  color: #282C36;
}
.ansi-black-intense-bg {
  background-color: #282C36;
}
.ansi-red-fg {
  color: #E75C58;
}
.ansi-red-bg {
  background-color: #E75C58;
}
.ansi-red-intense-fg {
  color: #B22B31;
}
.ansi-red-intense-bg {
  background-color: #B22B31;
}
.ansi-green-fg {
  color: #00A250;
}
.ansi-green-bg {
  background-color: #00A250;
}
.ansi-green-intense-fg {
  color: #007427;
}
.ansi-green-intense-bg {
  background-color: #007427;
}
.ansi-yellow-fg {
  color: #DDB62B;
}
.ansi-yellow-bg {
  background-color: #DDB62B;
}
.ansi-yellow-intense-fg {
  color: #B27D12;
}
.ansi-yellow-intense-bg {
  background-color: #B27D12;
}
.ansi-blue-fg {
  color: #208FFB;
}
.ansi-blue-bg {
  background-color: #208FFB;
}
.ansi-blue-intense-fg {
  color: #0065CA;
}
.ansi-blue-intense-bg {
  background-color: #0065CA;
}
.ansi-magenta-fg {
  color: #D160C4;
}
.ansi-magenta-bg {
  background-color: #D160C4;
}
.ansi-magenta-intense-fg {
  color: #A03196;
}
.ansi-magenta-intense-bg {
  background-color: #A03196;
}
.ansi-cyan-fg {
  color: #60C6C8;
}
.ansi-cyan-bg {
  background-color: #60C6C8;
}
.ansi-cyan-intense-fg {
  color: #258F8F;
}
.ansi-cyan-intense-bg {
  background-color: #258F8F;
}
.ansi-white-fg {
  color: #C5C1B4;
}
.ansi-white-bg {
  background-color: #C5C1B4;
}
.ansi-white-intense-fg {
  color: #A1A6B2;
}
.ansi-white-intense-bg {
  background-color: #A1A6B2;
}
.ansi-default-inverse-fg {
  color: #FFFFFF;
}
.ansi-default-inverse-bg {
  background-color: #000000;
}
.ansi-bold {
  font-weight: bold;
}
.ansi-underline {
  text-decoration: underline;
}
/* The following styles are deprecated an will be removed in a future version */
.ansibold {
  font-weight: bold;
}
.ansi-inverse {
  outline: 0.5px dotted;
}
/* use dark versions for foreground, to improve visibility */
.ansiblack {
  color: black;
}
.ansired {
  color: darkred;
}
.ansigreen {
  color: darkgreen;
}
.ansiyellow {
  color: #c4a000;
}
.ansiblue {
  color: darkblue;
}
.ansipurple {
  color: darkviolet;
}
.ansicyan {
  color: steelblue;
}
.ansigray {
  color: gray;
}
/* and light for background, for the same reason */
.ansibgblack {
  background-color: black;
}
.ansibgred {
  background-color: red;
}
.ansibggreen {
  background-color: green;
}
.ansibgyellow {
  background-color: yellow;
}
.ansibgblue {
  background-color: blue;
}
.ansibgpurple {
  background-color: magenta;
}
.ansibgcyan {
  background-color: cyan;
}
.ansibggray {
  background-color: gray;
}
div.cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-radius: 2px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: transparent;
  width: 100%;
  padding: 5px;
  /* This acts as a spacer between cells, that is outside the border */
  margin: 0px;
  outline: none;
  position: relative;
  overflow: visible;
}
div.cell:before {
  position: absolute;
  display: block;
  top: -1px;
  left: -1px;
  width: 5px;
  height: calc(100% +  2px);
  content: '';
  background: transparent;
}
div.cell.jupyter-soft-selected {
  border-left-color: #E3F2FD;
  border-left-width: 1px;
  padding-left: 5px;
  border-right-color: #E3F2FD;
  border-right-width: 1px;
  background: #E3F2FD;
}
@media print {
  div.cell.jupyter-soft-selected {
    border-color: transparent;
  }
}
div.cell.selected,
div.cell.selected.jupyter-soft-selected {
  border-color: #ababab;
}
div.cell.selected:before,
div.cell.selected.jupyter-soft-selected:before {
  position: absolute;
  display: block;
  top: -1px;
  left: -1px;
  width: 5px;
  height: calc(100% +  2px);
  content: '';
  background: #42A5F5;
}
@media print {
  div.cell.selected,
  div.cell.selected.jupyter-soft-selected {
    border-color: transparent;
  }
}
.edit_mode div.cell.selected {
  border-color: #66BB6A;
}
.edit_mode div.cell.selected:before {
  position: absolute;
  display: block;
  top: -1px;
  left: -1px;
  width: 5px;
  height: calc(100% +  2px);
  content: '';
  background: #66BB6A;
}
@media print {
  .edit_mode div.cell.selected {
    border-color: transparent;
  }
}
.prompt {
  /* This needs to be wide enough for 3 digit prompt numbers: In[100]: */
  min-width: 14ex;
  /* This padding is tuned to match the padding on the CodeMirror editor. */
  padding: 0.4em;
  margin: 0px;
  font-family: monospace;
  text-align: right;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
  /* Don't highlight prompt number selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  /* Use default cursor */
  cursor: default;
}
@media (max-width: 540px) {
  .prompt {
    text-align: left;
  }
}
div.inner_cell {
  min-width: 0;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_area {
  border: 1px solid #cfcfcf;
  border-radius: 2px;
  background: #f7f7f7;
  line-height: 1.21429em;
}
/* This is needed so that empty prompt areas can collapse to zero height when there
   is no content in the output_subarea and the prompt. The main purpose of this is
   to make sure that empty JavaScript output_subareas have no height. */
div.prompt:empty {
  padding-top: 0;
  padding-bottom: 0;
}
div.unrecognized_cell {
  padding: 5px 5px 5px 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.unrecognized_cell .inner_cell {
  border-radius: 2px;
  padding: 5px;
  font-weight: bold;
  color: red;
  border: 1px solid #cfcfcf;
  background: #eaeaea;
}
div.unrecognized_cell .inner_cell a {
  color: inherit;
  text-decoration: none;
}
div.unrecognized_cell .inner_cell a:hover {
  color: inherit;
  text-decoration: none;
}
@media (max-width: 540px) {
  div.unrecognized_cell > div.prompt {
    display: none;
  }
}
div.code_cell {
  /* avoid page breaking on code cells when printing */
}
@media print {
  div.code_cell {
    page-break-inside: avoid;
  }
}
/* any special styling for code cells that are currently running goes here */
div.input {
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.input {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_prompt {
  color: #303F9F;
  border-top: 1px solid transparent;
}
div.input_area > div.highlight {
  margin: 0.4em;
  border: none;
  padding: 0px;
  background-color: transparent;
}
div.input_area > div.highlight > pre {
  margin: 0px;
  border: none;
  padding: 0px;
  background-color: transparent;
}
/* The following gets added to the <head> if it is detected that the user has a
 * monospace font with inconsistent normal/bold/italic height.  See
 * notebookmain.js.  Such fonts will have keywords vertically offset with
 * respect to the rest of the text.  The user should select a better font.
 * See: https://github.com/ipython/ipython/issues/1503
 *
 * .CodeMirror span {
 *      vertical-align: bottom;
 * }
 */
.CodeMirror {
  line-height: 1.21429em;
  /* Changed from 1em to our global default */
  font-size: 14px;
  height: auto;
  /* Changed to auto to autogrow */
  background: none;
  /* Changed from white to allow our bg to show through */
}
.CodeMirror-scroll {
  /*  The CodeMirror docs are a bit fuzzy on if overflow-y should be hidden or visible.*/
  /*  We have found that if it is visible, vertical scrollbars appear with font size changes.*/
  overflow-y: hidden;
  overflow-x: auto;
}
.CodeMirror-lines {
  /* In CM2, this used to be 0.4em, but in CM3 it went to 4px. We need the em value because */
  /* we have set a different line-height and want this to scale with that. */
  /* Note that this should set vertical padding only, since CodeMirror assumes
       that horizontal padding will be set on CodeMirror pre */
  padding: 0.4em 0;
}
.CodeMirror-linenumber {
  padding: 0 8px 0 4px;
}
.CodeMirror-gutters {
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.CodeMirror pre {
  /* In CM3 this went to 4px from 0 in CM2. This sets horizontal padding only,
    use .CodeMirror-lines for vertical */
  padding: 0 0.4em;
  border: 0;
  border-radius: 0;
}
.CodeMirror-cursor {
  border-left: 1.4px solid black;
}
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .CodeMirror-cursor {
    border-left: 2px solid black;
  }
}
@media screen and (min-width: 4320px) {
  .CodeMirror-cursor {
    border-left: 4px solid black;
  }
}
/*

Original style from softwaremaniacs.org (c) Ivan Sagalaev <Maniac@SoftwareManiacs.Org>
Adapted from GitHub theme

*/
.highlight-base {
  color: #000;
}
.highlight-variable {
  color: #000;
}
.highlight-variable-2 {
  color: #1a1a1a;
}
.highlight-variable-3 {
  color: #333333;
}
.highlight-string {
  color: #BA2121;
}
.highlight-comment {
  color: #408080;
  font-style: italic;
}
.highlight-number {
  color: #080;
}
.highlight-atom {
  color: #88F;
}
.highlight-keyword {
  color: #008000;
  font-weight: bold;
}
.highlight-builtin {
  color: #008000;
}
.highlight-error {
  color: #f00;
}
.highlight-operator {
  color: #AA22FF;
  font-weight: bold;
}
.highlight-meta {
  color: #AA22FF;
}
/* previously not defined, copying from default codemirror */
.highlight-def {
  color: #00f;
}
.highlight-string-2 {
  color: #f50;
}
.highlight-qualifier {
  color: #555;
}
.highlight-bracket {
  color: #997;
}
.highlight-tag {
  color: #170;
}
.highlight-attribute {
  color: #00c;
}
.highlight-header {
  color: blue;
}
.highlight-quote {
  color: #090;
}
.highlight-link {
  color: #00c;
}
/* apply the same style to codemirror */
.cm-s-ipython span.cm-keyword {
  color: #008000;
  font-weight: bold;
}
.cm-s-ipython span.cm-atom {
  color: #88F;
}
.cm-s-ipython span.cm-number {
  color: #080;
}
.cm-s-ipython span.cm-def {
  color: #00f;
}
.cm-s-ipython span.cm-variable {
  color: #000;
}
.cm-s-ipython span.cm-operator {
  color: #AA22FF;
  font-weight: bold;
}
.cm-s-ipython span.cm-variable-2 {
  color: #1a1a1a;
}
.cm-s-ipython span.cm-variable-3 {
  color: #333333;
}
.cm-s-ipython span.cm-comment {
  color: #408080;
  font-style: italic;
}
.cm-s-ipython span.cm-string {
  color: #BA2121;
}
.cm-s-ipython span.cm-string-2 {
  color: #f50;
}
.cm-s-ipython span.cm-meta {
  color: #AA22FF;
}
.cm-s-ipython span.cm-qualifier {
  color: #555;
}
.cm-s-ipython span.cm-builtin {
  color: #008000;
}
.cm-s-ipython span.cm-bracket {
  color: #997;
}
.cm-s-ipython span.cm-tag {
  color: #170;
}
.cm-s-ipython span.cm-attribute {
  color: #00c;
}
.cm-s-ipython span.cm-header {
  color: blue;
}
.cm-s-ipython span.cm-quote {
  color: #090;
}
.cm-s-ipython span.cm-link {
  color: #00c;
}
.cm-s-ipython span.cm-error {
  color: #f00;
}
.cm-s-ipython span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}
div.output_wrapper {
  /* this position must be relative to enable descendents to be absolute within it */
  position: relative;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  z-index: 1;
}
/* class for the output area when it should be height-limited */
div.output_scroll {
  /* ideally, this would be max-height, but FF barfs all over that */
  height: 24em;
  /* FF needs this *and the wrapper* to specify full width, or it will shrinkwrap */
  width: 100%;
  overflow: auto;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  display: block;
}
/* output div while it is collapsed */
div.output_collapsed {
  margin: 0px;
  padding: 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
div.out_prompt_overlay {
  height: 100%;
  padding: 0px 0.4em;
  position: absolute;
  border-radius: 2px;
}
div.out_prompt_overlay:hover {
  /* use inner shadow to get border that is computed the same on WebKit/FF */
  -webkit-box-shadow: inset 0 0 1px #000;
  box-shadow: inset 0 0 1px #000;
  background: rgba(240, 240, 240, 0.5);
}
div.output_prompt {
  color: #D84315;
}
/* This class is the outer container of all output sections. */
div.output_area {
  padding: 0px;
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.output_area .MathJax_Display {
  text-align: left !important;
}
div.output_area .rendered_html table {
  margin-left: 0;
  margin-right: 0;
}
div.output_area .rendered_html img {
  margin-left: 0;
  margin-right: 0;
}
div.output_area img,
div.output_area svg {
  max-width: 100%;
  height: auto;
}
div.output_area img.unconfined,
div.output_area svg.unconfined {
  max-width: none;
}
div.output_area .mglyph > img {
  max-width: none;
}
/* This is needed to protect the pre formating from global settings such
   as that of bootstrap */
.output {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.output_area {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
div.output_area pre {
  margin: 0;
  padding: 1px 0 1px 0;
  border: 0;
  vertical-align: baseline;
  color: black;
  background-color: transparent;
  border-radius: 0;
}
/* This class is for the output subarea inside the output_area and after
   the prompt div. */
div.output_subarea {
  overflow-x: auto;
  padding: 0.4em;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
  max-width: calc(100% - 14ex);
}
div.output_scroll div.output_subarea {
  overflow-x: visible;
}
/* The rest of the output_* classes are for special styling of the different
   output types */
/* all text output has this class: */
div.output_text {
  text-align: left;
  color: #000;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
}
/* stdout/stderr are 'text' as well as 'stream', but execute_result/error are *not* streams */
div.output_stderr {
  background: #fdd;
  /* very light red background for stderr */
}
div.output_latex {
  text-align: left;
}
/* Empty output_javascript divs should have no height */
div.output_javascript:empty {
  padding: 0;
}
.js-error {
  color: darkred;
}
/* raw_input styles */
div.raw_input_container {
  line-height: 1.21429em;
  padding-top: 5px;
}
pre.raw_input_prompt {
  /* nothing needed here. */
}
input.raw_input {
  font-family: monospace;
  font-size: inherit;
  color: inherit;
  width: auto;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
}
input.raw_input:focus {
  box-shadow: none;
}
p.p-space {
  margin-bottom: 10px;
}
div.output_unrecognized {
  padding: 5px;
  font-weight: bold;
  color: red;
}
div.output_unrecognized a {
  color: inherit;
  text-decoration: none;
}
div.output_unrecognized a:hover {
  color: inherit;
  text-decoration: none;
}
.rendered_html {
  color: #000;
  /* any extras will just be numbers: */
}
.rendered_html em {
  font-style: italic;
}
.rendered_html strong {
  font-weight: bold;
}
.rendered_html u {
  text-decoration: underline;
}
.rendered_html :link {
  text-decoration: underline;
}
.rendered_html :visited {
  text-decoration: underline;
}
.rendered_html h1 {
  font-size: 185.7%;
  margin: 1.08em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h2 {
  font-size: 157.1%;
  margin: 1.27em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h3 {
  font-size: 128.6%;
  margin: 1.55em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h4 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h5 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h6 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h1:first-child {
  margin-top: 0.538em;
}
.rendered_html h2:first-child {
  margin-top: 0.636em;
}
.rendered_html h3:first-child {
  margin-top: 0.777em;
}
.rendered_html h4:first-child {
  margin-top: 1em;
}
.rendered_html h5:first-child {
  margin-top: 1em;
}
.rendered_html h6:first-child {
  margin-top: 1em;
}
.rendered_html ul:not(.list-inline),
.rendered_html ol:not(.list-inline) {
  padding-left: 2em;
}
.rendered_html ul {
  list-style: disc;
}
.rendered_html ul ul {
  list-style: square;
  margin-top: 0;
}
.rendered_html ul ul ul {
  list-style: circle;
}
.rendered_html ol {
  list-style: decimal;
}
.rendered_html ol ol {
  list-style: upper-alpha;
  margin-top: 0;
}
.rendered_html ol ol ol {
  list-style: lower-alpha;
}
.rendered_html ol ol ol ol {
  list-style: lower-roman;
}
.rendered_html ol ol ol ol ol {
  list-style: decimal;
}
.rendered_html * + ul {
  margin-top: 1em;
}
.rendered_html * + ol {
  margin-top: 1em;
}
.rendered_html hr {
  color: black;
  background-color: black;
}
.rendered_html pre {
  margin: 1em 2em;
  padding: 0px;
  background-color: #fff;
}
.rendered_html code {
  background-color: #eff0f1;
}
.rendered_html p code {
  padding: 1px 5px;
}
.rendered_html pre code {
  background-color: #fff;
}
.rendered_html pre,
.rendered_html code {
  border: 0;
  color: #000;
  font-size: 100%;
}
.rendered_html blockquote {
  margin: 1em 2em;
}
.rendered_html table {
  margin-left: auto;
  margin-right: auto;
  border: none;
  border-collapse: collapse;
  border-spacing: 0;
  color: black;
  font-size: 12px;
  table-layout: fixed;
}
.rendered_html thead {
  border-bottom: 1px solid black;
  vertical-align: bottom;
}
.rendered_html tr,
.rendered_html th,
.rendered_html td {
  text-align: right;
  vertical-align: middle;
  padding: 0.5em 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}
.rendered_html th {
  font-weight: bold;
}
.rendered_html tbody tr:nth-child(odd) {
  background: #f5f5f5;
}
.rendered_html tbody tr:hover {
  background: rgba(66, 165, 245, 0.2);
}
.rendered_html * + table {
  margin-top: 1em;
}
.rendered_html p {
  text-align: left;
}
.rendered_html * + p {
  margin-top: 1em;
}
.rendered_html img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.rendered_html * + img {
  margin-top: 1em;
}
.rendered_html img,
.rendered_html svg {
  max-width: 100%;
  height: auto;
}
.rendered_html img.unconfined,
.rendered_html svg.unconfined {
  max-width: none;
}
.rendered_html .alert {
  margin-bottom: initial;
}
.rendered_html * + .alert {
  margin-top: 1em;
}
[dir="rtl"] .rendered_html p {
  text-align: right;
}
div.text_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.text_cell > div.prompt {
    display: none;
  }
}
div.text_cell_render {
  /*font-family: "Helvetica Neue", Arial, Helvetica, Geneva, sans-serif;*/
  outline: none;
  resize: none;
  width: inherit;
  border-style: none;
  padding: 0.5em 0.5em 0.5em 0.4em;
  color: #000;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
a.anchor-link:link {
  text-decoration: none;
  padding: 0px 20px;
  visibility: hidden;
}
h1:hover .anchor-link,
h2:hover .anchor-link,
h3:hover .anchor-link,
h4:hover .anchor-link,
h5:hover .anchor-link,
h6:hover .anchor-link {
  visibility: visible;
}
.text_cell.rendered .input_area {
  display: none;
}
.text_cell.rendered .rendered_html {
  overflow-x: auto;
  overflow-y: hidden;
}
.text_cell.rendered .rendered_html tr,
.text_cell.rendered .rendered_html th,
.text_cell.rendered .rendered_html td {
  max-width: none;
}
.text_cell.unrendered .text_cell_render {
  display: none;
}
.text_cell .dropzone .input_area {
  border: 2px dashed #bababa;
  margin: -1px;
}
.cm-header-1,
.cm-header-2,
.cm-header-3,
.cm-header-4,
.cm-header-5,
.cm-header-6 {
  font-weight: bold;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.cm-header-1 {
  font-size: 185.7%;
}
.cm-header-2 {
  font-size: 157.1%;
}
.cm-header-3 {
  font-size: 128.6%;
}
.cm-header-4 {
  font-size: 110%;
}
.cm-header-5 {
  font-size: 100%;
  font-style: italic;
}
.cm-header-6 {
  font-size: 100%;
  font-style: italic;
}
/*!
*
* IPython notebook webapp
*
*/
@media (max-width: 767px) {
  .notebook_app {
    padding-left: 0px;
    padding-right: 0px;
  }
}
#ipython-main-app {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook_panel {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook {
  font-size: 14px;
  line-height: 20px;
  overflow-y: hidden;
  overflow-x: auto;
  width: 100%;
  /* This spaces the page away from the edge of the notebook area */
  padding-top: 20px;
  margin: 0px;
  outline: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  min-height: 100%;
}
@media not print {
  #notebook-container {
    padding: 15px;
    background-color: #fff;
    min-height: 0;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
@media print {
  #notebook-container {
    width: 100%;
  }
}
div.ui-widget-content {
  border: 1px solid #ababab;
  outline: none;
}
pre.dialog {
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0.4em;
  padding-left: 2em;
}
p.dialog {
  padding: 0.2em;
}
/* Word-wrap output correctly.  This is the CSS3 spelling, though Firefox seems
   to not honor it correctly.  Webkit browsers (Chrome, rekonq, Safari) do.
 */
pre,
code,
kbd,
samp {
  white-space: pre-wrap;
}
#fonttest {
  font-family: monospace;
}
p {
  margin-bottom: 0;
}
.end_space {
  min-height: 100px;
  transition: height .2s ease;
}
.notebook_app > #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
@media not print {
  .notebook_app {
    background-color: #EEE;
  }
}
kbd {
  border-style: solid;
  border-width: 1px;
  box-shadow: none;
  margin: 2px;
  padding-left: 2px;
  padding-right: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
.jupyter-keybindings {
  padding: 1px;
  line-height: 24px;
  border-bottom: 1px solid gray;
}
.jupyter-keybindings input {
  margin: 0;
  padding: 0;
  border: none;
}
.jupyter-keybindings i {
  padding: 6px;
}
.well code {
  background-color: #ffffff;
  border-color: #ababab;
  border-width: 1px;
  border-style: solid;
  padding: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
/* CSS for the cell toolbar */
.celltoolbar {
  border: thin solid #CFCFCF;
  border-bottom: none;
  background: #EEE;
  border-radius: 2px 2px 0px 0px;
  width: 100%;
  height: 29px;
  padding-right: 4px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
  display: -webkit-flex;
}
@media print {
  .celltoolbar {
    display: none;
  }
}
.ctb_hideshow {
  display: none;
  vertical-align: bottom;
}
/* ctb_show is added to the ctb_hideshow div to show the cell toolbar.
   Cell toolbars are only shown when the ctb_global_show class is also set.
*/
.ctb_global_show .ctb_show.ctb_hideshow {
  display: block;
}
.ctb_global_show .ctb_show + .input_area,
.ctb_global_show .ctb_show + div.text_cell_input,
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border-top-right-radius: 0px;
  border-top-left-radius: 0px;
}
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border: 1px solid #cfcfcf;
}
.celltoolbar {
  font-size: 87%;
  padding-top: 3px;
}
.celltoolbar select {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  width: inherit;
  font-size: inherit;
  height: 22px;
  padding: 0px;
  display: inline-block;
}
.celltoolbar select:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.celltoolbar select::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.celltoolbar select:-ms-input-placeholder {
  color: #999;
}
.celltoolbar select::-webkit-input-placeholder {
  color: #999;
}
.celltoolbar select::-ms-expand {
  border: 0;
  background-color: transparent;
}
.celltoolbar select[disabled],
.celltoolbar select[readonly],
fieldset[disabled] .celltoolbar select {
  background-color: #eeeeee;
  opacity: 1;
}
.celltoolbar select[disabled],
fieldset[disabled] .celltoolbar select {
  cursor: not-allowed;
}
textarea.celltoolbar select {
  height: auto;
}
select.celltoolbar select {
  height: 30px;
  line-height: 30px;
}
textarea.celltoolbar select,
select[multiple].celltoolbar select {
  height: auto;
}
.celltoolbar label {
  margin-left: 5px;
  margin-right: 5px;
}
.tags_button_container {
  width: 100%;
  display: flex;
}
.tag-container {
  display: flex;
  flex-direction: row;
  flex-grow: 1;
  overflow: hidden;
  position: relative;
}
.tag-container > * {
  margin: 0 4px;
}
.remove-tag-btn {
  margin-left: 4px;
}
.tags-input {
  display: flex;
}
.cell-tag:last-child:after {
  content: "";
  position: absolute;
  right: 0;
  width: 40px;
  height: 100%;
  /* Fade to background color of cell toolbar */
  background: linear-gradient(to right, rgba(0, 0, 0, 0), #EEE);
}
.tags-input > * {
  margin-left: 4px;
}
.cell-tag,
.tags-input input,
.tags-input button {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  box-shadow: none;
  width: inherit;
  font-size: inherit;
  height: 22px;
  line-height: 22px;
  padding: 0px 4px;
  display: inline-block;
}
.cell-tag:focus,
.tags-input input:focus,
.tags-input button:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.cell-tag::-moz-placeholder,
.tags-input input::-moz-placeholder,
.tags-input button::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.cell-tag:-ms-input-placeholder,
.tags-input input:-ms-input-placeholder,
.tags-input button:-ms-input-placeholder {
  color: #999;
}
.cell-tag::-webkit-input-placeholder,
.tags-input input::-webkit-input-placeholder,
.tags-input button::-webkit-input-placeholder {
  color: #999;
}
.cell-tag::-ms-expand,
.tags-input input::-ms-expand,
.tags-input button::-ms-expand {
  border: 0;
  background-color: transparent;
}
.cell-tag[disabled],
.tags-input input[disabled],
.tags-input button[disabled],
.cell-tag[readonly],
.tags-input input[readonly],
.tags-input button[readonly],
fieldset[disabled] .cell-tag,
fieldset[disabled] .tags-input input,
fieldset[disabled] .tags-input button {
  background-color: #eeeeee;
  opacity: 1;
}
.cell-tag[disabled],
.tags-input input[disabled],
.tags-input button[disabled],
fieldset[disabled] .cell-tag,
fieldset[disabled] .tags-input input,
fieldset[disabled] .tags-input button {
  cursor: not-allowed;
}
textarea.cell-tag,
textarea.tags-input input,
textarea.tags-input button {
  height: auto;
}
select.cell-tag,
select.tags-input input,
select.tags-input button {
  height: 30px;
  line-height: 30px;
}
textarea.cell-tag,
textarea.tags-input input,
textarea.tags-input button,
select[multiple].cell-tag,
select[multiple].tags-input input,
select[multiple].tags-input button {
  height: auto;
}
.cell-tag,
.tags-input button {
  padding: 0px 4px;
}
.cell-tag {
  background-color: #fff;
  white-space: nowrap;
}
.tags-input input[type=text]:focus {
  outline: none;
  box-shadow: none;
  border-color: #ccc;
}
.completions {
  position: absolute;
  z-index: 110;
  overflow: hidden;
  border: 1px solid #ababab;
  border-radius: 2px;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  line-height: 1;
}
.completions select {
  background: white;
  outline: none;
  border: none;
  padding: 0px;
  margin: 0px;
  overflow: auto;
  font-family: monospace;
  font-size: 110%;
  color: #000;
  width: auto;
}
.completions select option.context {
  color: #286090;
}
#kernel_logo_widget .current_kernel_logo {
  display: none;
  margin-top: -1px;
  margin-bottom: -1px;
  width: 32px;
  height: 32px;
}
[dir="rtl"] #kernel_logo_widget {
  float: left !important;
  float: left;
}
.modal .modal-body .move-path {
  display: flex;
  flex-direction: row;
  justify-content: space;
  align-items: center;
}
.modal .modal-body .move-path .server-root {
  padding-right: 20px;
}
.modal .modal-body .move-path .path-input {
  flex: 1;
}
#menubar {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin-top: 1px;
}
#menubar .navbar {
  border-top: 1px;
  border-radius: 0px 0px 2px 2px;
  margin-bottom: 0px;
}
#menubar .navbar-toggle {
  float: left;
  padding-top: 7px;
  padding-bottom: 7px;
  border: none;
}
#menubar .navbar-collapse {
  clear: left;
}
[dir="rtl"] #menubar .navbar-toggle {
  float: right;
}
[dir="rtl"] #menubar .navbar-collapse {
  clear: right;
}
[dir="rtl"] #menubar .navbar-nav {
  float: right;
}
[dir="rtl"] #menubar .nav {
  padding-right: 0px;
}
[dir="rtl"] #menubar .navbar-nav > li {
  float: right;
}
[dir="rtl"] #menubar .navbar-right {
  float: left !important;
}
[dir="rtl"] ul.dropdown-menu {
  text-align: right;
  left: auto;
}
[dir="rtl"] ul#new-menu.dropdown-menu {
  right: auto;
  left: 0;
}
.nav-wrapper {
  border-bottom: 1px solid #e7e7e7;
}
i.menu-icon {
  padding-top: 4px;
}
[dir="rtl"] i.menu-icon.pull-right {
  float: left !important;
  float: left;
}
ul#help_menu li a {
  overflow: hidden;
  padding-right: 2.2em;
}
ul#help_menu li a i {
  margin-right: -1.2em;
}
[dir="rtl"] ul#help_menu li a {
  padding-left: 2.2em;
}
[dir="rtl"] ul#help_menu li a i {
  margin-right: 0;
  margin-left: -1.2em;
}
[dir="rtl"] ul#help_menu li a i.pull-right {
  float: left !important;
  float: left;
}
.dropdown-submenu {
  position: relative;
}
.dropdown-submenu > .dropdown-menu {
  top: 0;
  left: 100%;
  margin-top: -6px;
  margin-left: -1px;
}
[dir="rtl"] .dropdown-submenu > .dropdown-menu {
  right: 100%;
  margin-right: -1px;
}
.dropdown-submenu:hover > .dropdown-menu {
  display: block;
}
.dropdown-submenu > a:after {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: block;
  content: "\f0da";
  float: right;
  color: #333333;
  margin-top: 2px;
  margin-right: -10px;
}
.dropdown-submenu > a:after.fa-pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.fa-pull-right {
  margin-left: .3em;
}
.dropdown-submenu > a:after.pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.pull-right {
  margin-left: .3em;
}
[dir="rtl"] .dropdown-submenu > a:after {
  float: left;
  content: "\f0d9";
  margin-right: 0;
  margin-left: -10px;
}
.dropdown-submenu:hover > a:after {
  color: #262626;
}
.dropdown-submenu.pull-left {
  float: none;
}
.dropdown-submenu.pull-left > .dropdown-menu {
  left: -100%;
  margin-left: 10px;
}
#notification_area {
  float: right !important;
  float: right;
  z-index: 10;
}
[dir="rtl"] #notification_area {
  float: left !important;
  float: left;
}
.indicator_area {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
[dir="rtl"] .indicator_area {
  float: left !important;
  float: left;
}
#kernel_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  border-left: 1px solid;
}
#kernel_indicator .kernel_indicator_name {
  padding-left: 5px;
  padding-right: 5px;
}
[dir="rtl"] #kernel_indicator {
  float: left !important;
  float: left;
  border-left: 0;
  border-right: 1px solid;
}
#modal_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
[dir="rtl"] #modal_indicator {
  float: left !important;
  float: left;
}
#readonly-indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  margin-top: 2px;
  margin-bottom: 0px;
  margin-left: 0px;
  margin-right: 0px;
  display: none;
}
.modal_indicator:before {
  width: 1.28571429em;
  text-align: center;
}
.edit_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f040";
}
.edit_mode .modal_indicator:before.fa-pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.fa-pull-right {
  margin-left: .3em;
}
.edit_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: ' ';
}
.command_mode .modal_indicator:before.fa-pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.fa-pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f10c";
}
.kernel_idle_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f111";
}
.kernel_busy_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f1e2";
}
.kernel_dead_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f127";
}
.kernel_disconnected_icon:before.fa-pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.fa-pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.pull-right {
  margin-left: .3em;
}
.notification_widget {
  color: #777;
  z-index: 10;
  background: rgba(240, 240, 240, 0.5);
  margin-right: 4px;
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget:focus,
.notification_widget.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.notification_widget:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active:hover,
.notification_widget.active:hover,
.open > .dropdown-toggle.notification_widget:hover,
.notification_widget:active:focus,
.notification_widget.active:focus,
.open > .dropdown-toggle.notification_widget:focus,
.notification_widget:active.focus,
.notification_widget.active.focus,
.open > .dropdown-toggle.notification_widget.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  background-image: none;
}
.notification_widget.disabled:hover,
.notification_widget[disabled]:hover,
fieldset[disabled] .notification_widget:hover,
.notification_widget.disabled:focus,
.notification_widget[disabled]:focus,
fieldset[disabled] .notification_widget:focus,
.notification_widget.disabled.focus,
.notification_widget[disabled].focus,
fieldset[disabled] .notification_widget.focus {
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget .badge {
  color: #fff;
  background-color: #333;
}
.notification_widget.warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning:focus,
.notification_widget.warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.notification_widget.warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active:hover,
.notification_widget.warning.active:hover,
.open > .dropdown-toggle.notification_widget.warning:hover,
.notification_widget.warning:active:focus,
.notification_widget.warning.active:focus,
.open > .dropdown-toggle.notification_widget.warning:focus,
.notification_widget.warning:active.focus,
.notification_widget.warning.active.focus,
.open > .dropdown-toggle.notification_widget.warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  background-image: none;
}
.notification_widget.warning.disabled:hover,
.notification_widget.warning[disabled]:hover,
fieldset[disabled] .notification_widget.warning:hover,
.notification_widget.warning.disabled:focus,
.notification_widget.warning[disabled]:focus,
fieldset[disabled] .notification_widget.warning:focus,
.notification_widget.warning.disabled.focus,
.notification_widget.warning[disabled].focus,
fieldset[disabled] .notification_widget.warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.notification_widget.success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success:focus,
.notification_widget.success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.notification_widget.success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active:hover,
.notification_widget.success.active:hover,
.open > .dropdown-toggle.notification_widget.success:hover,
.notification_widget.success:active:focus,
.notification_widget.success.active:focus,
.open > .dropdown-toggle.notification_widget.success:focus,
.notification_widget.success:active.focus,
.notification_widget.success.active.focus,
.open > .dropdown-toggle.notification_widget.success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  background-image: none;
}
.notification_widget.success.disabled:hover,
.notification_widget.success[disabled]:hover,
fieldset[disabled] .notification_widget.success:hover,
.notification_widget.success.disabled:focus,
.notification_widget.success[disabled]:focus,
fieldset[disabled] .notification_widget.success:focus,
.notification_widget.success.disabled.focus,
.notification_widget.success[disabled].focus,
fieldset[disabled] .notification_widget.success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.notification_widget.info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info:focus,
.notification_widget.info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.notification_widget.info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active:hover,
.notification_widget.info.active:hover,
.open > .dropdown-toggle.notification_widget.info:hover,
.notification_widget.info:active:focus,
.notification_widget.info.active:focus,
.open > .dropdown-toggle.notification_widget.info:focus,
.notification_widget.info:active.focus,
.notification_widget.info.active.focus,
.open > .dropdown-toggle.notification_widget.info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  background-image: none;
}
.notification_widget.info.disabled:hover,
.notification_widget.info[disabled]:hover,
fieldset[disabled] .notification_widget.info:hover,
.notification_widget.info.disabled:focus,
.notification_widget.info[disabled]:focus,
fieldset[disabled] .notification_widget.info:focus,
.notification_widget.info.disabled.focus,
.notification_widget.info[disabled].focus,
fieldset[disabled] .notification_widget.info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.notification_widget.danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger:focus,
.notification_widget.danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.notification_widget.danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active:hover,
.notification_widget.danger.active:hover,
.open > .dropdown-toggle.notification_widget.danger:hover,
.notification_widget.danger:active:focus,
.notification_widget.danger.active:focus,
.open > .dropdown-toggle.notification_widget.danger:focus,
.notification_widget.danger:active.focus,
.notification_widget.danger.active.focus,
.open > .dropdown-toggle.notification_widget.danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  background-image: none;
}
.notification_widget.danger.disabled:hover,
.notification_widget.danger[disabled]:hover,
fieldset[disabled] .notification_widget.danger:hover,
.notification_widget.danger.disabled:focus,
.notification_widget.danger[disabled]:focus,
fieldset[disabled] .notification_widget.danger:focus,
.notification_widget.danger.disabled.focus,
.notification_widget.danger[disabled].focus,
fieldset[disabled] .notification_widget.danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger .badge {
  color: #d9534f;
  background-color: #fff;
}
div#pager {
  background-color: #fff;
  font-size: 14px;
  line-height: 20px;
  overflow: hidden;
  display: none;
  position: fixed;
  bottom: 0px;
  width: 100%;
  max-height: 50%;
  padding-top: 8px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  /* Display over codemirror */
  z-index: 100;
  /* Hack which prevents jquery ui resizable from changing top. */
  top: auto !important;
}
div#pager pre {
  line-height: 1.21429em;
  color: #000;
  background-color: #f7f7f7;
  padding: 0.4em;
}
div#pager #pager-button-area {
  position: absolute;
  top: 8px;
  right: 20px;
}
div#pager #pager-contents {
  position: relative;
  overflow: auto;
  width: 100%;
  height: 100%;
}
div#pager #pager-contents #pager-container {
  position: relative;
  padding: 15px 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
div#pager .ui-resizable-handle {
  top: 0px;
  height: 8px;
  background: #f7f7f7;
  border-top: 1px solid #cfcfcf;
  border-bottom: 1px solid #cfcfcf;
  /* This injects handle bars (a short, wide = symbol) for 
        the resize handle. */
}
div#pager .ui-resizable-handle::after {
  content: '';
  top: 2px;
  left: 50%;
  height: 3px;
  width: 30px;
  margin-left: -15px;
  position: absolute;
  border-top: 1px solid #cfcfcf;
}
.quickhelp {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  line-height: 1.8em;
}
.shortcut_key {
  display: inline-block;
  width: 21ex;
  text-align: right;
  font-family: monospace;
}
.shortcut_descr {
  display: inline-block;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
span.save_widget {
  height: 30px;
  margin-top: 4px;
  display: flex;
  justify-content: flex-start;
  align-items: baseline;
  width: 50%;
  flex: 1;
}
span.save_widget span.filename {
  height: 100%;
  line-height: 1em;
  margin-left: 16px;
  border: none;
  font-size: 146.5%;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  border-radius: 2px;
}
span.save_widget span.filename:hover {
  background-color: #e6e6e6;
}
[dir="rtl"] span.save_widget.pull-left {
  float: right !important;
  float: right;
}
[dir="rtl"] span.save_widget span.filename {
  margin-left: 0;
  margin-right: 16px;
}
span.checkpoint_status,
span.autosave_status {
  font-size: small;
  white-space: nowrap;
  padding: 0 5px;
}
@media (max-width: 767px) {
  span.save_widget {
    font-size: small;
    padding: 0 0 0 5px;
  }
  span.checkpoint_status,
  span.autosave_status {
    display: none;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  span.checkpoint_status {
    display: none;
  }
  span.autosave_status {
    font-size: x-small;
  }
}
.toolbar {
  padding: 0px;
  margin-left: -5px;
  margin-top: 2px;
  margin-bottom: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.toolbar select,
.toolbar label {
  width: auto;
  vertical-align: middle;
  margin-right: 2px;
  margin-bottom: 0px;
  display: inline;
  font-size: 92%;
  margin-left: 0.3em;
  margin-right: 0.3em;
  padding: 0px;
  padding-top: 3px;
}
.toolbar .btn {
  padding: 2px 8px;
}
.toolbar .btn-group {
  margin-top: 0px;
  margin-left: 5px;
}
.toolbar-btn-label {
  margin-left: 6px;
}
#maintoolbar {
  margin-bottom: -3px;
  margin-top: -8px;
  border: 0px;
  min-height: 27px;
  margin-left: 0px;
  padding-top: 11px;
  padding-bottom: 3px;
}
#maintoolbar .navbar-text {
  float: none;
  vertical-align: middle;
  text-align: right;
  margin-left: 5px;
  margin-right: 0px;
  margin-top: 0px;
}
.select-xs {
  height: 24px;
}
[dir="rtl"] .btn-group > .btn,
.btn-group-vertical > .btn {
  float: right;
}
.pulse,
.dropdown-menu > li > a.pulse,
li.pulse > a.dropdown-toggle,
li.pulse.open > a.dropdown-toggle {
  background-color: #F37626;
  color: white;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
/** WARNING IF YOU ARE EDITTING THIS FILE, if this is a .css file, It has a lot
 * of chance of beeing generated from the ../less/[samename].less file, you can
 * try to get back the less file by reverting somme commit in history
 **/
/*
 * We'll try to get something pretty, so we
 * have some strange css to have the scroll bar on
 * the left with fix button on the top right of the tooltip
 */
@-moz-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
/*properties of tooltip after "expand"*/
.bigtooltip {
  overflow: auto;
  height: 200px;
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
}
/*properties of tooltip before "expand"*/
.smalltooltip {
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
  text-overflow: ellipsis;
  overflow: hidden;
  height: 80px;
}
.tooltipbuttons {
  position: absolute;
  padding-right: 15px;
  top: 0px;
  right: 0px;
}
.tooltiptext {
  /*avoid the button to overlap on some docstring*/
  padding-right: 30px;
}
.ipython_tooltip {
  max-width: 700px;
  /*fade-in animation when inserted*/
  -webkit-animation: fadeOut 400ms;
  -moz-animation: fadeOut 400ms;
  animation: fadeOut 400ms;
  -webkit-animation: fadeIn 400ms;
  -moz-animation: fadeIn 400ms;
  animation: fadeIn 400ms;
  vertical-align: middle;
  background-color: #f7f7f7;
  overflow: visible;
  border: #ababab 1px solid;
  outline: none;
  padding: 3px;
  margin: 0px;
  padding-left: 7px;
  font-family: monospace;
  min-height: 50px;
  -moz-box-shadow: 0px 6px 10px -1px #adadad;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  border-radius: 2px;
  position: absolute;
  z-index: 1000;
}
.ipython_tooltip a {
  float: right;
}
.ipython_tooltip .tooltiptext pre {
  border: 0;
  border-radius: 0;
  font-size: 100%;
  background-color: #f7f7f7;
}
.pretooltiparrow {
  left: 0px;
  margin: 0px;
  top: -16px;
  width: 40px;
  height: 16px;
  overflow: hidden;
  position: absolute;
}
.pretooltiparrow:before {
  background-color: #f7f7f7;
  border: 1px #ababab solid;
  z-index: 11;
  content: "";
  position: absolute;
  left: 15px;
  top: 10px;
  width: 25px;
  height: 25px;
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  -o-transform: rotate(45deg);
}
ul.typeahead-list i {
  margin-left: -10px;
  width: 18px;
}
[dir="rtl"] ul.typeahead-list i {
  margin-left: 0;
  margin-right: -10px;
}
ul.typeahead-list {
  max-height: 80vh;
  overflow: auto;
}
ul.typeahead-list > li > a {
  /** Firefox bug **/
  /* see https://github.com/jupyter/notebook/issues/559 */
  white-space: normal;
}
ul.typeahead-list  > li > a.pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .typeahead-list {
  text-align: right;
}
.cmd-palette .modal-body {
  padding: 7px;
}
.cmd-palette form {
  background: white;
}
.cmd-palette input {
  outline: none;
}
.no-shortcut {
  min-width: 20px;
  color: transparent;
}
[dir="rtl"] .no-shortcut.pull-right {
  float: left !important;
  float: left;
}
[dir="rtl"] .command-shortcut.pull-right {
  float: left !important;
  float: left;
}
.command-shortcut:before {
  content: "(command mode)";
  padding-right: 3px;
  color: #777777;
}
.edit-shortcut:before {
  content: "(edit)";
  padding-right: 3px;
  color: #777777;
}
[dir="rtl"] .edit-shortcut.pull-right {
  float: left !important;
  float: left;
}
#find-and-replace #replace-preview .match,
#find-and-replace #replace-preview .insert {
  background-color: #BBDEFB;
  border-color: #90CAF9;
  border-style: solid;
  border-width: 1px;
  border-radius: 0px;
}
[dir="ltr"] #find-and-replace .input-group-btn + .form-control {
  border-left: none;
}
[dir="rtl"] #find-and-replace .input-group-btn + .form-control {
  border-right: none;
}
#find-and-replace #replace-preview .replace .match {
  background-color: #FFCDD2;
  border-color: #EF9A9A;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .insert {
  background-color: #C8E6C9;
  border-color: #A5D6A7;
  border-radius: 0px;
}
#find-and-replace #replace-preview {
  max-height: 60vh;
  overflow: auto;
}
#find-and-replace #replace-preview pre {
  padding: 5px 10px;
}
.terminal-app {
  background: #EEE;
}
.terminal-app #header {
  background: #fff;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.terminal-app .terminal {
  width: 100%;
  float: left;
  font-family: monospace;
  color: white;
  background: black;
  padding: 0.4em;
  border-radius: 2px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
}
.terminal-app .terminal,
.terminal-app .terminal dummy-screen {
  line-height: 1em;
  font-size: 14px;
}
.terminal-app .terminal .xterm-rows {
  padding: 10px;
}
.terminal-app .terminal-cursor {
  color: black;
  background: white;
}
.terminal-app #terminado-container {
  margin-top: 20px;
}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sa { color: #BA2121 } /* Literal.String.Affix */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .dl { color: #BA2121 } /* Literal.String.Delimiter */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .fm { color: #0000FF } /* Name.Function.Magic */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .vm { color: #19177C } /* Name.Variable.Magic */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>
<style type="text/css">
    
/* Temporary definitions which will become obsolete with Notebook release 5.0 */
.ansi-black-fg { color: #3E424D; }
.ansi-black-bg { background-color: #3E424D; }
.ansi-black-intense-fg { color: #282C36; }
.ansi-black-intense-bg { background-color: #282C36; }
.ansi-red-fg { color: #E75C58; }
.ansi-red-bg { background-color: #E75C58; }
.ansi-red-intense-fg { color: #B22B31; }
.ansi-red-intense-bg { background-color: #B22B31; }
.ansi-green-fg { color: #00A250; }
.ansi-green-bg { background-color: #00A250; }
.ansi-green-intense-fg { color: #007427; }
.ansi-green-intense-bg { background-color: #007427; }
.ansi-yellow-fg { color: #DDB62B; }
.ansi-yellow-bg { background-color: #DDB62B; }
.ansi-yellow-intense-fg { color: #B27D12; }
.ansi-yellow-intense-bg { background-color: #B27D12; }
.ansi-blue-fg { color: #208FFB; }
.ansi-blue-bg { background-color: #208FFB; }
.ansi-blue-intense-fg { color: #0065CA; }
.ansi-blue-intense-bg { background-color: #0065CA; }
.ansi-magenta-fg { color: #D160C4; }
.ansi-magenta-bg { background-color: #D160C4; }
.ansi-magenta-intense-fg { color: #A03196; }
.ansi-magenta-intense-bg { background-color: #A03196; }
.ansi-cyan-fg { color: #60C6C8; }
.ansi-cyan-bg { background-color: #60C6C8; }
.ansi-cyan-intense-fg { color: #258F8F; }
.ansi-cyan-intense-bg { background-color: #258F8F; }
.ansi-white-fg { color: #C5C1B4; }
.ansi-white-bg { background-color: #C5C1B4; }
.ansi-white-intense-fg { color: #A1A6B2; }
.ansi-white-intense-bg { background-color: #A1A6B2; }

.ansi-bold { font-weight: bold; }

    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[111]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="s1">&#39;HOG-descriptor-from-scratch&#39;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>HOG-descriptor-from-scratch
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[112]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">datadir</span> <span class="o">=</span> <span class="s2">&quot;data&quot;</span>
<span class="n">dataset</span> <span class="o">=</span> <span class="s2">&quot;pedestrians128x64&quot;</span>
<span class="n">datafile</span> <span class="o">=</span> <span class="s2">&quot;</span><span class="si">%s</span><span class="s2">/</span><span class="si">%s</span><span class="s2">.tar.gz&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="n">datadir</span><span class="p">,</span> <span class="n">dataset</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[113]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">extractdir</span> <span class="o">=</span> <span class="s2">&quot;</span><span class="si">%s</span><span class="s2">/</span><span class="si">%s</span><span class="s2">&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="n">datadir</span><span class="p">,</span> <span class="n">dataset</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[114]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">extract_tar</span><span class="p">(</span><span class="n">filename</span><span class="p">):</span>
    <span class="k">try</span><span class="p">:</span>
        <span class="kn">import</span> <span class="nn">tarfile</span>
    <span class="k">except</span> <span class="ne">ImportError</span><span class="p">:</span>
        <span class="k">raise</span> <span class="ne">ImportError</span><span class="p">(</span><span class="s2">&quot;You do not have tarfile installed. &quot;</span>
                          <span class="s2">&quot;Try unzipping the file outside of &quot;</span>
                          <span class="s2">&quot;Python.&quot;</span><span class="p">)</span>
        <span class="n">tar</span> <span class="o">=</span> <span class="n">tarfile</span><span class="o">.</span><span class="n">open</span><span class="p">(</span><span class="n">datafile</span><span class="p">)</span>
        <span class="n">tar</span><span class="o">.</span><span class="n">extractall</span><span class="p">(</span><span class="n">path</span><span class="o">=</span><span class="n">extractdir</span><span class="p">)</span>
        <span class="n">tar</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="si">%s</span><span class="s2"> sucessfully extracted to </span><span class="si">%s</span><span class="s2">&quot;</span><span class="p">,</span> <span class="p">(</span><span class="n">datafile</span><span class="p">,</span>
                                                   <span class="n">extractdir</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[115]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">extract_tar</span><span class="p">(</span><span class="n">datafile</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[116]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">cv2</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[117]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">5</span><span class="p">):</span>
    <span class="n">filename</span> <span class="o">=</span> <span class="s2">&quot;</span><span class="si">%s</span><span class="s2">/per0010</span><span class="si">%d</span><span class="s2">.ppm&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="n">extractdir</span><span class="p">,</span> <span class="n">i</span><span class="p">)</span>
    <span class="n">img</span> <span class="o">=</span> <span class="n">cv2</span><span class="o">.</span><span class="n">imread</span><span class="p">(</span><span class="n">filename</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">subplot</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="n">i</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">cv2</span><span class="o">.</span><span class="n">cvtColor</span><span class="p">(</span><span class="n">img</span><span class="p">,</span> <span class="n">cv2</span><span class="o">.</span><span class="n">COLOR_BGR2RGB</span><span class="p">))</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s1">&#39;off&#39;</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[118]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">win_size</span> <span class="o">=</span> <span class="p">(</span><span class="mi">48</span><span class="p">,</span> <span class="mi">96</span><span class="p">)</span>
<span class="n">block_size</span> <span class="o">=</span> <span class="p">(</span><span class="mi">16</span><span class="p">,</span> <span class="mi">16</span><span class="p">)</span>
<span class="n">block_stride</span> <span class="o">=</span> <span class="p">(</span><span class="mi">8</span><span class="p">,</span> <span class="mi">8</span><span class="p">)</span>
<span class="n">cell_size</span> <span class="o">=</span> <span class="p">(</span><span class="mi">8</span><span class="p">,</span> <span class="mi">8</span><span class="p">)</span>
<span class="n">num_bins</span> <span class="o">=</span> <span class="mi">9</span>
<span class="n">hog</span> <span class="o">=</span> <span class="n">cv2</span><span class="o">.</span><span class="n">HOGDescriptor</span><span class="p">(</span><span class="n">win_size</span><span class="p">,</span> <span class="n">block_size</span><span class="p">,</span> <span class="n">block_stride</span><span class="p">,</span>
                        <span class="n">cell_size</span><span class="p">,</span> <span class="n">num_bins</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[119]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">random</span>
<span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="mi">42</span><span class="p">)</span>
<span class="n">X_pos</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">random</span><span class="o">.</span><span class="n">sample</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">900</span><span class="p">),</span> <span class="mi">400</span><span class="p">):</span>
    <span class="n">filename</span> <span class="o">=</span> <span class="s2">&quot;</span><span class="si">%s</span><span class="s2">/per</span><span class="si">%05d</span><span class="s2">.ppm&quot;</span> <span class="o">%</span> <span class="p">(</span><span class="n">extractdir</span><span class="p">,</span> <span class="n">i</span><span class="p">)</span>
    <span class="n">img</span> <span class="o">=</span> <span class="n">cv2</span><span class="o">.</span><span class="n">imread</span><span class="p">(</span><span class="n">filename</span><span class="p">)</span>
    <span class="k">if</span> <span class="n">img</span> <span class="ow">is</span> <span class="kc">None</span><span class="p">:</span>
        <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Could not find image </span><span class="si">%s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">filename</span><span class="p">)</span>
        <span class="k">continue</span>
    <span class="n">X_pos</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">hog</span><span class="o">.</span><span class="n">compute</span><span class="p">(</span><span class="n">img</span><span class="p">,</span> <span class="p">(</span><span class="mi">64</span><span class="p">,</span> <span class="mi">64</span><span class="p">)))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Could not find image data/pedestrians128x64/per00000.ppm
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[120]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">X_pos</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">X_pos</span><span class="p">,</span> <span class="n">dtype</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">float32</span><span class="p">)</span>
<span class="n">y_pos</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">ones</span><span class="p">(</span><span class="n">X_pos</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="n">dtype</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">int32</span><span class="p">)</span>
<span class="n">X_pos</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">y_pos</span><span class="o">.</span><span class="n">shape</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[120]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>((399, 1980, 1), (399,))</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[121]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">negdir</span> <span class="o">=</span> <span class="s2">&quot;</span><span class="si">%s</span><span class="s2">/pedestrians_neg&quot;</span> <span class="o">%</span> <span class="n">datadir</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[122]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">os</span>
<span class="n">hroi</span> <span class="o">=</span> <span class="mi">128</span>
<span class="n">wroi</span> <span class="o">=</span> <span class="mi">64</span>
<span class="n">X_neg</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">negfile</span> <span class="ow">in</span> <span class="n">os</span><span class="o">.</span><span class="n">listdir</span><span class="p">(</span><span class="n">negdir</span><span class="p">):</span>
    <span class="n">filename</span> <span class="o">=</span> <span class="s1">&#39;</span><span class="si">%s</span><span class="s1">/</span><span class="si">%s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span><span class="n">negdir</span><span class="p">,</span> <span class="n">negfile</span><span class="p">)</span>
    <span class="n">img</span> <span class="o">=</span> <span class="n">cv2</span><span class="o">.</span><span class="n">imread</span><span class="p">(</span><span class="n">filename</span><span class="p">)</span>
    <span class="n">img</span> <span class="o">=</span> <span class="n">cv2</span><span class="o">.</span><span class="n">resize</span><span class="p">(</span><span class="n">img</span><span class="p">,</span> <span class="p">(</span><span class="mi">512</span><span class="p">,</span> <span class="mi">512</span><span class="p">))</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">5</span><span class="p">):</span>
        <span class="n">rand_y</span> <span class="o">=</span> <span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">img</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">-</span> <span class="n">hroi</span><span class="p">)</span>
        <span class="n">rand_x</span> <span class="o">=</span> <span class="n">random</span><span class="o">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">img</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span> <span class="o">-</span> <span class="n">wroi</span><span class="p">)</span>
        <span class="n">roi</span> <span class="o">=</span> <span class="n">img</span><span class="p">[</span><span class="n">rand_y</span><span class="p">:</span><span class="n">rand_y</span> <span class="o">+</span> <span class="n">hroi</span><span class="p">,</span> <span class="n">rand_x</span><span class="p">:</span><span class="n">rand_x</span> <span class="o">+</span> <span class="n">wroi</span><span class="p">,</span> <span class="p">:]</span>
        <span class="n">X_neg</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">hog</span><span class="o">.</span><span class="n">compute</span><span class="p">(</span><span class="n">roi</span><span class="p">,</span> <span class="p">(</span><span class="mi">64</span><span class="p">,</span> <span class="mi">64</span><span class="p">)))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[123]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">X_neg</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">X_neg</span><span class="p">,</span> <span class="n">dtype</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">float32</span><span class="p">)</span>
<span class="n">y_neg</span> <span class="o">=</span> <span class="o">-</span><span class="n">np</span><span class="o">.</span><span class="n">ones</span><span class="p">(</span><span class="n">X_neg</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="n">dtype</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">int32</span><span class="p">)</span>
<span class="n">X_neg</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">y_neg</span><span class="o">.</span><span class="n">shape</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[123]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>((250, 1980, 1), (250,))</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[124]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">X</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">concatenate</span><span class="p">((</span><span class="n">X_pos</span><span class="p">,</span> <span class="n">X_neg</span><span class="p">))</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">concatenate</span><span class="p">((</span><span class="n">y_pos</span><span class="p">,</span> <span class="n">y_neg</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[125]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn</span> <span class="k">import</span> <span class="n">model_selection</span> <span class="k">as</span> <span class="n">ms</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">ms</span><span class="o">.</span><span class="n">train_test_split</span><span class="p">(</span>
    <span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span>
<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[126]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">train_svm</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">):</span>
    <span class="n">svm</span> <span class="o">=</span> <span class="n">cv2</span><span class="o">.</span><span class="n">ml</span><span class="o">.</span><span class="n">SVM_create</span><span class="p">()</span>
    <span class="n">svm</span><span class="o">.</span><span class="n">train</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">cv2</span><span class="o">.</span><span class="n">ml</span><span class="o">.</span><span class="n">ROW_SAMPLE</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">svm</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[127]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">score_svm</span><span class="p">(</span><span class="n">svm</span><span class="p">,</span> <span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">):</span>
    <span class="kn">from</span> <span class="nn">sklearn</span> <span class="k">import</span> <span class="n">metrics</span>
    <span class="n">_</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">svm</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">metrics</span><span class="o">.</span><span class="n">accuracy_score</span><span class="p">(</span><span class="n">y</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[128]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">svm</span> <span class="o">=</span> <span class="n">train_svm</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="n">score_svm</span><span class="p">(</span><span class="n">svm</span><span class="p">,</span> <span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[128]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>1.0</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[129]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">score_svm</span><span class="p">(</span><span class="n">svm</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[129]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>0.6461538461538462</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[130]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">score_train</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">score_test</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">3</span><span class="p">):</span>
    <span class="n">svm</span> <span class="o">=</span> <span class="n">train_svm</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
    <span class="n">score_train</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">score_svm</span><span class="p">(</span><span class="n">svm</span><span class="p">,</span> <span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">))</span>
    <span class="n">score_test</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">score_svm</span><span class="p">(</span><span class="n">svm</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">))</span>
    <span class="n">_</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">svm</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>
    <span class="n">false_pos</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">logical_and</span><span class="p">((</span><span class="n">y_test</span><span class="o">.</span><span class="n">ravel</span><span class="p">()</span> <span class="o">==</span> <span class="o">-</span><span class="mi">1</span><span class="p">),</span>
                               <span class="p">(</span><span class="n">y_pred</span><span class="o">.</span><span class="n">ravel</span><span class="p">()</span> <span class="o">==</span> <span class="mi">1</span><span class="p">))</span>
    <span class="k">if</span> <span class="ow">not</span> <span class="n">np</span><span class="o">.</span><span class="n">any</span><span class="p">(</span><span class="n">false_pos</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;no more false positives: done&#39;</span><span class="p">)</span>
        <span class="k">break</span>
    <span class="n">X_train</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">concatenate</span><span class="p">((</span><span class="n">X_train</span><span class="p">,</span>
                              <span class="n">X_test</span><span class="p">[</span><span class="n">false_pos</span><span class="p">,</span> <span class="p">:]),</span>
                             <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
    <span class="n">y_train</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">concatenate</span><span class="p">((</span><span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span><span class="p">[</span><span class="n">false_pos</span><span class="p">]),</span>
                             <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>no more false positives: done
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[131]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">score_train</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[131]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[1.0, 1.0]</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[132]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">score_test</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt output_prompt">Out[132]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[0.6461538461538462, 1.0]</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[136]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">stride</span> <span class="o">=</span> <span class="mi">16</span>
<span class="n">found</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">img_test</span> <span class="o">=</span> <span class="n">cv2</span><span class="o">.</span><span class="n">imread</span><span class="p">(</span><span class="s1">&#39;img_test.jpg&#39;</span><span class="p">)</span>
<span class="k">for</span> <span class="n">ystart</span> <span class="ow">in</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">img_test</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="n">stride</span><span class="p">):</span>
    <span class="k">for</span> <span class="n">xstart</span> <span class="ow">in</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">img_test</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">],</span> <span class="n">stride</span><span class="p">):</span>
        <span class="k">if</span> <span class="n">ystart</span> <span class="o">+</span> <span class="n">hroi</span> <span class="o">&gt;</span> <span class="n">img_test</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]:</span>
            <span class="k">continue</span>
        <span class="k">if</span> <span class="n">xstart</span> <span class="o">+</span> <span class="n">wroi</span> <span class="o">&gt;</span> <span class="n">img_test</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]:</span>
             <span class="k">continue</span>
        <span class="n">roi</span> <span class="o">=</span> <span class="n">img_test</span><span class="p">[</span><span class="n">ystart</span><span class="p">:</span><span class="n">ystart</span> <span class="o">+</span> <span class="n">hroi</span><span class="p">,</span>
                       <span class="n">xstart</span><span class="p">:</span><span class="n">xstart</span> <span class="o">+</span> <span class="n">wroi</span><span class="p">,</span> <span class="p">:]</span>
        <span class="n">feat</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="n">hog</span><span class="o">.</span><span class="n">compute</span><span class="p">(</span><span class="n">roi</span><span class="p">,</span> <span class="p">(</span><span class="mi">64</span><span class="p">,</span> <span class="mi">64</span><span class="p">))])</span>
        <span class="n">_</span><span class="p">,</span> <span class="n">ypred</span> <span class="o">=</span> <span class="n">svm</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">feat</span><span class="p">)</span>
        
        <span class="k">if</span> <span class="n">np</span><span class="o">.</span><span class="n">allclose</span><span class="p">(</span><span class="n">ypred</span><span class="p">,</span> <span class="mi">1</span><span class="p">):</span>
            <span class="n">found</span><span class="o">.</span><span class="n">append</span><span class="p">((</span><span class="n">ystart</span><span class="p">,</span> <span class="n">xstart</span><span class="p">,</span> <span class="n">hroi</span><span class="p">,</span> <span class="n">wroi</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[137]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">rho</span><span class="p">,</span> <span class="n">_</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">svm</span><span class="o">.</span><span class="n">getDecisionFunction</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="n">sv</span> <span class="o">=</span> <span class="n">svm</span><span class="o">.</span><span class="n">getSupportVectors</span><span class="p">()</span>
<span class="n">hog</span><span class="o">.</span><span class="n">setSVMDetector</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">sv</span><span class="o">.</span><span class="n">ravel</span><span class="p">(),</span> <span class="n">rho</span><span class="p">))</span>
<span class="n">found</span> <span class="o">=</span> <span class="n">hog</span><span class="o">.</span><span class="n">detectMultiScale</span><span class="p">(</span><span class="n">img_test</span><span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>


<div class="output_subarea output_text output_error">
<pre>
<span class="ansi-red-fg">---------------------------------------------------------------------------</span>
<span class="ansi-red-fg">error</span>                                     Traceback (most recent call last)
<span class="ansi-green-fg">&lt;ipython-input-137-2586b15c274f&gt;</span> in <span class="ansi-cyan-fg">&lt;module&gt;</span>
<span class="ansi-green-intense-fg ansi-bold">      1</span> rho<span class="ansi-blue-fg">,</span> _<span class="ansi-blue-fg">,</span> _ <span class="ansi-blue-fg">=</span> svm<span class="ansi-blue-fg">.</span>getDecisionFunction<span class="ansi-blue-fg">(</span><span class="ansi-cyan-fg">0</span><span class="ansi-blue-fg">)</span>
<span class="ansi-green-intense-fg ansi-bold">      2</span> sv <span class="ansi-blue-fg">=</span> svm<span class="ansi-blue-fg">.</span>getSupportVectors<span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">)</span>
<span class="ansi-green-fg">----&gt; 3</span><span class="ansi-red-fg"> </span>hog<span class="ansi-blue-fg">.</span>setSVMDetector<span class="ansi-blue-fg">(</span>np<span class="ansi-blue-fg">.</span>append<span class="ansi-blue-fg">(</span>sv<span class="ansi-blue-fg">.</span>ravel<span class="ansi-blue-fg">(</span><span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">,</span> rho<span class="ansi-blue-fg">)</span><span class="ansi-blue-fg">)</span>
<span class="ansi-green-intense-fg ansi-bold">      4</span> found <span class="ansi-blue-fg">=</span> hog<span class="ansi-blue-fg">.</span>detectMultiScale<span class="ansi-blue-fg">(</span>img_test<span class="ansi-blue-fg">)</span>

<span class="ansi-red-fg">error</span>: OpenCV(4.0.0) /Users/travis/build/skvark/opencv-python/opencv/modules/objdetect/src/hog.cpp:115: error: (-215:Assertion failed) checkDetectorSize() in function &#39;setSVMDetector&#39;
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[138]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">matplotlib</span> <span class="k">import</span> <span class="n">patches</span>
<span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
<span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">111</span><span class="p">)</span>
<span class="n">ax</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">cv2</span><span class="o">.</span><span class="n">cvtColor</span><span class="p">(</span><span class="n">img_test</span><span class="p">,</span> <span class="n">cv2</span><span class="o">.</span><span class="n">COLOR_BGR2RGB</span><span class="p">))</span>

<span class="k">for</span> <span class="n">f</span> <span class="ow">in</span> <span class="n">found</span><span class="p">:</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">add_patch</span><span class="p">(</span><span class="n">patches</span><span class="o">.</span><span class="n">Rectangle</span><span class="p">((</span><span class="n">f</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="n">f</span><span class="p">[</span><span class="mi">1</span><span class="p">]),</span> <span class="n">f</span><span class="p">[</span><span class="mi">2</span><span class="p">],</span> <span class="n">f</span><span class="p">[</span><span class="mi">3</span><span class="p">],</span>
                                   <span class="n">color</span><span class="o">=</span><span class="s1">&#39;y&#39;</span><span class="p">,</span> <span class="n">linewidth</span><span class="o">=</span><span class="mi">3</span><span class="p">,</span>
                                   <span class="n">fill</span><span class="o">=</span><span class="kc">False</span><span class="p">))</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

    <div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span> 
</pre></div>

    </div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span> 
</pre></div>

    </div>
</div>
</div>

</div>
    </div>
  </div>
</body>

 


</html>
