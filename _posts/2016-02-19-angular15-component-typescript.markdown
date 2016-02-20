---
layout: post
title:  "Creating an AngularJS 1.5 component in TypeScript without losing your hair."
date:   2016-02-19 19:52:21 -0200
categories: angularJS1.5 component typescript
---
This article assumes that you already know what is new in AngularJS 1.5 with regards to building component 
directives and that you have already looked at creating AngularJS elements in TypeScript.

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

{% highlight typescript %}
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
