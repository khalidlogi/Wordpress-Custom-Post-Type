# Wordpress-Custom-Post-Type


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
