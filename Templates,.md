tell WordPress which is your single CPT template in your plugin

 
 ```php
 function load_single_ad_template( $template ) {

       

 global $post;

    

        if ( 'ads' === $post->post_type && locate_template( ['single-ads.php'] ) !== $template ) {

            /*

             * This is an 'ads' post

             * AND a 'single ad template' is not found on

             * theme or child theme directories, so load it

             * from our plugin directory from inside a /templates folder.

             */

            return YOUR_PLUGIN_DIR_PATH . 'templates/single-ads.php';

        }

    

        return $template;

    }

```
    
 ###  And for archive template use
   
 ```php  
 function load_archive_ads_template( $archive_template ) {

     global $post;

     if ( is_post_type_archive ( 'ads' ) ) {

          $archive_template = YOUR_PLUGIN_DIR_PATH . 'templates/archive-ads.php';

     }

     return $archive_template;

}

add_filter( 'archive_template', 'load_archive_ads_template', 10, 1 ) ; ```

    

    add_filter( 'single_template', 'load_single_ad_template', 10, 1 );
