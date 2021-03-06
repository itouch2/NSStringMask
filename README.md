NSStringMask
------------

This tiny library was developed to help you apply masks and formats to strings.

For instance, suppose you have the string `12345678` and want to format it as a Social Security Number (which regex pattern is `\d{3}-\d{2}-\d{3}`). With NSStringMask, all you have to do is `[NSStringMask maskString:@"12345678" withPattern:@"(\\d{3})-(\\d{2})-(\\d{3})"]` and the result will be "123-45-678". Simple enough?

## Installation

You can clone the repository and copy the NSStringMask.[hm] to your project or via cocoa pods.

## Documentation

Take a look on the [complete documentation](http://fjcaetano.github.io/NSStringMask/).

## Usage Example

Whenever you set a string pattern or a regex, it must have at least one capturing parentheses `[group]`. This is because the class comprehends that everything that is in between parentheses are the strings that must be matched and replaced. If you need explicit parentheses in your format, escape it with slashes:

	[NSStringMask maskString:@"c" withPattern:@"\\w"]
	// result: nil

	[NSStringMask maskString:@"c" withPattern:@"(\\w)"]
	// result: "c"

	[NSStringMask maskString:@"c" withPattern:@"\\w-(\\w)"]
	// result: w-c

	[NSStringMask maskString:@"3" withPattern:@"\\((\\d)\\)"]
	// result: (3)

These are few of the many forms to use NSStringMask:

### Simple Pattern

In this case, the method will return the expected result _only_ if the provided string's length is equal or longer than expected:

	[NSStringMask maskString:@"1234567890" withPattern:@"(\\d{3})-(\\d{3})-(\\d{4})"]
	// result: 123-456-7890
	
If the string is shorter, the method won't apply the format, but instead, return a cleaned string with the valid characters:

	[NSStringMask maskString:@"123foo456" withPattern:@"(\\d{3})#(\\d{4})]
	// result: 123456
	
	
### Pattern with Placeholder:

Placeholders allow you to fill strings shorter than expected with characters to complete the formatting:

	[NSStringMask maskString:@"" withPattern:@"(\\d{2})/(\\d{2})/(\\d{4})" placeholder:@"_"]
	// result: __/__/____
	
It can also be a long string. In this case, the replacement will restart for each group in your pattern:

	[NSStringMask maskString:@"" withPattern:@"(\\d{2})/(\\d{2})/(\\d{4})" placeholder:@"abcde"]
	// result: ab/ab/abcd
	
### NSRegularExpression

You may also provide an instance of NSRegularExpression instead of a pattern, the result is the same.

When a pattern is passed, the class creates a NSRegularExpression object with NSRegularExpressionCaseInsensitive option. If you need it to be different, it may be interesting to provide the regex and not a string pattern.
	
## License

NSStringMask is licensed under the MIT License:

Copyright (c) 2013 Flávio Caetano ([http://flaviocaetano.com](http://flaviocaetano.com))

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.