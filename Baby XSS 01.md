    <script src="hook.js"></script>
    <?php
    echo $_GET["payload"];
    ?>

    <h1>inject</h1>
    <form>
    <input type="text" name="payload" placeholder="your payload here">
    <input type="submit" value="GO">
    </form>

    <h1>src</h1>
    <?php highlight_string(file_get_contents(basename(__FILE__))); ?>

Simply typed `<script>javascript:alert('XSS');</script>` in the input field and won.
