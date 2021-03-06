# ot_revslider
Revolution slider metabox for option tree plugin (select field)

## Synopsis
This is an addition to the default example of demo-meta-boxes.php included in Option Tree Plugin:

https://github.com/valendesigns/option-tree/blob/master/assets/theme-mode/demo-meta-boxes.php

## Code
The addition is in the first part of the function custom_meta_boxes() where i create an array of all the revolution slider created in your theme.

    $array_choices      = array();
    if(shortcode_exists("rev_slider"))  { 
    $new_slider       = new RevSlider();
    $tot_revsliders   = $new_slider->getArrSliders();
    array_push($array_choices, 
                    array('value' => '',
                          'label' => __('Choose a Slider','theme-text-domain'),
                          'src'   =>''));  
    foreach ( $tot_revsliders as $rev_single ) {
         $alias   = $rev_single->getAlias();
         $title   = $rev_single->getTitle();
         array_push($array_choices, 
                    array('value' => $alias,
                          'label' =>$title,
                          'src'   =>''));
    }
    
Then i add the array to $my_meta_box array

      // addition to the 'fields' group:
      array(
        'id'          => 'slider_select',
        'label'       => __( 'Revolution Slider', 'theme-text-domain' ),
        'desc'        => __( 'Choose one of the revolution slider created.', 'theme-text-domain' ),
        'type'        => 'select',
        'choices'     => $array_choices
      ),
      // rest of the settings
      
## Installation
Just replace the original demo-meta-box.php with this one, or copy only the two parts above. You'll find the new element in your page/post metabox

![Alt text](http://i.imgur.com/UDSe5vm.jpg "Screenshot")

In order to print the selected metabox revolution slider in your theme use:
      
      $my_slider        = get_post_meta($post->ID, 'slider_select', true); 
      if ( ( function_exists("putRevSlider") ) && ( !empty($my_slider) ) ) { 
        putRevSlider  ( $my_slider ); 
        // or you can user standard do_shortcode('[rev_slider ' . $my_slider. ']');
      };
