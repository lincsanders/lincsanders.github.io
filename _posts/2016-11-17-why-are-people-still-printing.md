---
title: CSS for printing tables at 100% width
layout: post
date: '2016-11-17 04:44:32'
categories: programming css
---

One of the many things people do in Endas is print things out. Included (but not limited to) client lists. This might be needed to take on the road where data services might be partial or non-existing, where they can more quickly jot down notes and ideas onto paper with pen as opposed to being forced to use a phone's keyboard - whatever, the need for printing things in a nice enough format is apparently still alive and well.

I've gone through the effort of providing a lot of "information at a glance" in the base "List" views in most places of Endas. Instead of writing a special printable version of these pages, I decided to keep it DRY and solve it with CSS which hooks into the existing patterns I use for my "List" views.

The fix (for my standard Bootstrap/SASS stack at least) was significantly easier than I thought using pretty much exclusively the following:

```css
@media print {
	a.btn, button.btn {
		display: none;
	}
}
```

However no matter how much I googled I couldn't get a table to stay at width: 100% when previewing using print media.

![Paperton](/assets/posts/2016-11-17-why-are-people-still-printing-1.png)

Notice the table not respecting the 100% width usually enforced via bootstrap.

The fix for that was the following two lines, which took me an embarrasingly long time to find: 

```css
@media print {
	table.table {
		width: 100%;
		display: inline-table !important;
	}
}
```

And voila!

![Paperton](/assets/posts/2016-11-17-why-are-people-still-printing-3.png)


**But that doesn't fix my main problem, which is *It's 2016 and people are still printing things.***