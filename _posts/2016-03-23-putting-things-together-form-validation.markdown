---
layout: post
title:  "Angular2: Form validation salad."
description: "You know the basics, now see the power..."
date:   2016-03-23 16:10:21 -0100
categories: angular2 component form validation styles css content-projection transclude
---

One of the best things that ever happened to me in **AngularJS** was **ng-messages**. The projects I find myself on
are all very form intensive, and when **ng-messages** hit release it was, well, simply awesome. 

But I wanted more, I wanted a *transclude* directive that would wrap my input in some magical form-validation candy
without me having to write the boilerplate on every single form for every single form. And I did it. The *holy grail*
of form validation. 

If was pimped. No jokes. Adding custom validators in the HTML and controller code only, rendering the errors on the fly
and lots more.

So what better to try out in **Angulars** than to recreate one of the most complex **AngularJS** directives I ever wrote.

**SAY WHAT???!!**

In short, today we will be building an **Angular2** form validation component. And to see just how flexible it is,
we will be building the same component in three different ways. 

Before we come out the end of this blog post we will have used the following concepts in **Angular2** to see how they
fit into making a more complex functional component:

* Model forms
* Custom validators
* Contentchildren
* Displaying validation errors
* Content projection (transclusion)
* Component styles
* Change detection

We will also be using **Bootstrap** as styling framework. It can, of course, be translated to use any styling you prefer
to use.

And we are going to use all of that to build this:

Excited yet? 

**Pick your flavour**

* With content projection, ngDoCheck and contentchildren
* With content projection and component styling
* With content projection, ngOnChanges and full error template rendering

I do encourage you, brave traveler, to sample them all. 

**The base of our salad: Content projection and validation**

We already know how to create component in **Angular2** with form validation. So let us build one quickly.

Our component will consist of a form with one input as form element. The input will have three validations, two 
standard validations that **Angular2** gives you, and then one custom validation we built to check if the 
component input is divisible by 10. These validations are only a means to an end here, you can add any validations
you want.

Our component:
{% highlight javascript %}
@Component({
  selector: 'some-form',
  templateUrl: './some-form.component.html'
})
export class SomeForm implements OnInit {

  someFormHandle:ControlGroup;
  someNumber:AbstractControl;

  constructor(private formBuilder:FormBuilder) {
  }
  
  divisibleByTen(control:Control) {
      return parseInt(control.value) % 10 == 0 ? null : {
        divisibleByTen: true
      }
  }

  onSubmit(){
    //Some submit logic
  }
  
  ngOnInit():void {
    this.someFormHandle = this.formBuilder.group({
      'someNumber': ['', Validators.compose([Validators.required, 
                                             Validators.minLength(7), 
                                             this.divisibleByTen])]
    });

    this.someNumber = this.someFormHandle.find('someNumber');
  }
  
  
}
{% endhighlight %}

And our component template:
{% highlight html %}
<form [ngFormModel]="someFormHandle" 
      [(ngSubmit)="onSubmit()">

    <input class="form-control"
           type="text"
           [ngFormControl]="someNumber">

    <button class="btn btn-primary" 
            [disabled]="!someFormHandle.valid">
            Submit
    </button>
    
</form>
{% endhighlight %}

**Now add some orange juice for flavour: Content projection**

So now we have an input with some validation attached. But face it, going to a form with only empty inputs on it
will make even the most sane person reach for the chainsaw so it really, really needs a label.

**NOTE:** *a11y also really really thinks a form needs a label, by the way. Not providing well formed labels for your
will really impede some users from using your forms. This article will not focus very deeply on a11y to avoid making
an already complex matter even more so. But look out for some articles on this in future.*

We could do this in our component template:

{% highlight html %}
<label class="control-label">Some number
    <input class="form-control"
           type="text"
           [ngFormControl]="someNumber">
</label>
{% endhighlight %}

And this will work perfectly. **BUT** why would we want to write this for every single input if we are using something
as nice and shiny as **Angular2**? Well, you could argue that at this stage it is not a lot of **HTML** to write extra
and you would be perfectly right, but we will be extending our boilerplating a lot more before this is done. So let's 
use **Content Projection** to solve this. 

So we need another component that does this and we will be putting our label into the template:

{% highlight javascript %}
@Component({
  selector: 'extended-input',
  template: ` <label class="control-label">{% raw %}{{labelText}}{% endraw %}
                <ng-content></ng-content>
              </label>
            `
})
export class ExtendedInput {
  @Input()
  labelText:string = '';
}
{% endhighlight %}

By using the `<ng-content>` element, the content of your component will be projected into this slot of your **HTML**.

So let us use this!

{% highlight html %}
<extended-input [labelText]="'Some number'">
    <input class="form-control"
           type="text"
           [ngFormControl]="someNumber">
   
</extended-input>
{% endhighlight %}

**BAZINGA**, a label gets rendered around our input.

