# WordPress-Guide-Lines
=	Required Plugins: =
Theme can recommend plugins but not make them required. This is most is your submitting theme in WordPress.org but for theme forest it's recommended.
= Screenshot Issues: =
The screenshot should be of the actual theme as it appears with default options, not a logo or mockup. Screenshot size should be 1200x900, to account for HiDPI displays. Any 4:3 image size is acceptable, but 1200x900 is preferred.
•	Readme File: For proper readme file, you can read more at https://make.wordpress.org/themes/2014/07/08/proper-copyrightlicense-attribution-for-themes/.
•	Third party Resources: Make sure you first have permission to distribute third party resources. And, make sure to list the copyright and license for each in your readme.
•	Other Framewords/Plugins: If you have used any frameworks, you need to keep them updated.
•	Admin Menu: Themes are not allowed to add anything in admin bar.
•	Theme Options: There is no need to add Theme Options page since all options are already in customizer.
•	Custom Logo: As of WordPress version 4.5, logo can be added via theme support and in included in core, so you need to use it rather than adding using custom header. More info: https://make.wordpress.org/core/2016/03/10/custom-logo/. Also, remove default logo image.
•	Fatal Errors: If you are using third party functions, you need to use function_exists check.
•	Unused Variables: Removed unused variables.
•	Translation Issues: Make every string strings translation ready.  https://gist.github.com/emiluzelac/32d53ab85c05cda846ad61590588a7bb .
•	Search Form issue: If you are adding theme support for search-form then you shouldn't use searchform.php. Choose one or the other.
•	Prefixing styles/scripts handles: Only custom scripts and styles need handle prefix
o	Third party scripts/styles must not have handle prefixed
o	For reference, check: https://github.com/grappler/wp-standard-handles.
o	
•	Using core scripts: Datepicker : WordPress Core has jquery-ui datepicker bundled in core, so, if you want to use datepicked, simply use that one. 
o	Do not enqueue extra script for datepicked.
•	Using core functions: Pagination : You can just use function the_posts_pagination(), it will display like the one you need.
•	Prefixing: Functions: All functions must be prefixed with theme_slug
o	Ref: http://themereview.co/prefix-all-the-things/.
•	Commented Code: Remove all commented codes in production version of theme.
•	Plugin Territory: Login Page manipulation : Manipulating login page, in this case adding logo, falls under plugin territory, which means, this functionality needs to be removed from theme and added in via plugin.
•	Using core functionality: Image resize : WordPress resizes images when the image sizes are added via add_image_size
o	If you really need then you need to resize image using core functions rather than using custom functionality
o	Image resizing is definitely plugin territory. Themes should use the core WP functions available to them -- add_image_size() and the_post_thumbnail(). By using the core functions, it allows users to choose their preferred plugin for any custom image resizing (or no plugin at all).
•	Plugin Territory: Social Sharing:
•	Input Sanitization:
•	Escaping Translated Strings: Recommended escaping translation strings : All translation functions must be escaped as sometimes an improper translation may break the html.
o	Almost all instances of __()/_e() need to be esc_html__()/esc_html_e()
o	esc_attr__() where used as attribute values
o	passed via wp_kses() if some html elements are required
o	You do not need to translate variables. Only hard coded strings are in need of translation.
o	Note: if you want to use post's title as attribute then use the_title_attribute instead of the_title().
•	Code Optimization:
•	Output Sanitization/Escaping output issues : 
o	Escape following using esc_url
o	Sanitize email outputs using antispambot()
o	Escape following using esc_attr
o	Use the_title_attribute() instead of the_title() where title is being used as attribute
o	https://divpusher.com/blog/wordpress-customizer-sanitization-examples
•	Error Notices: Theme should not produce any error OR norices.
•	Use . to concatenate rather than ,
inc/extras.php file. echo '<link rel="pingback" href="'. bloginfo( 'pingback_url' ) . '">';
•	Unused Bundled Scripts
•	Run the code sniffer - https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards
phpcs --standard=WordPress PATH_TO_THE_PROJECT >> PATH_TO_SAVE_FILE
Ex: c:\codesniffer>phpcs --standard=WordPress C:\xampp\htdocs\pest-guard\wp-content\
themes\pest-guard >> C:\xampp\htdocs\pest-guard\wp-content\themes\pest-guard\cod
esniffer.txt
•	Incorrect Locale file: Core WP auto-loads the rtl.css file if it exists in the root directory. Your theme is loading it like this:
o	If you wish to change the location of the locale-stylesheet, you should filter locale_stylesheet_uriinstead: https://developer.wordpress.org/reference/hooks/locale_stylesheet_uri/
o	Be sure to properly account for child themes too.
•	Use comments number function : In comments.php, use the comments_number() function to properly output the comments header: https://codex.wordpress.org/Function_Reference/comments_number
o	Additionally, you shouldn't use all caps like COMMENTS. If you want all caps, use CSS to handle that rather than doing it in the HTML.
•	User Core excerpt function: Instead of writing your own excerpt function, use the excerpt_length filter hook to control the number of words shown: https://developer.wordpress.org/reference/hooks/excerpt_length/
•	Categories Display: Themes should display all of the user-selected categories for a post. There's no real design limitation in this theme where this should be limited to a single category.
o	Additionally, you don't need the category code in content-page.php because pages don't support categories.
•	Post Date: Because you're using the core the_date() function, the date will not be output when multiple posts have the same date on the page. It's only output for the first post. Following posts show "Date: ".
o	Instead, use echo get_the_date().
•	Stying Avatars: Avatars in comments are stretched. They're currently set at 32 x 32 px, but the theme stretches them to much larger. See screenshot.
•	Stying Galleries: When using the [gallery] shortcode, it's not adhering to the columns it's supposed to be in. The screenshot should be 3 columns. Instead, everything is lined up in a single column.
•	Outputting tags and categories : When outputting post tags and categories, use an appropriate core function, such as get_the_term_list(): https://codex.wordpress.org/Function_Reference/get_the_term_list
•	Styling: Lists in comment text : Make sure to account for <ul> and <ol> lists when used within comment text. Right now, the lists items are missing bullets and have huge left margins. See screenshot.
•	Missing pingbacks/trackbacks : Themes must support all core comment types (comment, pingback, and trackback). It'd be even better if it supported custom comment types too (though not a requirement anywhere).
o	Make sure to account for pingbacks and trackbacks too.
•	Avoid the global $post: In various places in the theme, you've used the global $post variable. This should be avoided if at all possible. Use the available WP function when it's available because they often have filter hooks that plugins may filter for various reasons. And, it makes your code more future-proof.
o	For example, this from single.php:
o	get_template_part( 'template-parts/content', $post->post_type );
o	$post->post_type should be replaced with get_post_type().
•	Security: Paged variable : In template-grid.php and template-listing.php, make sure to wrap $paged with intval().
•	Prefixing: Global variables : In admin/simon-config.php, you have many variables in the global namespace. Make sure to prefix those with simontaxi_. Or, better yet, wrap all of that code up in a function.
•	Encode all variables: In inc/section-socialshare.php, make sure to wrap the $title variable in urlencode().
•	Paginated Posts: Make sure to call wp_link_pages() when displaying the single post/page: https://codex.wordpress.org/Function_Reference/wp_link_pages
o	This is used to display pagination when the user uses <!--nextpage--> in the post editor.
•	Do not use any deprecated functions:
•	Including core files: In inc/top-banner-front.php (and any other places), you should never include core admin files like this on the front end:
include_once( ABSPATH . 'wp-admin/includes/plugin.php' );
I understand that the purpose is to use the is_plugin_active() function, but that's not the best way to do that. Instead, use a function_exists() check to check if one of the plugin's functions exist.
•	Security: Customizer Settings: __return_false is not an acceptable function for the sanitize_callback argument when adding customizer settings. A reviewer at a place like WordPress.org or ThemeForest would likely see this as an attempt to bypass security checks and sneak something nasty into their repository. That's a red flag.
o	Make sure to sanitize each bit of data correctly based on the type of data the setting should return.
o	Meant to link up this page for reference: https://codex.wordpress.org/Data_Validation
•	Broken Widget TItles: All of your custom widgets have broken widget titles because they are outputting the title something like this:
o	echo '<h4 class="st-widget-heading">' . $title . '</h4>';
o	Instead, that should look like:
o	echo $args['before_title'] . $title . $args['after_title'];
Overwritting Core Widgets: When creating custom widgets, you need to prefix their names. Otherwise, it overwrites core widgets, such as your archives widget:
parent::__construct('archives', __('Simontaxi Archives', 'simontaxi'), $widget_ops);
Instead of archives, it should be simon-archives.
Also, why are you creating custom widgets that are essentially the same as the core widgets (e.g., Archives, Categories, Text)? I'm not seeing what the benefit is here.
•	Missing Internationalization: Make sure to internationalize all text strings so that they can be translated.
•	Need to run http://validator.w3.org for HTML validation
•	Avoid using custom menu as much as possible
•	Avoid using image resize using external functions
