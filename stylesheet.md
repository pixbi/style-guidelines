# CSS and HTML Guidelines

This guideline will grow and evolve as Pixbi does. If an idea here conflicts with your personal philosophy then we urge you to talk about it. The issues section is your soapbox, so do not be afraid to climb up and start yelling.

## HTML General Guidelines

1. Avoid over-nesting elements, and be as conservative as possible with adding elements.
2. Don't use IDs unless you have a really good reason.

## CSS General Guidelines

1. Only use classes/attribues/pseudoselectors. Make an attempt to refrain from the use of IDs and element names.
2. Don't use *. It's most likely never necessary.
3. Try not to nest further than three levels. Any more is probably unnecessary and will add weight. If you see anything nested more than three levels, refactor it.
5. Anything quantitative that isn't immediately obvious should be saved into a variable. No one we've met has the ability to visualize hex color codes.
6. The use of magic numbers (i.e. 382px for a margin-top) is dangerous and not flexible. Attempt to be more graceful.
