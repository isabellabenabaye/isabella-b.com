+++
# A Projects section created with the Portfolio widget.
widget = "today-i-learned"  # See https://sourcethemes.com/academic/docs/page-builder/
headless = true  # This file represents a page section.
active = true  # Activate this widget? true/false
weight = 20  # Order that this section will appear.

title = "today i learned"
subtitle = "A collection of mini-posts of the things I learn"

[content]
  # Page type to display. E.g. project.
  page_type = "today-i-learned"
  
  # Filter toolbar (optional).
  # Add or remove as many filters (`[[content.filter_button]]` instances) as you like.
  # To show all items, set `tag` to "*".
  # To filter by a specific tag, set `tag` to an existing tag name.
  # To remove toolbar, delete/comment all instances of `[[content.filter_button]]` below.
  
  # Default filter index (e.g. 0 corresponds to the first `[[filter_button]]` instance below).
  filter_default = 0
  
  [[content.filter_button]]
    name = "All"
    tag = "*"
  
#  [[content.filter_button]]
#    name = "Visualizations"
#    tag = "Data Visualizations"
  
#  [[content.filter_button]]
#    name = "Tidy Tuesday"
#    tag = "Tidy Tuesday"     

[design]
  # Choose how many columns the section has. Valid values: 1 or 2.
  columns = "1"

  # Toggle between the various page layout types.
  #   1 = List
  #   2 = Compact
  #   3 = Card
  #   5 = Showcase
  view = 3

[design.background]
  # Apply a background color, gradient, or image.
  #   Uncomment (by removing `#`) an option to apply it.
  #   Choose a light or dark text color by setting `text_color_light`.
  #   Any HTML color name or Hex value is valid.
  
  # Background color.
  # color = "navy"

  # Background image.
  # image = "background.jpg"  # Name of image in `static/img/`.
  # image_darken = 0.6  # Darken the image? Range 0-1 where 0 is transparent and 1 is opaque.

  # Text color (true=light or false=dark).
  # text_color_light = true  

  # Background gradient.
  gradient_start = "#F7F7F7"
  gradient_end = "#A5DDC5"
  
[advanced]
 # Custom CSS. 
 css_style = ""
 
 # CSS class.
 css_class = ""

 [design.spacing]
  # Customize the section spacing. Order is top, right, bottom, left.
  padding = ["2rem", "0", "4rem", "0"]
+++

