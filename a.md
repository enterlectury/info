# 📘 How to Implement Own Template Page on Live WordPress Site

This guide explains step-by-step how to upload your **custom HTML/CSS/JS** and set it as the **homepage** in WordPress.

---

### 🔹 Steps

🔴 1. **Login via SSH (terminal).**

🔴 2. **Navigate to your active theme directory:** ` cd /var/www/html/wp-content/themes/astra`
   
🔴 4. Create a custom template file (e.g., homepage-template.php):

```
<?php
/*
Template Name: Custom Homepage
*/
get_header(); ?>

<!-- Your HTML here -->
<div id="custom-home">
<?php
// Load raw HTML file content if you want to keep index.html separate
// echo file_get_contents(get_stylesheet_directory() . '/index.html');
?>
</div>

<?php get_footer(); ?>
```

🔴 4. Create an assets2 directory to keep your custom CSS/JS: `mkdir /var/www/html/wp-content/themes/astra/assets2` Move your style.css, script.js, or other files here.

<br><br>
🔴 5. Edit functions.php → append this at the bottom:
```
function custom_homepage_assets() {
    if (is_page_template('homepage-template.php')) {
        wp_enqueue_style('custom-homepage', get_stylesheet_directory_uri() . '/assets2/style.css');
        wp_enqueue_script('custom-homepage', get_stylesheet_directory_uri() . '/assets2/script.js', array(), false, true);
    }
}
add_action('wp_enqueue_scripts', 'custom_homepage_assets');
```
<br><br>

🔴 6. Set up the page in WordPress Admin Panel:

Login → Pages → Add New Page. -> Name it Home (or any name you like). ->  On the right side → Page Attributes → Template → Custom Homepage. -> Click Publish.

<br>

🔴 7. Make it the Front Page:

Go to Settings → Reading. -> Under Your homepage displays, choose: -> A static page → Homepage: Home (the one you just made). -> Save changes.

<br><br>

This is **ready-to-upload to GitHub**, fully self-contained, with code sections collapsible for readability.  

If you want, I can also **add a table of contents at the top** with clickable links to steps so it’s super neat for GitHub viewing. Do you want me to do that?
