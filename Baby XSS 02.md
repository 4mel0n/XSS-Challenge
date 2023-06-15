```
<script src="hook.js"></script>
<script>
    window.addEventListener("load", function() {
        var q = location.hash.substring(1);
        window.query.innerHTML = q == '' ? `Hello!` : (`Hello, ${decodeURI(q)}`);
    });
</script>

<p id="query"></p>

<h1>inject</h1>
<p>Inspect the source code carefully and find where to inject :-)</p>

<h1>src</h1>
<?php highlight_string(file_get_contents(basename(__FILE__))); ?>
```
This is a DOM based XSS exploit. First thing I tried was injecting into the URL ```https://xss.challenge.training.hacq.me/challenges/baby02.php=<script>javascript:alert('XSS')</script>```, but this only brought me to a 404 error.
