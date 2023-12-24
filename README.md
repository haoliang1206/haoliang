<!DOCTYPE html>
<html lang="en">
    <head>
		<meta charset="utf-8">
 
		<meta name="description" content="A Christmas tree built out of form elements." />
		<meta name="author" content="Hakim El Hattab" />
 
		<meta http-equiv="X-UA-Compatible" content="chrome=1">
 
        <title>圣诞树</title>
 
		<link href='https://fonts.googleapis.com/css?family=Armata' rel='stylesheet' type='text/css'>
		
		<style type="text/css">
			html{color:#000;background:#222222;}
			a{cursor:pointer;}
			html,body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,code,form,fieldset,legend,input,textarea,p,blockquote,th,td{margin:0;padding:0;}
			table{border-collapse:collapse;border-spacing:0;}
			fieldset,img{border:0;}
			address,caption,cite,code,dfn,em,strong,th,var{font-style:normal;font-weight:normal;}
			li{list-style:none;}
			caption,th{text-align:left;}
			/* h1,h2,h3,h4,h5,h6{font-size:100%;} */
			q:before,q:after{content:'';}
			abbr,acronym {border:0;font-variant:normal;}
			sup {vertical-align:text-top;}
			sub {vertical-align:text-bottom;}
			input,textarea,select{font-family:inherit;font-size:inherit;font-weight:inherit;outline-style:none;outline-width:0pt;}
			legend{color:#000;}
			a:focus,object,h1,h2,h3,h4,h5,h6{-moz-outline-style: none; border:0px;}
			/*input[type="Submit"]{cursor:pointer;}*/
			strong {font-weight: bold;}
			body, html {
				overflow: hidden;
				font-family: Helvetica, Arial, sans-serif;
				color: #fff;
				font-size: 11px;
 
				width: 100%;
				height: 100%;
 
				background: #b72424;
				background: -moz-radial-gradient(center, ellipse cover, #b72424 0%, #492727 100%);
				background: -webkit-gradient(radial, center center, 0px, center center, 100%, color-stop(0%,#b72424), color-stop(100%,#492727));
				background: -webkit-radial-gradient(center, ellipse cover, #b72424 0%,#492727 100%);
				background: radial-gradient(center, ellipse cover, #b72424 0%,#492727 100%);
			}
 
			@keyframes spin {
				0% { transform: rotateY( 0deg ); }
				100% { transform: rotateY( 360deg ); }
			}
 
			body {
				perspective: 3000px;
				perspective-origin: 0 20%;
			}
 
			.tree {
				margin: 0 auto;
				position: relative;
				animation: spin 18s infinite linear;
				transform-origin: 50% 0;
				transform-style: preserve-3d;
			}
 
			.tree * {
				position: absolute;
				transform-origin: 0 0;
			}
		</style>
 
 
    </head>
    <body>
		<audio src="music.wav" autoplay loop controls></audio>
		
    	<div class="tree"></div>
 
		<script type="text/javascript">
			// JavaScript Document
const width = 500;
const height = 600;
const quantity = 150;
const types = [ 'text', 'select', 'progress', 'meter', 'button', 'radio', 'checkbox' ];
const greetings = [ '圣诞节快乐','圣诞节快乐','Merry Christmas','Merry Christmas','Merry Christmas','Merry Christmas','圣诞节快乐','圣诞节快乐','圣诞节快乐','Merry Christmas','Happy Holidays', ' 圣诞节快乐','圣诞节快乐','圣诞节快乐','Merry Christmas','圣诞节快乐','Merry Christmas','圣诞节快乐' ];
let tree = document.querySelector( '.tree' ),
	treeRotation = 0;
 
tree.style.width = width + 'px';
tree.style.height = height + 'px';
 
window.addEventListener( 'resize', resize, false );
 
// The tree
for( var i = 0; i < quantity; i++ ) {
	let element = null,
		type = types[ Math.floor( Math.random() * types.length ) ],
		greeting = greetings[ Math.floor( Math.random() * greetings.length ) ];
 
	let x = width/2,
		y = Math.round( Math.random() * height );
 
	let rx = 0,
		ry = Math.random() * 360,
		rz = -Math.random() * 15;
 
	let elemenWidth = 5 + ( ( y / height ) * width / 2 ),
		elemenHeight = 26;
 
	switch( type ) {
		case 'button':
			element = document.createElement( 'button' );
			element.textContent = greeting;
			element.style.width = elemenWidth + 'px';
			element.style.height = elemenHeight + 'px';
			break;
		case 'progress':
			element = document.createElement( 'progress' );
			element.style.width = elemenWidth + 'px';
			element.style.height = elemenHeight + 'px';
			if( Math.random() > 0.5 ) {
				element.setAttribute( 'max', '100' );
				element.setAttribute( 'value', Math.round( Math.random() * 100 ) );
			}
			break;
		case 'select':
			element = document.createElement( 'select' );
			element.setAttribute( 'selected', greeting );
			element.innerHTML = '<option>' + greetings.join( '</option><option>' ) + '</option>';
			element.style.width = elemenWidth + 'px';
			element.style.height = elemenHeight + 'px';
			break;
		case 'meter':
			element = document.createElement( 'meter' );
			element.setAttribute( 'min', '0' );
			element.setAttribute( 'max', '100' );
			element.setAttribute( 'value', Math.round( Math.random() * 100 ) );
			element.style.width = elemenWidth + 'px';
			element.style.height = elemenHeight + 'px';
			break;
		case 'text':
		default:
			element = document.createElement( 'input' );
			element.setAttribute( 'type', 'text' );
			element.setAttribute( 'value', greeting );
			element.style.width = elemenWidth + 'px';
			element.style.height = elemenHeight + 'px';
	}
 
	element.style.transform = `translate3d(${x}px, ${y}px, 0px) rotateX(${rx}deg) rotateY(${ry}deg) rotateZ(${rz}deg)`;
 
	tree.appendChild( element );
}
 
// Let it snow
for( var i = 0; i < 200; i++ ) {
	let element = document.createElement( 'input' );
	element.setAttribute( 'type', 'radio' );
 
	let spread = window.innerWidth/2;
 
	let x = Math.round( Math.random() * spread ) - ( spread / 4 ),
		y = Math.round( Math.random() * height ),
		z = Math.round( Math.random() * spread ) - ( spread / 2 );
 
	let rx = 0,
		ry = Math.random() * 360,
		rz = 0;
 
	if( Math.random() > 0.5 ) element.setAttribute( 'checked', '' );
 
	element.style.transform = `translate3d(${x}px, ${y}px, ${z}px) rotateX(${rx}deg) rotateY(${ry}deg) rotateZ(${rz}deg)`;
 
	tree.appendChild( element );
}
 
function resize() {
	tree.style.top = ( ( window.innerHeight - height - 100 ) / 2 ) + 'px';
}
 
resize();
		</script>
 
		<!-- Third party scripts and sharing UI -->
		<p class="project-title">圣诞树</p>
 
		<style type="text/css" media="screen">
			.project-title {
				position: absolute;
				left: 25px;
				bottom: 20px;
 
				font-size: 16px;
				color: #fff;
			}
 
			.credits {
				position: absolute;
				right: 20px;
				bottom: 25px;
				font-size: 15px;
				z-index: 20;
				color: #fff;
				vertical-align: middle;
			}
 
			.credits * + * {
				margin-left: 15px;
			}
 
			.credits a {
				padding: 8px 10px;
				color: rgba(255,255,255,0.7);
				border: 2px solid rgba(255,255,255,0.7);
				text-decoration: none;
			}
 
			.credits a:hover {
				border-color: #fff;
				color: #fff;
			}
 
			@media screen and (max-width: 1040px) {
				.project-title {
					display: none;
				}
 
				.credits {
					width: 100%;
					left: 0;
					right: auto;
					bottom: 0;
					padding: 30px 0;
					background: #b72424;
					text-align: center;
				}
 
				.credits a {
					display: inline-block;
					margin-top: 7px;
					margin-bottom: 7px;
				}
			}
		</style>
 
		<script>
			var _gaq = [['_setAccount', 'UA-15240703-1'], ['_trackPageview']];
			(function(d, t) {
			var g = d.createElement(t),
			    s = d.getElementsByTagName(t)[0];
			g.async = true;
			g.src = ('https:' == location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
			s.parentNode.insertBefore(g, s);
			})(document, 'script');
		</script>
 
    </body>
</html>
