---
layout: post
title:  "Angular2: Binding an observable to an immutable child component input."
description: "Avoiding an undefined component input..."
date:   2016-03-09 13:10:21 -0100
categories: angular2 component observable @input immutable ngOnChanges
---

Today I was confronted with my first not-so-obvious challenge in Angular2. After moving past the basics, it was time to
take the next step towards building a serious application in this shiny new framework.

And the challenge came in the form of passing the result of an **RxJS Observable** stream into an immutable component 
input.

**The problem** 

I wanted to create a re-usable child component to edit an incoming value and then pass the changed value back to the 
parent component. Also I wanted the incoming value to be immutable, so the value was first copied in the the child 
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

{% highlight javascript %}
<form (submit)="save()">
  <div>
    <label for="firstName">First Name:
      <input id="firstName" [(ngModel)]="internalItem.firstname">
    </label>
    <label for="lastName">Last Name:
      <input id="lastName" [(ngModel)]="internalItem.lastname">
    </label>
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








