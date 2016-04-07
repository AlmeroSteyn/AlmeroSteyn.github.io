---
layout: post
title:  "Angular 2: Connect your custom control to ngModel and ngControl with ControlValueAccessor."
description: "How to expose your component data to forms and bindings... "
date:   2016-04-06 16:10:21 -0100
categories: angular2 angular component ngModel ngControl ControlValueAccessor, NG_VALUE_ACCESSOR
---

So you are starting to flex your new **Angular 2** muscles and have built the mother of all custom form controls. I
mean that thing can do everything except make coffee when the moment comes to extract and use it as a separate
component in your application.

You plug it into your HTML form, thinking your work is done and as your browser refreshes your start seeing all sorts of 
errors appear on the console. Attaching it to **ngModel** produces similar errors. 

As it turns out, your journey is far from over and today we will take a look at what **Angular2** expects from you if
you want to build components that can talk to directives like **ngControl** and **ngModel**.

**TL;DR: Here's the code**

For the example we will use a basic **input** component. You may argue that this component could be easily replaced by 
simply using the native **HTML input** element, and you would be right!

But we are trying to clearly see how to expose the component to the required interfaces and to avoid making the example
overly complex we will be using this example. We will also not be looking at `a11y` in this post. But be aware that 
when writing custom controls you have to ensure that they are accessible.

So without further ado, here is our component:
{% highlight javascript %}
import {Component, Provider, forwardRef, Input} from "angular2/core";
import {ControlValueAccessor, NG_VALUE_ACCESSOR} from "angular2/common";

const noop = () => {};

const CUSTOM_INPUT_CONTROL_VALUE_ACCESSOR = new Provider(
  NG_VALUE_ACCESSOR, {
    useExisting: forwardRef(() => CustomInput),
    multi: true
  });

@Component({
  selector: 'custom-input',
  template: `
      <div class="form-group">
        <label><ng-content></ng-content>
          <input class="form-control" [(ngModel)]="value">
        </label>
      </div>
  `,
  providers: [CUSTOM_INPUT_CONTROL_VALUE_ACCESSOR]
})
export class CustomInput implements ControlValueAccessor{

  private _value: any = '';

  private _onTouchedCallback: () => void = noop;
 
  private _onChangeCallback: (_: any) => void = noop;

  get value(): any { return this._value; };

  @Input() set value(v: any) {
    if (v !== this._value) {
      this._value = v;
      this._onChangeCallback(v);
    }
  }

  writeValue(value: any) {
    this._value = value;
  }

  registerOnChange(fn: any) {
    this._onChangeCallback = fn;
  }

  registerOnTouched(fn: any) {
    this._onTouchedCallback = fn;
  }

}
{% endhighlight %}

We are then able to use this custom control as follows:
{% highlight html %}
 <form>
  
    <custom-input ngControl="someValue" 
                  [(ngModel)]="dataModel">
          Enter data:
    </custom-input>
    
  </form>
{% endhighlight %}

And that gives is this working example:

{::nomarkdown}
<iframe style="width: 100%; height: 300px" src="https://embed.plnkr.co/nqKUSPWb6w5QXr8a0wEu/" frameborder="0" allowfullscren="allowfullscren"></iframe>
{:/}