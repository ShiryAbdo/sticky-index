# Sticky Index Library
This repository contains the source code for a component that implements the " Sticky Letter Index" such as it is presented in the Android Contact App from Android Lollipop (API 21) on. Please feel free to use it as well as enhance it

Current Stable Version: [ ![Download](https://api.bintray.com/packages/edsilfer/maven/sticky-index/images/download.svg) ](https://bintray.com/edsilfer/maven/sticky-index/_latestVersion)
---

**Dont't forget to read the P.S.1 at the [how to use](#how-to-use) section**

# Table of Contents
* [Introduction](#intro)
* [Showcase](#showcase)
* [How to use](#how-to-use)
* [TODO List](#to-do)
* [Team Members](#team-members)
* [License](#license)

<a name="intro"></a>

# Introduction
You've just got a smartphone with Android API 21+, took a look in the "Contact" app and got excited by those sticky letters that scrolls with the list in a beautiful manner? Well, this library intend to provide you with the same component.

<a name="showcase"></a>

# Showcase
Check below the library in a Contact app context:

![Demo](https://github.com/edsilfer/sticky-index/blob/master/art/horizontal-demo.gif)   

![Demo](https://github.com/edsilfer/sticky-index/blob/master/art/vertical-demo.gif)

<a name="how-to-use"></a>

# How to use
You can compile the library from JCenter through:

```
repositories {
    repositories {
        jcenter()
    }
}

dependencies {
    compile 'br.com.edsilfer:stickyindex:1.0.0'
}

```

Or Maven through:

```
repositories {
    maven {
        url "https://jitpack.io"
    }
}

dependencies {
    compile 'com.github.edsilfer:sticky-index:1.2.1'
}

```

Then, add this component to your XML layout (usualy, right after the RecyclerView):

```xml
<br.com.stickyindex.StickyIndex
        android:id="@+id/sticky_index_container"
        android:layout_width="wrap_content"
        android:layout_height="match_parent" />
```

You can customizing the stick-index with the following arguments:

 * ```xml android:textSize```: changes the index list text size;
 * ```xml android:textStyle```: changes the index list text style;
 * ```xml android:textColor```: changes the index list test color;
 * ```xml app:rowHeight```: changes the index list row height;
 * ```xml app:stickyWidth```: changes the LinearLayout width that wrappers the text - which, by its turn, it is centralized inside it. Use this atribute to control the distance of the index list from the corner of its parent.

**The last attribute ```xml android:rowHeight``` is mandatory. Understand that the sticky-index consists of another RecyclerView which needs to match the reference one (in terms of ScrollListener and rowHeight). Having different rowHeights WILL lead to layout failures.**

By last, initialize it in the container main class. Also add the dataSet (a char array that will contain the indexes). This array must have the same size as the main list, with each row corresponding to the element that it will be associated). Finally, set the corresponding RecyclerVIew that will control the scroll movement:

```java
// Creates index viewer
        StickyIndex indexContainer = (StickyIndex) this.findViewById(R.id.sticky_index_container);
        // INSERT CHAR LIST
        indexContainer.setDataSet(getIndexList(myContacts));
        indexContainer.setReferenceList(indexList);
```

**P.S.1: Please, don't forget to set the android:rowHeight attribute to match your RecyclerView row height (if you don't set app:stickyWidth default value will be 60dp)**

P.S.2.: As said above, **the sticky-index is another RecyclerView that needs to match the reference one** (which you should provide). In order to sync the scroll action of both, a **OnScrollListener** of your given RecyclerView is created inside the library. If you need to receive scroll updates, please, create a class that implements the interface **Subscriber** and register it inside **StickyIndex** class through the method ```subscribeForScrollListener()```. The ```update``` method is equivalent to the ```onScroll()``` method of the **OnScrollView**. If the action that you'll develop inside your update need to affect the scroll of the sticky-index list, the method ```getHeader()``` is provided through the class **StickyIndex**. The returned instance has a call for the method ```update``` (Refer to the demo app code for further details, there the described approach is implemented to make the sticky-index compatible with the fastscroller class)

<a name="to-do"></a>

# TODO List
* Upload library into JCenter/Maven;
* ~~Make index list background transparent in order to correct the detail when user pushes down the list in the top or bottom of it;~~
* ~~Add attributes gather from the XML in order to set the row height, text size, style and color;~~
* ~~Fix flying action (sometimes when scrolling too fast the sticky letter might get invisible);~~
* ~~Make it compatible with layout orientation horizontal;~~
* Improve Search Dialog from demo app;
* ~~Rename app project to demo;~~
* ~~Create separeted branch for art;~~

<a name="team-members"></a>

# Team Members
* "Fernandes S. Edgar" <fernandes.s.edgar@gmail.com>

<a name="license"></a>

# License
Copyright 2015 Edgar da Silva Fernandes

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
