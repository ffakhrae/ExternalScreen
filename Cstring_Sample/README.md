# CString Sample

## Source:

[developer.blackberry.com](http://developer.blackberry.com/playbook/native/reference/com.qnx.doc.screen.lib_ref/topic/cscreen_displays_complete_sample.html)


## Presentation on YouTube:

[Native API Deep Dive: Bluetooth and HDMI](http://youtu.be/66-EsgyibsQ)


## Usage:

#### Library:
Everything you'll need is in screen.h:

``` c++
#include <screen/screen.h>
```

#### Getting a Screen Context:

``` c++
screen_create_context(&screen_ctx, SCREEN_APPLICATION_CONTEXT);
```

#### Determining the Number of Screens:

``` c++
screen_get_context_property_iv(screen_ctx, SCREEN_PROPERTY_DISPLAY_COUNT, &ndisplays);
```

#### Getting References to All of the Displays:

``` c++
screen_get_context_property_pv(screen_ctx, SCREEN_PROPERTY_DISPLAYS, (void **)screen_dpy);
```

#### Querying a Display to See If It Is Attached:

``` c++
screen_get_display_property_iv(screen_dpy[i], SCREEN_PROPERTY_ATTACHED, &active);
```

#### Creating a Window

``` c++
screen_create_window(&screen_win, screen_ctx);
```

#### Assigning the Window to the Desired Display:

``` c++
screen_set_window_property_pv(screen_win, SCREEN_PROPERTY_DISPLAY, (void **)&screen_dpy[idx]);
```

#### Finding the Size of the Display:

``` c++
screen_get_display_property_iv(screen_dpy[idx], SCREEN_PROPERTY_SIZE, rect+2);
```

#### Setting the Size of the Window:

``` c++
screen_set_window_property_iv(screen_win, SCREEN_PROPERTY_BUFFER_SIZE, rect+2);
```

#### Creating Buffers for Rendering:

``` c++
screen_create_window_buffers(screen_win, 2);
```

#### Rendering Contents:

Lots of options:
1. Blit and Pixmap operations
2. OpenGL
3. ...

#### Showing the Content

``` c++
screen_post_window(screen_win, screen_buf[0], 1, rect, 0);
```

The sample code also detects, and reacts to HDMI disconnection.

The external screen continues to display the content, even if the user switches to a different app/view on their device.


## What the Code Doesn't Cover:

HDCP - High bandwidth Digital Content Protection. However, *it is supported on BlackBerry 10 platform*. In order to achieve this, two properties must be set: 

1. Protecting a buffer
2. Enabling content protection
