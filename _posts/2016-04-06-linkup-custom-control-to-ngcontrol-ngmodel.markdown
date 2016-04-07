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
import {Component, Provider, forwardRef} from "angular2/core";
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
          <input class="form-control" 
                 [(ngModel)]="value" 
                 (blur)="onTouched()">
        </label>
      </div>
  `,
  providers: [CUSTOM_INPUT_CONTROL_VALUE_ACCESSOR]
})
export class CustomInput implements ControlValueAccessor{

   private _value: any = '';
    
   private _onTouchedCallback: (_: any) => void = noop;
     
   private _onChangeCallback: (_: any) => void = noop;
    
   get value(): any { return this._value; };
    
   set value(v: any) {
     if (v !== this._value) {
       this._value = v;
       this._onChangeCallback(v);
     }
   }
      
   onTouched(){
     this._onTouchedCallback();
   }
   
   //From ControlValueAccessor interface
   writeValue(value: any) {
     this._value = value;
   }
   
   //From ControlValueAccessor interface 
   registerOnChange(fn: any) {
     this._onChangeCallback = fn;
   }
    
   //From ControlValueAccessor interface 
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
<iframe style="width: 100%; height: 180px" src="https://embed.plnkr.co/nqKUSPWb6w5QXr8a0wEu/" frameborder="0" allowfullscren="allowfullscren"></iframe>
{:/}

**What did I just see, man? My eyes are bleeding!**

Don't panic! We will have a brief look at what just happened. But first it is perhaps interesting to state the following:

1. By using native `HTML` form elements in your code, you are avoiding having to write this code. Always consider this
first.
2. For the cases where you need more power and want to create your own custom form control, **Angular 2** gives you all
you need to make it work!

So let us dive into the code...

**NG_VALUE_ACCESSOR and multi-provider: The glue**

As you know, we can register multi-providers in **Angular 2**. In short, it is possible to extend existing providers to
avoid the duplicate provider issues. And for the communication to work we need to tell the **NG_VALUE-ACCESSOR** token
inside **Angular 2** that our class exists and has got something to say to the data bindings.

That we do with:
{% highlight javascript %}
const CUSTOM_INPUT_CONTROL_VALUE_ACCESSOR = new Provider(
  NG_VALUE_ACCESSOR, {
    useExisting: forwardRef(() => CustomInput),
    multi: true
  });
{% endhighlight %}

Here we are telling this token about our component class. Important is the use of **forwardRef**. This is needed as our
class will not be defined yet when the provider is registered and we need to tell the **Provider constructor** about
it so it can wait for the class to be defined.

And once we have created this provider we need to tell our component to use it:
{% highlight javascript %}
providers: [CUSTOM_INPUT_CONTROL_VALUE_ACCESSOR]
{% endhighlight %}

Now **Angular 2** know about our class, but we are not done yet.

**Implementing ControlValueAccessor: The machinery**

We also need to do the necessary work to manage the data and events inside our new component. And for this we need to 
implement the **ControlValueAccessor** interface that **Angular 2** gives us.

Let us implement this interface and hook it into our data model.

{% highlight javascript %}
 private _value: any = '';
  
 private _onTouchedCallback: (_: any) => void = noop;
   
 private _onChangeCallback: (_: any) => void = noop;
  
 get value(): any { return this._value; };
  
 set value(v: any) {
   if (v !== this._value) {
     this._value = v;
     this._onChangeCallback(v);
   }
 }
 
 onTouched(){
       this._onTouchedCallback();
 }
 
 //From ControlValueAccessor interface 
 writeValue(value: any) {
   this._value = value;
 }
 
 //From ControlValueAccessor interface
 registerOnChange(fn: any) {
   this._onChangeCallback = fn;
 }
  
 //From ControlValueAccessor interface 
 registerOnTouched(fn: any) {
   this._onTouchedCallback = fn;
 }
{% endhighlight %}

Let us first focus on the last three functions. These are functions we have to implement due to the **ControlValueAccessor**
interface and these are the functions we need to use internally to communicate with the outside world.

The **writeValue** function allows you to update your internal model with incoming values, for example if you use
**ngModel** to bind your control to data.

The **registerOnChange** function provides you with a function you can call when changes happen to notify the outside 
world that the data model has changed. Note that you call it with the changed data model value.

The **registerOnTouched** function provides you with a function you can call when you want to set your control to 
**touched**. This is then reflected by **Angular 2** by adding the correct touched state and classes to your control.

