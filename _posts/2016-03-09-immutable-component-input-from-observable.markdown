---
layout: post
title:  "Angular2: Binding an observable to an immutable child component input."
description: "Avoiding an undefined component input..."
date:   2016-03-09 13:10:21 -0100
categories: angular2 component observable @input immutable ngOnChanges
---

Sometimes it is the simple things that can cost you hours when looking at new technology. For me it was creating a simple
binding in **Angular2**.

I wanted to create a re-usable child component that would receive data, then edit it and finally pass the changed value back to the 
parent component. Also I wanted the incoming value to be immutable so, before making changes to the data in the child
component, I first wanted to make a copy of it.

All worked perfectly smoothly while using static local data, but then I refactored it to fetch data from the server
using **Http** and suddenly it was a few hours later with my application bleeding red undefined error messages all over my
Chrome console.

So come with me, oh intrepid Angular2 adventurer, let us discover together how to consume an **Observable** in a child component
without using ***ngIf** whilst still retaining an immutable object as a component input.

**Simple binding eh? What gives?** 

It all started with what seemed like a completely innocent child component:

{% highlight javascript %}
@Component({
  selector: 'child-component',
  templateUrl: './child-component.html',
  directives: [FORM_DIRECTIVES]
})
export class ChildComponent implements OnInit {

  @Input() person:IContact;
  @Output() onChange:EventEmitter<IContact> = new EventEmitter();

  internalModel:IContact;

  ngOnInit():void {
      this.internalModel = new Contact(person.id, person.firstname, person.lastname);
  }

  save():void {
    this.onChange.emit(this.internalModel);
  }

}
{% endhighlight %}

And the template for the component, where the properties of the incoming input were displayed and edited in
input fields:

{% highlight html %}
<form (submit)="save()">
  <div>
      <input id="firstName" [(ngModel)]="internalModel.firstname">
      <input id="lastName" [(ngModel)]="internalModel.lastname">
  </div>
  <button type="submit">Save</button>
</form>
{% endhighlight %}

And, for clarity sake, this is the definition of the **Contact** data model:

{% highlight javascript %}
export interface IContact {
  id: number,
  firstname: string,
  lastname: string
}

export class Contact implements IContact {

  constructor();
  constructor(id:number, firstname:string, lastname:string);
  constructor(public id?:any, public firstname?:any, public lastname?:any) {
    this.id = id ? id : 0;
    this.firstname = firstname ? firstname : '';
    this.lastname = lastname ? lastname : '';
  }

}
{% endhighlight %}

This all works very well until the incoming value is fetched from an **Observable** stream.

Why?

Because, at the time of **ngOnInit**, the value has not yet been resolved from the **Observable**.

Oh the horror! There was a monster loose in the once peaceful and happy town of *AngularComponent*. We need a 
superhero!

**Is it a bird? Is it a plane? It's ASYNC PIPE!**

The following snippet of HTML shows the usage of our child component with a binding to a data item called **selectedPerson**
which is defined in the parent component. This works like a charm when binding to a locally defined static object:

{% highlight html %}
<child-component [person]="selectedPerson" 
                 (onChange)="save($event)">
</child-component>
{% endhighlight %}

But as soon as this **selectedPerson** object is populated by subscribing to an observable, the undefined
errors starts to appear.

There has to be a way to solve this without using ***ngIf** or sacrificing the immutable input... 

The reason that solving this with ***ngIf** may not be the best solution is that overuse can cause some issues, from 
confusing assistive technologies to creating problems with CSS animation. Remember that this directive completely 
removes elements from the DOM and do not simply hide them. No, we should try to solve this by using the other shiny tools 
that Angular2 gives us. Removing DOM elements to solve a binding problem in our JavaScript should indicate that our
bindings are not very robust.

And indeed **Angular2** gives us a very natural way to directly subscribe to an **Observable** stream in your HTML 
by using the **Async pipe**. 

So in the parent component we could store the **Observable** in **selectedPerson**:

{% highlight javascript %}
this.selectedPerson = this.someService.getPersonFromObservable();
{% endhighlight %}

And then it should magically work by changing the HTML above to:

{% highlight html %}
<child-component [person]="selectedPerson | async" 
                 (onChange)="save($event)">
</child-component>
{% endhighlight %}

Right??!!!

WRONG!!

Even though the async pipe handles subscribing to the observable, the child component will still initialize before
the data hits the the **person** input. And the undefined errors continue to pour out on the console.

**ngOnChanges: The secret sauce.**

So up to this point we have data being fetched asynchronously and then being resolved and passed into a child component. However, 
there is nothing telling the child component to calm down, relax, and wait a little before making a copy of the data. 
There was one more required change.

A quick dive in the <a href="https://angular.io/docs/ts/latest/cheatsheet.html" target="_blank">**Angular2 Docs**</a> 
reveals a lifecycle hook we can use. And that is 
<a href="https://angular.io/docs/ts/latest/api/core/OnChanges-interface.html" target="_blank">**ngOnChanges**</a>.

What this does it to react to changes to the **@Input()** values of the component. BINGO!

As we are treating the input as immutable, the function will only be executed when the data is changed 
from the parent component, thereby also avoiding unnecessary execution of the code inside the function.

So our child component becomes:

{% highlight javascript %}
@Component({
  selector: 'child-component',
  templateUrl: './child-component.html',
  directives: [FORM_DIRECTIVES]
})
export class ChildComponent implements OnChanges {

  @Input() person:IContact;
  @Output() onChange:EventEmitter<IContact> = new EventEmitter();

   internalModel:IContact = new Contact();
  
    ngOnChanges(changes:any):void {
      var personChange:IContact = changes.person.currentValue;
      if (personChange) {
        this.internalModel = new Contact(personChange.id, 
                                        personChange.firstname, 
                                        personChange.lastname);
      }
    }
  
    save():void {
      this.onChange.emit(this.internalModel);
    }

}
{% endhighlight %}

It starts off by creating an empty version of the data model to, firstly, avoid the **ngModel** bindings from freaking out
and giving undefined errors and, secondly, so that we can use this component not only to edit incoming data, but also 
serve us to create new entries of the same type.

Then we can implement the **ngOnChanges** function. Note that this is best done by implementing the **OnChanges** 
**TypeScript** interface that **Angular2** gives us.

Every change to our incoming **person** input will trigger this function. 

At that point we can safely make a copy of the data into the internal model of our child component. From this point all
everything starts working as planned again.

And so we have restored calm to the town of *AngularComponent*. The *Monster of Undefined* has been slain.

**Points to remember:**

* Store your **Observable** stream in a data item inside your parent component.
* Use **ngOnChanges** to watch the immutable input in your child component.
* Then connect them up in the HTML template of your parent component using the **Async Pipe**.