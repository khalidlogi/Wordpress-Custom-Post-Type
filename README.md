https://themefoundation.com/wordpress-meta-boxes-guide/

# Wordpress-Custom-Post-Type

## meta box input fields
- Create a saparate file for html content and include it:
```php 
  public function kh_custom_car_content( $post ) {
    require_once plugin_dir_path(__FILE__).'form.php';
```
## Save the meta box form input
```php
/**
 * Saves the custom meta input
 */
function prfx_meta_save( $post_id ) {
 
    // Make sure that the nonce is valid and this isn’t an autosave.
    $is_autosave = wp_is_post_autosave( $post_id );
    $is_revision = wp_is_post_revision( $post_id );
    $is_valid_nonce = ( isset( $_POST[ 'prfx_nonce' ] ) && wp_verify_nonce( $_POST[ 'prfx_nonce' ], basename( __FILE__ ) ) ) ? 'true' : 'false';
 
    // Exits script depending on save status
    if ( $is_autosave || $is_revision || !$is_valid_nonce ) {
        return;
    }
 
    // Checks for input and sanitizes/saves if needed
    if( isset( $_POST[ 'meta-text' ] ) ) {
        update_post_meta( $post_id, 'meta-text', sanitize_text_field( $_POST[ 'meta-text' ] ) );
    }
 
}
add_action( 'save_post', 'prfx_meta_save' );
```

## Using saved meta data
```<?php
 
    // Retrieves the stored value from the database
    $meta_value = get_post_meta( get_the_ID(), 'meta-text', true );
    // single= true (Optional) This determines whether the value is returned as a string or an array
    // Checks and displays the retrieved value
    if( !empty( $meta_value ) ) {
        echo $meta_value;
    }
 
?>```


## Style Fields



# Custom taxonomie
```php
<?php

// Register Custom Taxonomy
function custom_taxonomy_car_brands() {

	$labels = array(
		'name'                       => _x( 'Car Brands', 'Taxonomy General Name', 'text_domain' ),
		'singular_name'              => _x( 'Car Brand', 'Taxonomy Singular Name', 'text_domain' ),
		'menu_name'                  => __( 'Car Brands', 'text_domain' ),
		'all_items'                  => __( 'All Car Brands', 'text_domain' ),
		'parent_item'                => __( 'Parent Car Brand', 'text_domain' ),
		'parent_item_colon'          => __( 'Parent Car Brand:', 'text_domain' ),
		'new_item_name'              => __( 'New Car Brand Name', 'text_domain' ),
		'add_new_item'               => __( 'Add New Car Brand', 'text_domain' ),
		'edit_item'                  => __( 'Edit Car Brand', 'text_domain' ),
		'update_item'                => __( 'Update Car Brand', 'text_domain' ),
		'view_item'                  => __( 'View Car Brand', 'text_domain' ),
		'separate_items_with_commas' => __( 'Separate car brands with commas', 'text_domain' ),
		'add_or_remove_items'        => __( 'Add or remove car brands', 'text_domain' ),
		'choose_from_most_used'      => __( 'Choose from the most used', 'text_domain' ),
		'popular_items'              => __( 'Popular Car Brands', 'text_domain' ),
		'search_items'               => __( 'Search Car Brands', 'text_domain' ),
		'not_found'                  => __( 'Not Found', 'text_domain' ),
		'no_terms'                   => __( 'No car brands', 'text_domain' ),
		'items_list'                 => __( 'Car Brands list', 'text_domain' ),
		'items_list_navigation'      => __( 'Car Brands list navigation', 'text_domain' ),
	);
	$args = array(
		'labels'                     => $labels,
		'hierarchical'               => true,
		'public'                     => true,
		'show_ui'                    => true,
		'show_admin_column'          => true,
		'show_in_nav_menus'          => true,
		'show_tagcloud'              => true,
	);
	register_taxonomy( 'car_brands', array( 'post' ), $args );

}
add_action( 'init', 'custom_taxonomy_car_brands', 0 );

?>
```
