angular2-bundle
===============
*Full bundle of Angular 4 that can be put into a script tag.*

Now that Angular 2 (and now 4) is out, there are things that I missed in the old
Angular 2 beta versions.
For example, the beta Angular 2 bundle files used to be `System.js` modules that 
I can quickly put into a `script` tag.

No more. They are now UMD modules that require a build process (e.g. with WebPack).

For those who don't want to bother with a build step (and just want all of Angular 4
anyway), I have hand-crafted a bundle that you can simply throw into your HTML page.

This version is 4.1.3.


How to Use
----------

~~~~~~~~~~ {.html}
<!DOCTYPE html>
<html>
<head>
	<base href="/">

	<!-- Polyfills for ES6 -->
	<script src="polyfills-4.1.3.js"></script>

	<!-- Library bundle -->
	<script src="bundle-4.1.3.min.js"></script>

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


What's Included
---------------

* `Zone.js`
* `Reflect.js`
* `System.js`
* `Rx.js`

* `@angular/core`
* `@angular/common`
* `@angular/compiler`
* `@angular/platform-browser`
* `@angular/platform-browser-dynamic`
* `@angular/forms`
* `@angular/http`
* `@angular/router`
* `@angular/animations`


Note on Rx
----------

The `rxjs` bundle included is the whole thing.  It does not split into
further modules.  As a result, you only have to `import { ... } from "rxjs/Rx"`
to get the entire feature set.

Loading individual `Rx` modules is not supported.  For example, the following
is not supported:

~~~~~~~~ {.js}
import { merge } from "rxjs/operator/merge";

merge(...);
~~~~~~~~

Instead, simply importing the entire `Rx` package will be fine:

~~~~~~~~ {.js}
import { Observable } from "rxjs/Rx";

...merge(...);
Observable.prototype.merge(...);
~~~~~~~~

Instead of:


~~~~~~~~ {.js}
import { from } from "rxjs/Observable/from";

var obs = from(...);
~~~~~~~~

do this:

~~~~~~~~ {.js}
import { from } from "rxjs/Rx";

var obs = Observable.from(...);
~~~~~~~~


How Is It Done?
---------------

Well, I merged the above UMD bundle files, in the correct order, then
manually hand-edited the file, converting UMD module declaration headers
with `System.amdDefine` calls.


How Large Is It?
----------------

Raw: `polyfills.js`: 78KB, `bundle-4.1.3.min.js`: 1MB, Total: 1,078KB  
Gzipped: `polyfills.js`: 27KB, `bundle-4.1.3.min.js`: 233KB, Total: 260KB  
