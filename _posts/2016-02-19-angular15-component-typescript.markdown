---
layout: post
title:  "Creating an AngularJS 1.5 component in TypeScript without losing your hair."
date:   2016-02-19 19:52:21 -0200
categories: angularJS1.5 component typescript
---
*Refers to AngularJS v1.5.0.*

This article assumes that you already know what is new in AngularJS 1.5 with regards to building component 
directives and that you have already looked at creating AngularJS elements in 
<a href="http://www.typescriptlang.org/" target="_blank">TypeScript</a>.

At the time of writing this, I had just embarked on my first attempt to create applications 
in AngularJS using TypeScript. All was going reasonably well until I started refactoring my 
brand new and shiny AngularJS 1.5 Component file. As I was also using this exercise to learn TypeScript, 
I guess you can imagine the consequences…

For the record I have been using AngularJS to create enterprise applications for a while, but in Javascript.  
So translating standard element directives into the new component structure was an easy refactor.

However, the TypeScript version posed a few more challenges. This article will show you how to use TypeScript to 
create AngularJS 1.5 Components.

For those only interested in the code, here it is, but unless it is immediately clear why this is working, 
I invite you to stay for the discussion.

{% highlight javascript %}
module app.directives {
 
    interface ISomeComponentBindings {
        textBinding: string;
        dataBinding: number;
        functionBinding: () => any;
    }
 
    interface ISomeComponentController extends ISomeComponentBindings {
        add(): void;
    }
 
    class SomeComponentController implements ISomeComponentController {
 
        public textBinding:string;
        public dataBinding:number;
        public functionBinding:() => any;
 
        constructor() {
            this.textBinding = '';
            this.dataBinding = 0;
        }
 
        add():void {
            this.functionBinding();
        }
 
    }
 
    class SomeComponent implements ng.IComponentOptions {
 
        public bindings:any;
        public controller:any;
        public templateUrl:string;
 
        constructor() {
            this.bindings = {
                textBinding: '@',
                dataBinding: '=',
                functionBinding: '&'
            };
            this.controller = SomeComponentController;
            this.templateUrl = 'some-component.html';
        }
 
    }
 
    angular.module('appModule').component('someComponent', new SomeComponent());
 
}
{% endhighlight %}

The template:

{% highlight html %}
<div>
    <h1>{{::$ctrl.headerText}}</h1>
    <span>You have clicked the button {{$ctrl.dataBinding}} times.</span>
    <button ng-click="$ctrl.add()">Add Click</button>
</div>
{% endhighlight %}

**Remember your training, Luke.**

So with one hand behind your back, blindfolded, while tapdancing with one foot you could write the following JavaScript 
to create the component:

{% highlight javascript %}
(function () {
    'use strict';
 
    angular.module('appModule').component('someComponent', {
        bindings: {
            textBinding: '@',
            dataBinding: '=',
            functionBinding: '&'
        },
        controller: SomeComponentController,
        templateUrl: 'some-component.html'
    });
 
    function SomeComponentController () {
        var vm = this;
 
        vm.add = function (){
            vm. functionBinding();
        };
    }
})();
{% endhighlight %}

But how does this work in TypeScript? I mean literally thousands of people have done this with the new 1.5 
version of Angular and posted their results online, haven’t they?

*“Hello Google my old friend, I’ve come to speak to you again! Yeah I will have this up and 
running in no time. Yeah, any time now. Urm…. Ok why am I on page 2 of the search results? 
This feels like visiting the dusty basement of Search Engine Optimization. What? What am I doing on page 3?! 
NOOOOOOOOOO!!!!!!!!!”*

Sitting there, looking accusingly at the search result screen, it dawned on me to have a look at the 
file for Angular. So I fetched the latest version of the angular.d.ts file from the DefinitelyTyped 
website and found that some unnamed savior had already added the types for the AngularJS 1.5 component. 
Whoever you are, you rock! (*Note: At the time of writing the type file still did not include the changes 
to the component interface from AngularJS 1.5-rc.1*)

{% highlight javascript %}
interface IComponentOptions {
 controller?: string | Function;
 controllerAs?: string;
 template?: string | Function;
 templateUrl?: string | Function;
 bindings?: any;
 transclude?: boolean;
 isolate?: boolean;
 restrict?: string;
 $canActivate?: () => boolean;
 $routeConfig?: RouteDefinition[];
}
{% endhighlight %}

So I flexed my awesome five-day-old TypeScript skills and realized again why, despite knowing that 
this is also recommended best practice in AngularJS 1.x, there remains a resistance amongst some 
Javascript developers to make the transition to TypeScript. I mean, how do you translate this into a 
working piece of code?

What makes this quite different to the normal AngularJS directive examples in TypeScript is that the 
component definition requires a configuration object instead of a function returning the configuration. 
The key was remembering that I can create such an object in a strongly typed way by generating a new 
instance of a class within TypeScript.

Now everything should be easy, yes? Well no, not if you have not done this before.

So let’s start by defining the body of the component and registering it with Angular.

{% highlight javascript %}
module app.directives {
 
    class SomeComponent implements ng.IComponentOptions {
 
        public bindings:any;
        public controller:any;
        public templateUrl:string;
 
        constructor() {
            this.bindings = {
                textBinding: '@',
                dataBinding: '=',
                functionBinding: '&'
            };
            this.controller = SomeComponentController;
            this.templateUrl = 'some-component.html';
        }
 
    }
 
    angular.module('appModule').component('someComponent', new SomeComponent());
 
}
{% endhighlight %}

For this example, I wanted to create a basic component with each of the three binding types. 
My component will fetch its HTML from a file and, as I also want some function, it will come with a controller.

So I created a class implementing the interface from the angular.d.ts file and defined 
the three properties I want to use in this example. As all properties of the configuration 
object are marked as optional in the interface I am free to only define the ones I will 
actually use. YAY! (*This also means that the current component interface definition still 
works with the slightly different component definition object from AngularJS 1.5.0. Double YAY!*).

Having defined the class, I can now set these properties in my class constructor. 
Then I am able to register it with angular using the new keyword and that will generate 
the needed configuration object to get my component working.

BUT, that was only step one. The real challenge for me was creating my controller. 
Here it is important to remember that the component defaults to ControllerAs syntax, 
meaning that all your bindings exist on your controller ‘this’. If you are not yet using 
ControllerAs in AngularJS, you need to start doing this.

As we are using TypeScript I will be unable to reference these ‘magically created’ 
controller variables without defining them first, not unless I want Typescript compiler errors.

And that is where the following comes in:

{% highlight javascript %}
interface ISomeComponentBindings {
    textBinding: string;
    dataBinding: number;
    functionBinding: () => any;
}
 
interface ISomeComponentController extends ISomeComponentBindings {
    add(): void;
}
 
class SomeComponentController implements ISomeComponentController {
 
    public textBinding:string;
    public dataBinding:number;
    public functionBinding:() => any;
 
    constructor() {
        this.textBinding = '';
        this.dataBinding = 0;
    }
 
    add():void {
        this.functionBinding();
    }
 
}
{% endhighlight %}

Like many AngularJS developers today, I use the John Papa AngularJS Style Guide. 
[*As an AngularJS developer you need to at least be aware of this document. 
So if you are reading this and have not seen this style guide, please read it*]. 
According to the guide, it is important to define the user interface of the AngularJS element 
you are writing as high up in the code file as possible. This makes it instantly clear to the 
reader of your code what the intention of you code is.

When writing the AngularJS 1.5 component in Javascript, this interface becomes clear 
from the configuration object, but in TypeScript we use an interface for the job.

So, what is the interface of my component? As it turns out, there are two.

Firstly there is the interface the user of my component will use when adding it to his/her HTML, 
literally the bindings.

Then secondly, there is the interface my component’s HTML template will use when communicating 
internally to the controller. As with any AngularJS controller I write in TypeScript, 
I need to clearly state my intent by defining an interface for the controller.

Since the component bindings are also exposed on my controller object I could simply do this:

{% highlight javascript %}
interface ISomeComponentController {
    textBinding: string;
    dataBinding: number;
    functionBinding(): any;
    add(): void;
}
{% endhighlight %}

The problem with this is that it does not clearly distinguish between the public 
component interface and the internal ‘private’ interface used by the component 
template for controller communication.

So as a user of this component, I would have to look further down into the internal 
implementation of my controller to see what I need to define in my HTML to activate 
the required bindings of the component.

So I decided to solve this by using TypeScript interface inheritance:

{% highlight javascript %}
interface ISomeComponentBindings {
    textBinding: string;
    dataBinding: number;
    functionBinding: () => any;
}
 
interface ISomeComponentController extends ISomeComponentBindings {
    add(): void;
};
{% endhighlight %}

Through this technique I created a bindings interface right at the top of the file, 
thereby clearly showing the user interface of my component. Then I extend this by 
creating the controller interface, which adds the internal interface I need to make my 
component HTML talk to its controller.

By implementing this interface in my controller class, I am now able to use the 
TypeScript strong typing inside my controller without getting errors from the TypeScript 
compiler when I use the binding variables (which I know are created on my controller object by AngularJS).

{% highlight javascript %}
class SomeComponentController implements ISomeComponentController {
    public textBinding:string;
    public dataBinding:number;
    public functionBinding:() => any;
 
    constructor() {
        this.textBinding = '';
        this.dataBinding = 0;
    }
 
    add():void {
        this.functionBinding();
    }
 
}
{% endhighlight %}

One final caveat was to define the functionBinding function in my class definition by using the fat arrow syntax. 
This way I am also able to write the function call with TypeScript without generating compiler errors.

And that solves all the issues of translating the Javascript version of the AngularJS 1.5 component to TypeScript.

Please let me know if you found this article useful and if it helped you. Also feel free to share the 
alternative methods you have found to solve this problem.


