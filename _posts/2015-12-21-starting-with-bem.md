---
layout: post
title: Starting with BEM
tags:
- css
- BEM
---

BEM has been around for a while now, and there's people who loves it and people who hates it. Here's my opinion on the matter after having used it several times in production in different teams, both in size and seniority.

# What is BEM?

First, a bit of theory. BEM stands for Block, Element, Modifier. It aims to help you create reusable components and establish a hierarchy inside it.  If you use BEM correctly, your HTML structure will look clearer and your CSS too, as it avoid complicated nested selectors.

`Blocks` are the names of the components. `Elements` are children that, when combined, conform the component. `Modifiers` are classes that provide flexibility in how blocks and elements look.

# A real world example

Let's talke a look at a real world example and go over th descisions i have made.

## Defining the block and its content

{% highlight html %}
<button class="button">
  <span class="button__label">Normal button</span>
</button>
{% endhighlight %}

{% highlight css %}
.button{
  border: 0;
  display: block;
  margin: 1rem 0 0 0;

  padding: .5rem 1rem;
  font-size: 13px;
  color: white;
  background: #3177F5;
  box-shadow: 0 0 10px 0 rgba(0,0,0,.3);
  
  cursor: pointer;
}
{% endhighlight %}

We just created our first BEM block, `button`. You can add a prefix if you want. I usually use the project name, but anything you find useful will do it, just stick to it. Then we created out first element, `button__label`. Note the double underscore. In BEM, `__` denotes hierarchy. In `buttton__label`, label is an element the button. 

But, what does *being an element* mean? It means direct relation. It means that the fragment of HTML belogs directly to the component. It doesn't really matter which HTML is in the fragment, but the fragment itself. This may sound confusing, but it is actually a good thing: if doesn't matter if the element is an `span` or a `div` or a `p`. That's HTML implementation. What matters is that that fragment belongs to the components. That's the power of BEM. 

## Creating different variants

We created a defailt button before. In any website, changes are we need more types of button (to accept, to remove, to cancel, you name it). `Modifiers` are thw way to say "Ok, i want the same component but with a *slightly* different behavior". Notice i added the word *slightly*. If your modifiers are changing dramatically your component, you probably need two different components.

{% highlight html %}
<button class="button button--danger">
  <span class="button__label">Normal button</span>
</button>
{% endhighlight %}

{% highlight css %}
.button--danger{
  background: tomato;
}
{% endhighlight %}

Here we have just created the `button--danger` modifier, by using two dashes. We created a new version of a button, one to denote danger. This means that this new version is still a button, it still has the same functionality of a regular button but it looks different.

## Combining modifiers

Now we're getting used to BEM we can create more modifiers for this button: `.button--danger`, `.button--warning`, `.button--success`. But let's imagine we need a *disabled* state. We could easily create more modifiers: `.button--danger-disabled`, `.button--warning-disabled`, '.button--success-disabled`. It doesn't look right; if we were to add more versions of the button, we sould need to create the disabled version for the new ones as well.

Well, BEM is flexible enough to allow us to use more than one modifier per block or element. So, we could solve the previous problem like this.

{% highlight html %}
<button class="button button--danger button--disabled">
  <span class="button__label">Normal button</span>
</button>
{% endhighlight %}

{% highlight css %}
.button--disabled{
  opacity: .5;
  pointer-events: none;
}
{% endhighlight %}

Nice! We have a modifier to handle the disabled state that is not coupled to any other modifier, so we ca use it freely.

[Full live example here](http://codepen.io/asainz/pen/PZzOoY)

# What's next

I'm planning to write more about bem. I enjoy using it, writing about it and i have  enough experience with it to have identified what i like and what i *don't* like about it. So, here's what i expect to write in the following days.

1. A more complex example, where we can see more benefits of using BEM.
2. Overuse of BEM. When do i need a BEM component and when do i need just a class.
3. Using it correctly in large teams. Not everyone is skilled enough to use it correctly and, let's be honest, not everyone care about css.