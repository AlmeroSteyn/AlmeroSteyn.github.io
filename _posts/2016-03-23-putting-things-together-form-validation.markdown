---
layout: post
title:  "Angular2: Form validation salad."
description: "You know the basics, now see the power..."
date:   2016-03-23 16:10:21 -0100
categories: angular2 component form validation styles css content-projection transclude
---

>*The weary traveler moved up the mountainside. For weeks he had travelled the land of Anghu-LAHR, facing many trials,
>gathering many magical items. He felt the weight of them in his backpack as he approached the wise woman at the top.*
>
>*Laying down his enchanted items he saw what he had gained again. The Amulet of Component, the Sword of Validation,
>the Wind of Changedetection...*
>
>*"Well done, brave warrior", she said.*
>
>*"But what is next? What is their purpose?"*
>
>*She looked up at him. "To become a Champion of Angul-LAHR, you need to learn to wield their power together. By
>themselves these items are magical, only by putting them together will they become functional.*
>
>*He understood.*

Today, we will see how to put together some of the many bits that **Angular2** gives us, to construct a component that can decorate
any input with some cool form validation function. Not only that, but it will have the power of **ng-messages** from
**AngularJS** as well.

For those who have not used **ng-messages**, this is an **AngularJS 1.x** directive that makes the management of multiple
input field validation messages a breeze by ensuring that, at any time, a maximum of one message is shown.

So why don't we build a component that we can wrap any input in like this:
{% highlight html %}
<extended-input>
  <input class="i_am_just_a_normal_input_bound_to_something">
  <maybe-some-error-info></maybe-some-error-info>
</extended-input>
{% endhighlight %}

Which should produce this:
 
{::nomarkdown}
<figure>
    <img src="/css/images/2016-03-24-form-validation-zen/Component.jpg" alt="Form component with styled validation.">
</figure>
{:/}

And, while we are at it, why don't we see just how flexible **Angular2** is, and look at more than one way to construct 
this?

Before we are done, we will have used the following key concepts inside **Angular2**
* Model driven forms
* Form validation and custom validators
* Displaying validation errors
* Contentchildren decorator
* Content projection (Angular2's own transclusion)
* Component styling
* Change detection
* Lifecycle hooks

If you are not familiar with these, it may be a good idea to look at them first. The **Angular2** documentation contains
information about these points and a number of very good articles have been written on all of these topics.

We will use **Bootstrap CSS** as styling framework. However this can be replaced with your framework of choice.

**The three paths**

>*In front of him were three paths. He could choose one, but the words of the wise woman haunted him and he secretly knew
>that his journey could only ever become complete if he explores them all.*

We will look at there ways to get to the same result. All three options will use **Content Projection** as basis but will
differ in how the error messages are managed.

1. Using general change detection and communicating with the content children.
2. Using component styles.
3. Using component input change detection and an error definition object.

**Preparing the journey: part 1**

>*Being well prepared was crucial for his journey. He packed quick and light making sure that everything he needed
>was there.*

We need a basis to work from and already know how to create component in **Angular2** with form validation. 
So let us build one quickly.

Our component will consist of a form with one input as form element. This input will have a mix of standard and 
custom validations. 

Our component:
{% highlight javascript %}
@Component({
  selector: 'some-form',
  templateUrl: './some-form.component.html',
  directives: [FORM_DIRECTIVES]
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
           [ngFormControl]="someNumber">

    <button class="btn btn-primary" 
            [disabled]="!someFormHandle.valid">
            Submit
    </button>
    
</form>
{% endhighlight %}

We now have a component that one input. This input is required, wants an input of minimal length seven, and the number
value of the input should be divisible by ten.

**Preparing for the journey: part 2**

>*Having packed, he strapped on his armour. It was magical armour that shone with colour and power.*

So now we have an input with some validation attached. But face it, going to a form with only empty inputs on it
will make even the most sane person reach for the chainsaw so it really, really needs a label.

**NOTE:** *a11y also really really thinks a form needs a label, by the way. Not providing well formed labels for your
will really impede some users from using your forms. This article will not focus very deeply on a11y to avoid making
an already complex matter even more so. But look out for some articles on this in future.*

We could do this in our component template:

{% highlight html %}
<label class="control-label">Some number
    <input class="form-control"
           [ngFormControl]="someNumber">
</label>
{% endhighlight %}

And this will work perfectly. **BUT** why would we want to write this for every single input if we are using something
as nice and shiny as **Angular2**? Why don't we use **Content Projection** to solve this? Well, you could argue that, 
at this stage, it is not a lot of **HTML** to write extra and you would be perfectly right, so lets also add 
some *Bootstrap** goodness to style our input and highlight error situations!

For this we need another component: 

{% highlight javascript %}
@Component({
  selector: 'extended-input',
  template: `<div class="form-group"
                  [ngClass]="{'has-error':isError}"> 
                        <label class="control-label">{% raw %}{{labelText}}{% endraw %}
                            <ng-content></ng-content>
                        </label>
             </div>
            `,
  directives: [CORE_DIRECTIVES]
})
export class ExtendedInput {
  @Input()
  labelText:string = '';
  @Input()
  isError:boolean = false;
}
{% endhighlight %}

By using the `<ng-content>` element, the content of your component will be projected into this slot of your **HTML**.

So let us use this!

{% highlight html %}
<extended-input [labelText]="'Some number'"
                [isError]="!someNumber.valid">
    <input class="form-control"
           [ngFormControl]="someNumber">
   
</extended-input>
{% endhighlight %}

**BAZINGA!!!** Now we can decorate any input we want with a label and some magic!

**Salad zen: Reflecting on what we are about to do**

What I really love **ng-messages** in **AngularJS** is its ability to display only the first error message of 
a hierarchy of defined error messages. This saves just so much code and complex logic. 

So this is our real mission, fellow adventurer. Now that we have a component that decorates and input with a label and
styles to show the validation state, lets add some validation messages and only show a max of one message at any time.

Here our path splits in three. Which one will your choose? Or will you choose all three? 

**A salad of ContentChildren**

The basis of the solution we are about to implement is to make use of the **@ContentChildren** decorator of
**Angular2** to get access our error messages and progrmatically switch them on an off.

In order to do this we need to first create a component to put our errors in. And give it the functionality to
add or remove itself to the DOM. **HEY** we are trying to recreate **ng-messages** here!

And yes, we are going to use **Content Projection** in this component too!
{% highlight javascript %}
@Component({
  selector: 'input-error',
  template: `<span *ngIf="showErrorFlag" class="help-block">
               <ng-content></ng-content>
             </span>
             `,
  directives: [CORE_DIRECTIVES]
})
export class InputError {

  showErrorFlag:boolean = true;

  hideError():void {
    this.showErrorFlag = false;
  }

  showError():void {
    this.showErrorFlag = true;
  }

}
{% endhighlight %}

So now we can extent the **HTML** of our top level component as follows:
{% highlight html %}
<extended-input [labelText]="'Some number'"
                [isError]="!someNumber.valid">
    <input class="form-control"
           [ngFormControl]="someNumber">
    <input-errors>
        <input-error class="help-block" 
                     *ngIf="someNumber.hasError('required')">
            A number is required
        </nput-error>
        <input-error class="help-block" *
                     *ngIf="someNumber.hasError('divisibleByTen')">
            The number should be divisible by 10
        </input-error>
        <input-error class="help-block" 
                     *ngIf="someNumber.hasError('minlength')">
            The number should be at least 7 digits
        </input-error>
    </input-errors>
</extended-input>
{% endhighlight %}

Three important things to note here:

1. We are using our new `<input-error>` component and projecting the text into its template.
2. We have created an `<input-errors>` in the template. It simply acts as a placeholder. We could have used a div but 
for this example it is clearer.
3. We are using ***ngIf** to display only error messages for failed validations.

So now we still need to do two things in our decorator component. Firstly we need to project the error messages into
another `<ng-content>` slot, and we need remove all but the first displayed error.

And once again **Angular2** comes to our rescue! 

We can complete our component:
{% highlight javascript %}
@Component({
  selector: 'extended-input',
  template: `<div class="form-group"
                  [ngClass]="{'has-error':isError}"> 
                        <label class="control-label">{% raw %}{{labelText}}{% endraw %}
                            <ng-content select="input"></ng-content>
                        </label>
                        <ng-content select="input-errors"></ng-content>
             </div>
            `,
  directives: [CORE_DIRECTIVES, InputError]
})
export class ExtendedInput {
  @Input()
  labelText:string = '';
  @Input()
  isError:boolean = false;
  @ContentChildren(InputError)
  errors:QueryList<InputError>;
  
  ngDoCheck():void {
    if (this.errors) {
      this.errors.toArray().forEach(
        (error:QaInputError, i:number) => {
          if (i == 0) {
            error.showError();
          } else {
            error.hideError();
          }
        });
    }
  }
}
{% endhighlight %}

Important here is seeing how the use of **@ContentChildren** give us access to the functions on those components. Making
it a breeze to remove or show error messages.

Two important things to note:
1. Because we projecting content into more than one slot we need to use **CSS** selectors to select the content per
`<ng-content>` slot
2. We need to reset the display of the error messages on each change detection cycle. In this case it is best done
using the **ngDoCheck** lifecycle hook.

And here we have our first solution. It works, displaying only the highest priority defined error message. 

**A salad of style**

This is the simplest solution we will be looking at. And it is based on **Angular2** components accepting styling as
well as part of their definition.

In this case we do not need the extra error wrapper component of the previous solution and therefore our base component's
**HTML** becomes:
{% highlight html %}
<extended-input [labelText]="'Some number'"
                [isError]="!someNumber.valid">
    <input class="form-control"
           [ngFormControl]="someNumber">
    <input-errors>
        <span class="help-block" 
              *ngIf="someNumber.hasError('required')">
            A number is required
        </span>
        <span class="help-block" *
              *ngIf="someNumber.hasError('divisibleByTen')">
            The number should be divisible by 10
        </span
        <span class="help-block" 
              *ngIf="someNumber.hasError('minlength')">
            The number should be at least 7 digits
        </span>
    </input-errors>
</extended-input>
{% endhighlight %}

What we will do in this solution is to hide all but the first displayed error message with **CSS**. 

{% highlight javascript %}
@Component({
  selector: 'extended-input',
  template: `<div class="form-group"
                  [ngClass]="{'has-error':isError}"> 
                        <label class="control-label">{% raw %}{{labelText}}{% endraw %}
                            <ng-content select="input"></ng-content>
                        </label>
                        <ng-content select="input-errors"></ng-content>
             </div>
            `,
  styles: [`
            :host qa-input-errors > :not(:first-child) {
                display: none;
            }     
          `]
  directives: [CORE_DIRECTIVES]
})
export class ExtendedInput {
  @Input()
  labelText:string = '';
  @Input()
  isError:boolean = false;
}
{% endhighlight %}

And with that, it is done! It certainly has simplicity in its favour! If anything, the only issue is that some error
messages are now removed from the **DOM** while the rest are hidden with styling. 

But very light weight!

**NOTE:** In case you have not spotted the `:host` pseudo-class selector in the **CSS**, it is very important. If you are
trying to apply component styles to projected content you **HAVE** to use this to indicate that you are planning to style
the projected content. Omitting this will apply the styles only to the component's template. This pseudo-class is 
a **Shadow DOM** selector.

**A configuration object salad**

Taking some inspiration from **ngClass**, couldn't we provide out error definition object to our decorator directive and
let it do all the hard work for us?

The answer is a big **YES WE CAN**.

And with this solution our top level component template definition of the input becomes:
{% highlight html %}
<extended-input [labelText]="'Some number'"
                [inputErrors]="someNumber.errors"
                [errorDefs]="{required: 'A number is required',
                              divisibleByTen: 'The number should be divisible by 10',
                              minlength: 'The number should be at least 7 digits'}">
    <input class="form-control"
           [ngFormControl]="someNumber">
</extended-input>
{% endhighlight %}

I would lie if I did not admit that I really, REALLY like how concise this is in the **HTML**. That is a lot less
copy-and-paste when creating complex forms!

So what does it take to make this work?

A component definition like this:
{% highlight javascript %}
@Component({
  selector: 'extended-input',
  template: `<div class="form-group"
                  [ngClass]="{'has-error':isError}"> 
                        <label class="control-label">{% raw %}{{labelText}}{% endraw %}
                            <ng-content></ng-content>
                        </label>
                        <span class="help-block" 
                              *ngIf="errorMessage">
                              {% raw %}{{errorMessage}}{% endraw %}
                        </span>
             </div>
            `,
  directives: [CORE_DIRECTIVES]
})
export class ExtendedInput {
  @Input()
  labelText:string = '';
  @Input()
  isError:boolean = false;
  @Input()
  errorDefs:any;
  
  errorMessage:string = '';
  
  ngOnChanges(changes:any):void {
    var errors:any = changes.inputErrors.currentValue;
    this.errorMessage = '';
    if (errors) {
      Object.keys(this.errorDefs).some(key => {
        if (errors[key]) {
          this.errorMessage = this.errorDefs[key];
          return true;
        }
      });
    }
  }
}
{% endhighlight %}

In this solution we bind the error object of the input form control to the component and then watch it for changes. When
changes occur, we populate the error placeholder with the first error. Or completely remove it from the **DOM** if there
are no errors.

**NOTE:** In this case we used **Array.some** instead of **Array.foreach** as it stops iteration when your return a 
true boolean value.

**Taking a look back**

WOW, **Angular2** rocks.

I mean this is some seriously useful function! And written in minimal code. 

Making this in **AngularJS**, with the same level of customization and validation took a whole lot more effort!

But aside form what we made here, the point of this article is also to highlight how all the basic pieces you have already
learnt in **Angular2** can be easily put together to build some serious functionality.

And not only that, but the architecture of **Angular2** gives us the freedom to find a lot more different solutions 
to the same problem.
