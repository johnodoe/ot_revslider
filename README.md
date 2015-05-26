# ot_revslider
Revolution slider metabox for option tree plugin (select field)


This is an addition to the default example of meta_boxex.php included in Option Tree Plugin:
https://wordpress.org/plugins/option-tree/

The addition is in the first part of the function where i create an array of all the revolution slider created in your theme.

    $array_choices      = array();
    if(shortcode_exists("rev_slider"))  { 
    $new_slider       = new RevSlider();
    $tot_revsliders   = $new_slider->getArrSliders();
    foreach ( $tot_revsliders as $rev_single ) {
         $alias   = $rev_single->getAlias();
         $title   = $rev_single->getTitle();
         array_push($array_choices, 
                    array('value' => $alias,
                          'label' =>$title,
                          'src'   =>''));
    }
    
Then i add the array to $my_meta_box array

      $my_meta_box = array(
      // original code bla bla bla
      // addition:
      array(
        'id'          => 'slider_select',
        'label'       => __( 'Revolution Slider', 'option-tree-theme' ),
        'desc'        => __( 'Choose one of the revolution slider created.', 'option-tree-theme' ),
        'type'        => 'select',
        'choices'     => $array_choices
      ),
       // original code bla bla bla
      );
      if ( function_exists( 'ot_register_meta_box' ) )
      ot_register_meta_box( $my_meta_box );
  
  
  
