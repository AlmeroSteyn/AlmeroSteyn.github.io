---
layout: post
title:  "Angular2: Binding an observable to an immutable child component input."
description: "Avoiding an undefined component input..."
date:   2016-03-09 13:10:21 -0100
categories: angular2 component observable @input immutable ngOnChanges
---

Sometimes it is the simple things that can cost you hours when looking at new technology. For me it was creating a simple
binding in **Angular2**.

I wanted to create a re-usable child component to pass some data into, then edit it and finally pass the changed value back to the 
parent component. Also I wanted the incoming value to be immutable so, before making changes to the data in the child
component, I first wanted to make a copy of it.

All worked perfectly smoothly while using static local data, but then I translated it to fetching data from the server
using **Http** and suddenly it was a few hours later with my application bleeding red error messages all over my
Chrome console.

So come with me and I will show you, oh intrepid Angular2 adventurer, how to consume an **Observable** in a child component
without using ***ngIf** whilst still retaining an immutable object as a component input.


**Simple binding eh? What gives?** 

It all started with what seemed like a completely innocent child component. 

{% highlight javascript %}
@Component({
  selector: 'child-component',
  templateUrl: './child-component.html',
  directives: [FORM_DIRECTIVES]
})
export class ChildComponent implements OnInit {

  @Input() person:IContact;
  @Output() onChange:EventEmitter<IContact> = new EventEmitter();

  internalItem:IContact;

  ngOnInit():void {
      this.internalItem = new Contact(person.id, person.firstname, person.lastname);
  }

  save():void {
    this.onChange.emit(this.internalItem);
  }

}
{% endhighlight %}

And the template for the component, where the properties of the incoming input were being displayed and edited in
input fields.

{% highlight html %}
<form (submit)="save()">
  <div>
      <input id="firstName" [(ngModel)]="internalItem.firstname">
      <input id="lastName" [(ngModel)]="internalItem.lastname">
  </div>
  <button type="submit">Save</button>
</form>
{% endhighlight %}

This all works very well until the incoming value is being fetched from an **Observable** stream.

Why?

Because, at the time of **ngOnInit**, there is no guarantee that a value has been resolved from the **Observable**. And,
in fact, even with a server running locally and fetching data with **Http**, the **person** input ended up being
undefined. 

Oh the horror! 

**Is it a bird? Is it a plane? It's ASYNC PIPE!**

The following snippet of HTML worked like a charm when binding to a locally defined static object:

{% highlight html %}
<child-component [person]="selectedPerson" (onChange)="save($event)"></child-component>
{% endhighlight %}

But as soon as this the **selectedPerson** object gets populated as a result of subscribing to an observable, the undefined
errors start appearing.

There had to be a way to solve this without using ***ngIf** or sacrificing the immutable input. 

The reason I do not like solving this with ***ngIf** is that overuse can cause some issues, from confusing assistive 
technologies to problems with CSS animation. No, we should try to solve this using the shiny tools that Angular2 gives us.

Yes, it gives us a very natural way to directly subscribe to an **Observable** stream by using the **Async pipe**. 

So in the parent component I would store the **Observable** in **selectedPerson**:

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

Even though the async pipe will handle subscribing to the observable, the child component will still initialize before
the data hits the the **person** input. And the undefined errors continue to pour out on the console.

**ngOnChanges: The secret sauce.**

So up to this point I have data being fetches asynchronously and then being given to a child component who has not idea
that this is happening. There was one more required change. The child component had to somehow wait for the input to 
be populated before making the copy that could be edited.

And a quick dive in the **Angular2 Docs** revealed another lifecycle event I could use. And that is **ngOnChanges**.

What this does it to react to changes to the **@Input()** values of the component. BINGO!

And as the component is seeing its input as immutable the this function will only be executed when the data is changed 
from the parent component, thereby also avoiding this function from being overly executed.

{% highlight javascript %}
@Component({
  selector: 'child-component',
  templateUrl: './child-component.html',
  directives: [FORM_DIRECTIVES]
})
export class ChildComponent implements OnChanges {

  @Input() person:IContact;
  @Output() onChange:EventEmitter<IContact> = new EventEmitter();

   internalItem:IContact = new Contact();
  
    ngOnChanges(changes:any):void {
      var personChange:IContact = changes.person.currentValue;
      if (personChange) {
        this.internalItem = new Contact(personChange.id, personChange.firstname, personChange.lastname);
      }
    }
  
    save():void {
      this.onChange.emit(this.internalItem);
    }

}
{% endhighlight %}







