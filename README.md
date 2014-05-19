$plugin_dir = basename(dirname(__FILE__));
load_plugin_textdomain( 'simplesplash', null, $plugin_dir );

class simplesplash {

	/**
	 * Constructor
	 */
	function simplesplash() {
		
		// Check the relation between the referer and WordPress-Home-Url.
		// Also the requested URL should be the WordPress-Startpage.
		
		if( (strpos($_SERVER['HTTP_REFERER'], get_bloginfo('home')) === false) && 
		        get_bloginfo('wpurl').'/' == 'http://'.$_SERVER['HTTP_HOST'].$_SERVER['REQUEST_URI'])
		add_action('send_headers', array('simplesplash', 'display_splash'));
			
	}


	/**
	 * Display the splash screen if its enabled
	 */
	function display_splash() {
		
		$filename = 'splash.php';
		$themepath = get_theme_root().'/'.get_template();
		
		if(is_file($themepath.'/'.$filename)) {
		  @include($themepath.'/'.$filename);

		}else {
		  @include(dirname(__FILE__).'/'.$filename);

		}
		exit();
	}
}


$splash = new simplesplash;
?>
