---
layout: post
title:  "NexusDialog: Dynamic Form Builder for Android"
date:   2013-12-12 00:00:00 -0800
---
Writing repetitive UI code can be tedious sometimes. Whenever you observe a repetitive pattern in how code is built, it's usually a good sign that it can be refactored out to its own module, or even its own library. It's also likely that other developers will run into similar needs. This is exactly why I just released an open-source project for Android I called [NexusDialog](https://github.com/dkharrat/NexusDialog). It provides an easy and simple way to build a form-based UI. This was motivated by a recent app I developed that required displaying many form-based screens. As most developers do, I initially looked around to see if there were existing libraries that provided such functionality. On iOS, there are plenty, so I expected to similarly find many options for Android. Surprisingly, I was not able to find an active one. This is perhaps because UI design is significantly easier and more flexible on Android than iOS. Nevertheless, there is merit to having a framework that simplifies the development of a certain class of UIs, like forms. Thus, NexusDialog was born.

Here's a simple example of how to create the following form:

![NexusDialog Form Example](http://dkharrat.github.io/NexusDialog/images/screenshot01.png)

Here's the code to generate the form:

{% highlight java %}
import java.util.Arrays;
import com.github.dkharrat.nexusdialog.FormActivity;
import com.github.dkharrat.nexusdialog.controllers.*;

public class SimpleExample extends FormActivity {

    @Override protected void initForm() {
        FormSectionController section = new FormSectionController(this, "Personal Info");
        section.addElement(new EditTextController(this, "firstName", "First name"));
        section.addElement(new EditTextController(this, "lastName", "Last name"));
        section.addElement(new SelectionController(this, "gender", "Gender", true, "Select", Arrays.asList("Male", "Female"), true));

        addSection(section);
        setTitle("Simple Example");
    }
}
{% endhighlight %}

It doesn't get any simpler than that. Read more details about the library at [https://github.com/dkharrat/NexusDialog](https://github.com/dkharrat/NexusDialog). Feedback, suggestions, and contributions are very welcome!

