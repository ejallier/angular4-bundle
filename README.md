angular2-bundle
===============
*Full bundle of Angular 2 that can be put into a script tag.*

Now that Angular 2 is out, there are things that I missed in the old beta versions.
For example, the beta Angular 2 bundle files used to be `System.js` modules that 
I can quickly put into a `script` tag.

No more. They are now UMD modules that require a build process (e.g. with WebPack).

For those who don't want to bother with a build step (and just want all of Angular 2
anyway), I have hand-crafted a bundle that you can simply throw into your HTML page.


How to Use
----------

~~~~~~~~~~ {.html}
<!DOCTYPE html>
<html>
<head>
	<base href="/">

  <!-- Polyfills for ES6 -->
	<script src="polyfills.js"></script>

	<!-- Library bundle -->
	<script src="bundle.min.js"></script>

	<!-- Your scripts -->
	<script src="script.js"></script>

	<script type="text/javascript">
		// Bootstrap the main component
		document.addEventListener("DOMContentLoaded", function ()
		{
			System.import("main").catch(console.error.bind(console));
		});
	</script>
</head>

<body>
</body>
</html>
~~~~~~~~~~
