---
layout: post_page
---
I'm looking into ASP.NET MVC 5 now, as I haven't worked with it since the 2 version, and I want to get up to date again.

While I was implementing a view that includes validation of decimals, I ran into trouble once I enabled client side validation (it is enabled by default, but I had not included the jQuery Validation scripts yet). The issue stems from the fact that I live in a region where the decimal separator is a comma instead of a period. The default implementation of jQuery Validation apparently is not handling this well, so I had to look for a solution. And the allmighty Google supplied me with [this solution](http://www.stevendewaele.be/?p=183), which I wanted to reference here for future usage. I'll briefly repeat here in case the link would be disappearing (I assume this is ok for [Steven](http://twitter.com/StevenDeWaele)), as long as I honestly reference his post):

	$.validator.methods.range = function (value, element, param) {
		var globalizedValue = value.replace(",", ".");
		return this.optional(element) || (globalizedValue >= param[0] && globalizedValue <= param[1]);
	} 

	$.validator.methods.number = function (value, element) {
		return this.optional(element) || /^-?(?:\d+|\d{1,3}(?:[\s\.,]\d{3})+)(?:[\.,]\d+)?$/.test(value);
	}


