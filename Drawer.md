> Thinking

```

```

> Memory

#### DrawerLayout

```
implementation 'androidx.drawerlayout:drawerlayout:'
implementation 'com.android.support:drawerlayout:'

ViewGroup
    DrawerLayout

DrawerLayout.SimpleDrawerListener <-- DrawerLayout.DrawerListener

DrawerLayout
    addDrawerListener DrawerLayout.DrawerListener
        onDrawerSlide
        onDrawerOpened
        onDrawerClosed
        onDrawerStateChanged
    removeDrawerListener
    closeDrawer
        GravityCompat.START
    closeDrawers

```

### CSS