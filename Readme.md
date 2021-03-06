# Pager Tabs Indicator

PagerTabIndicator started as a customisable android library that designed to work with the ViewPager component. After a few years I decided to revamp the project for my current needs so I decided to update it to also support `ViewPager2` and Jetpack navigation. I'm updating the project as my time allows it. PRs are always welcome.

#### Features
* Support dynamic adapter switch of the ViewPager / ViewPager2 / Jetpack Navigation
* Customizable tab indicator (bottom/top/background)
* Built in support for text/image/text+image tabs
* Support for custom views in tabs


#### Installation
Project has been moved on maven central

```gradle
implementation 'ro.holdone:pagertabindicator:2.0.0-alpha04'
```

Inside your layout insert a PagerTabIndicator element

```xml
    <com.hold1.pagertabsindicator.PagerTabsIndicator
        android:id="@+id/tabs_indicator"
        android:layout_width="0dp"
        android:layout_height="64dp"
        android:background="#ffffff"
        app:tab_indicator="bottom_bar"
        app:tab_lock_expanded="true" />
```

In your java code you should create a PagerAdapter for your ViewPager. After initialization, make sure you attach the ViewPager to PagerTabsIndicator component.

```java
        viewPager = findViewById(R.id.view_pager);
        tabsIndicator = findViewById(R.id.tabs_indicator);

        viewTextAdapter = new TextAdapter(getSupportFragmentManager());

        viewPager.setAdapter(viewTextAdapter);
        tabsIndicator.setViewPager(viewPager);
```


#### Supported Params

* `tab_padding` - set the left/right padding of a tab
* `tab_text_color` - set text color for default PagerAdapter implementation
* `tab_text_size` - set text size
* `tab_show_divider` - display tabs divider
* `tab_lock_expanded` - make tabs expand to their container size in equal sizes
* `tab_indicator` - specify tab indicator type: `top_bar`,`bottom_bar`,`background`
* `tab_indicator_resource` - use this param to specify a drawable resource that shold be used to draw the indicator if you want something more complext than a simple color. You can also specify an image as indicator.
* `tab_indicator_scale_type` - this param works in conjuction with `tab_indicator_resource`, and you can use it to specify if the indicator drawable should expand on the all available space, of it it should center inside indicator area to maintain a correct aspect. Possible values: `fitXY`, `centerInside`
* `tab_indicator_height` - define indicator height
* `tab_indicator_bg_height` - define indicator bar height
* `tab_indicator_margin` - indicator margin. with this param you can make the indicator float above indicator bar
* `tab_indicator_color` - indicator color. mutual exclusive with `tab_indicator_resource`
* `tab_indicator_bg_color` - indicator bar color
* `tab_divider_width` - divider width
* `tab_divider_margin` - divider vertical margin
* `tab_divider_color`
* `tab_divider_resource` - used to specify a drawable resource that should be used to be drawn as a divider
* `tab_show_bar_indicator` - param to show/hide the indicator bar. default set tot true
* `tab_elevation` - set tabElevation to the tab bar. In case of bottom bar placement, you should use a higher value to make the shadow more visible.
* `tab_disable_animation` - disable indicator animation while switching tabs
* `tab_highlight_text` - highlight the text color of the current tab for basic PagerAdapters. Defaults to indicator color.
* `tab_highlight_text_color` - set a custom color for highlighted tab text.

#### Changing params at runtime

In order to change the TabsIndicator parameters at run-time, you can call setters for all supported paramteres. To make things easier, setters can be chained. After setting the properties, it's mandatory to call `refresh()` in order to apply changes.

```java
 tabsIndicator.setShowDivider(false)
                        .setIndicatorBgHeight(0)
                        .setShowBarIndicator(false)
                        .setHeight(getResources().getDimensionPixelSize(R.dimen.tab_height_min))
                        .refresh();

```

#### TabViewProvider
