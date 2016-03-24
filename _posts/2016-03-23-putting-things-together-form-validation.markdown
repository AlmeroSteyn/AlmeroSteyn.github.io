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

So what better to try out in **Angular2** than to recreate one of the most complex **AngularJS** directives I ever wrote.

**SAY WHAT???!!**

In short, today we will be building an **Angular2** form validation component. And to see just how flexible it is,
we will be building the same component in three different ways. 

Before we come out the end of this blog post we will have used the following concepts in **Angular2** to see how they
fit into making a more complex functional component:

* Model forms
* Custom validators
* @Contentchildren decorator
* Displaying validation errors
* Content projection (transclusion)
* Component styles
* Change detection
* Lifecycle hooks

We will also be using **Bootstrap** as styling framework. It can, of course, be translated to use any styling you prefer
to use.

And we are going to use all of that to build this:

{::nomarkdown}
<figure>
    <img src="/css/images/2016-03-24-form-validation-zen/Component.jpg" alt="Form component with styled validation.">
</figure>
{:/}

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
