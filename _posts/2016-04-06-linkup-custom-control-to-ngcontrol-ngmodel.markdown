---
layout: post
title:  "Angular 2: Connect your custom control to ngModel with Control Value Accessor."
description: "How to expose your component data to forms and bindings... "
date:   2016-04-06 16:10:21 -0100
categories: angular2 angular component ngModel ControlValueAccessor, NG_VALUE_ACCESSOR
---
***UPDATE** 2016/07-27:Now supports Angular v2.0.0-RC4 with the new forms API*

So you are starting to flex your new **Angular 2** muscles and have built the mother of all custom form controls. I
mean that thing can do everything except make coffee... And then the moment comes to extract and use it as a separate
component in your application.

You plug it into your HTML form with **ngModel** and a **name**, thinking your work is done and as your browser refreshes you
start seeing all sorts of errors appearing on the console.

As it turns out, your journey is far from over and today we will take a look at what **Angular2** expects from you if
you want to build components that can talk to **ngModel**.

**TL;DR: Here's the code**

For the example we will use a basic **input** component. You may argue that this component could easily by replaced by 
simply using the native **HTML input** element, and you would be right!

But we are trying to clearly show how to expose the component to the required interfaces and, to avoid making the example
overly complex, we will be sticking to this example. Once you understand how this works you can easily build on it to
make more complex controls as well. We will also not be looking at **a11y** in this post, also for simplicity.
But be aware that there is a lot of hidden work to be done if you want your controls to work well with **assistive technologies**.

So without further ado, here is our component:
{% highlight javascript %}
import { Component, forwardRef } from '@angular/core';
import { NG_VALUE_ACCESSOR, ControlValueAccessor } from '@angular/forms';

const noop = () => {
};

export const CUSTOM_INPUT_CONTROL_VALUE_ACCESSOR: any = {
    provide: NG_VALUE_ACCESSOR,
    useExisting: forwardRef(() => CustomInputComponent),
    multi: true
};

@Component({
    selector: 'custom-input',
    template: `<div class="form-group">
                    <label><ng-content></ng-content>
                        <input [(ngModel)]="value"
                                class="form-control"
                                (blur)="onBlur()" >
                    </label>
                </div>`,
    providers: [CUSTOM_INPUT_CONTROL_VALUE_ACCESSOR]
})
export class CustomInputComponent implements ControlValueAccessor {

    //The internal data model
    private innerValue: any = '';

    //Placeholders for the callbacks which are later providesd
    //by the Control Value Accessor
    private onTouchedCallback: () => void = noop;
    private onChangeCallback: (_: any) => void = noop;

    //get accessor
    get value(): any {
        return this.innerValue;
    };

    //set accessor including call the onchange callback
    set value(v: any) {
        if (v !== this.innerValue) {
            this.innerValue = v;
            this.onChangeCallback(v);
        }
    }

    //Set touched on blur
    onBlur() {
        this.onTouchedCallback();
    }

    //From ControlValueAccessor interface
    writeValue(value: any) {
        if (value !== this.innerValue) {
            this.innerValue = value;
        }
    }

    //From ControlValueAccessor interface
    registerOnChange(fn: any) {
        this.onChangeCallback = fn;
    }

    //From ControlValueAccessor interface
    registerOnTouched(fn: any) {
        this.onTouchedCallback = fn;
    }

}
{% endhighlight %}

We are then able to use this custom control as follows:
{% highlight html %}
 <form>
  
    <custom-input name="someValue"
                  [(ngModel)]="dataModel">
          Enter data:
    </custom-input>
    
  </form>
{% endhighlight %}

And here it is in action:

{::nomarkdown}
<iframe style="width: 100%; height: 350px" src="https://embed.plnkr.co/nqKUSPWb6w5QXr8a0wEu/?show=preview" frameborder="0" allowfullscren="allowfullscren"></iframe>
{:/}

**What did I just see, man? My eyes are bleeding!**

Don't panic! We will have a brief look at what just happened. But first it is perhaps important to state the following:

1. By using native **HTML** form elements in your code, you are avoiding having to write this code. Always consider 
using them first.
2. For the cases where you do need more power and want to create your own custom form control, **Angular 2** gives you all
you need to make it work!

So let us dive into the code...

**Bootstrap: Getting things started**

The code in this article uses the **new forms API** inside Angular 2 and will not work with the deprecated forms. In order to
use it you will need to activate it during your application bootstrap phase:

{% highlight javascript %}
import { bootstrap } from '@angular/platform-browser-dynamic';
import { disableDeprecatedForms, provideForms } from '@angular/forms';

bootstrap(App, [
  disableDeprecatedForms(),
  provideForms()
  ])
  .catch(err => console.error(err));
{% endhighlight %}

**NG_VALUE_ACCESSOR and the multi-provider: The glue**

As you know, we can register multi-providers in **Angular 2**. In short, it is possible to extend existing providers to
avoid duplicate providers from clashing. And for this communication to work we need to tell the **NG_VALUE_ACCESSOR** token
inside **Angular 2** that our class exists and has got something to say to the data bindings.

That we do with:
{% highlight javascript %}
export const CUSTOM_INPUT_CONTROL_VALUE_ACCESSOR: any = {
    provide: NG_VALUE_ACCESSOR,
    useExisting: forwardRef(() => CustomInputComponent),
    multi: true
};
{% endhighlight %}

Here we are telling this token about our component class. Important is the use of **forwardRef**. This is needed as our
class will not be defined yet when the provider is registered and we need to tell the **Provider constructor** about
it so it can wait for the class to be defined.

And once we have created this provider we need to tell our component to use it:
{% highlight javascript %}
    providers: [CUSTOM_INPUT_CONTROL_VALUE_ACCESSOR]
{% endhighlight %}

Now **Angular 2** knows about our form control component class, but we are not done yet.

**Implementing ControlValueAccessor: The machinery**

We also need to do the necessary work to manage the data and events inside our new component. And for this we need to 
implement the **ControlValueAccessor** interface that **Angular 2** gives us.

Let us implement this interface and hook it into our data model.

{% highlight javascript %}
    //The internal data model
    private innerValue: any = '';

    //Placeholders for the callbacks which are later provided
    //by the Control Value Accessor
    private onTouchedCallback: () => void = noop;
    private onChangeCallback: (_: any) => void = noop;

    //get accessor
    get value(): any {
        return this.innerValue;
    };

    //set accessor including call the onchange callback
    set value(v: any) {
        if (v !== this.innerValue) {
            this.innerValue = v;
            this.onChangeCallback(v);
        }
    }

    //Set touched on blur
    onBlur() {
        this.onTouchedCallback();
    }

    //From ControlValueAccessor interface
    writeValue(value: any) {
        if (value !== this.innerValue) {
            this.innerValue = value;
        }
    }

    //From ControlValueAccessor interface
    registerOnChange(fn: any) {
        this.onChangeCallback = fn;
    }

    //From ControlValueAccessor interface
    registerOnTouched(fn: any) {
        this.onTouchedCallback = fn;
    }
{% endhighlight %}

Let us first focus on the last three functions. These are functions we have to implement from the **ControlValueAccessor**
interface and these are the functions we need to use internally to communicate with the outside world.

The **writeValue** function allows you to update your internal model with incoming values, for example if you use
**ngModel** to bind your control to data.

The **registerOnChange** accepts a callback function which you can call when changes happen so that you can notify the outside
world that the data model has changed. Note that you call it with the changed data model value.

The **registerOnTouched** function accepts a callback function which you can call when you want to set your control to
**touched**. This is then managed by **Angular 2** by adding the correct touched state and classes to the actual
element tag in the **DOM**.

**NOTE**: Both these functions are later provided by **Angular 2** itself. But we need to register dummy functions
to be able able code and transpile it without errors.

The rest of the code are all internal component stuff! Providing function placeholders for the callbacks before they are
registered, a getter and setter for the data and a function to capture the blur event of the internal input to mark 
the entire component as touched. No rocket science there.

And there you have it! Now you can fully integrate your shiny new control with directives like **ngControl** and **ngModel**! 

Go forth and conquer!

If you want to know more about how to build extremely powerful form controls in **Angular 2**, the
<a href="https://github.com/angular/material2" target="_blank">Angular Material 2</a> repository is a veritable
treasure trove of information on the subject. If you are willing to dive into the code.

