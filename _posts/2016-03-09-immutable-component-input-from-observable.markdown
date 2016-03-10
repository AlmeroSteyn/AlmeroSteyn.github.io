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

I finally found a solution to this problem not using ***ngIf** and, as this type of solution is not yet easy to find, I 
thought maybe I should show it here. 

**Simple binding eh? What gives?** 

I wanted to create a re-usable child component to edit an incoming value and then pass the changed value back to the 
parent component. Also I wanted the incoming value to be immutable, so the value has to be first copied in the child 
component, before making any changes to it.

Here follows the code that, at first, worked perfectly well.

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

Of course, at the time of **ngOnInit**, there is no guarantee that a value has been resolved from the **Observable**. And,
in fact, even with a server running locally and fetching data with **Http**, the **person** input ended up being
undefined.

Oh the horror! My nice Angular2 application started bleeding red all over the console and, while it was quickly clear why
this was happening, it was not so obvious how to solve this, it first.

**Is it a bird? Is it a plane? It's ASYNC PIPE!**

The following snippet of HTML worked like a charm when binding to an object that is not fetched asynchronously:

{% highlight html %}
<child-component [person]="selectedPerson" (onChange)="save($event)"></child-component>
{% endhighlight %}

The problem described started when the object populated asynchronously via 

A quick search suggested that adding ***ngIf** to the html 

There simply had to be a way to use the beautiful new binding tools in Angular2 to make this work. 







