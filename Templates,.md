tell WordPress which is your single CPT template in your plugin

 
 ```php
 /custom template 
    add_filter('template_include', array($this,'load_car_template'), 99);


  }

  function load_car_template($template) {
    if ( is_singular('car') ) {
        $template = plugin_dir_path(__FILE__) . '/single-car.php';
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
