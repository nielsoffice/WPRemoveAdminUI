# WPRemoveAdminUI
Remove menu to toolbar WordPress backend by user role meta box and more

```PHP
// remove toolbar items
function shapeSpace_remove_toolbar_node($wp_admin_bar) {
	
    /*
     Begin remove to selected user role
    */
	$current_user   = wp_get_current_user();
	$role_name      = $current_user->roles[0];
	   
	$user 		    = wp_get_current_user();
	$allowed_roles  = array('admin', 'administrator');  // which role can use tool bar ? means show toolbar !

	
   if( !array_intersect($allowed_roles, $user->roles ) ) : 

	// replace 'updraft_admin_node' with your node id
	$wp_admin_bar->remove_node('tribe-events');
	$wp_admin_bar->remove_node('new-content');
	$wp_admin_bar->remove_node('comments');

   endif;

	
}
add_action('admin_bar_menu', 'shapeSpace_remove_toolbar_node', 999);

// remove toolbar items (alt technique)
function shapeSpace_remove_toolbar_menu() {
	
	global $wp_admin_bar;
	
	$current_user   = wp_get_current_user();
	$role_name      = $current_user->roles[0];
	   
	$user 		    = wp_get_current_user();
	$allowed_roles  = array('admin', 'administrator');

	
   if( !array_intersect($allowed_roles, $user->roles ) ) : 
	
	// replace 'updraft_admin_node' with your node id
	$wp_admin_bar->remove_menu('tribe-events');
	$wp_admin_bar->remove_menu('new-content');
	$wp_admin_bar->remove_menu('comments');

   endif;
	
}
add_action('wp_before_admin_bar_render', 'shapeSpace_remove_toolbar_menu', 999); 

/** 
 * Default WP function add remove_metabox
**/
add_action('admin_head','remove_meta_boxes', 999);
function remove_meta_boxes() 
{

  global $current_user; 
  global $role_name;
  global $user;
  global $allowed_roles;
	
 if( !array_intersect($allowed_roles, $user->roles ) || ! current_user_can( 'manage_options' ) ) : 

   remove_meta_box('et-post-format','post','normal');
   remove_meta_box('aioseo-settings','post','normal');
   remove_meta_box('postcustom','post','normal');
   remove_meta_box('lptw_recent_posts_options','post','normal');
   remove_meta_box('amember_sectionid','post','normal');
   remove_meta_box('amember_shortcodes_sectionid','post','normal');
   remove_meta_box('post-review-box','post','normal');
   remove_meta_box('extra-page-post-settings','post','normal');
   remove_meta_box('spp_isim_main_editor_dialog','post','normal');
	
 endif;

}

```

<br /> Reference: 
<br /> https://digwp.com/2016/06/remove-toolbar-items/

