# Swift API Design Guide

Fundamentals
The most important thing is not brevity but clarity.
Use all the words needed to avoid ambiguity but get rid of the redundant words.
Remove x ? or Remove something at x index ?

employees.remove(x)



employees.remove(at: x)



Which is more natural? Remove element cancelButton ? or Remove cancelButton ?

allViews.removeElement(cancelButton)



allViews.remove(cancelButton)



Name variables, parameters, associated types according to their roles.
var greeting: String?
func restock(from supplier: WidgetFactory)
associatedtype ContentView: View
Letter case
All upper or all lower case
Acronyms like ASCII and initialisms like SMTP use all upper or all lower case.
asciiCodes
representableAsASCII
smtpPort
userSMTPServer
Acronyms that are using as words like scuba, radar, laser
Use them as ordinary words
var radarDetector = RadarScanner()
Functions
Use grammatical English phrases.
Base name
Naming
Factory Method
Begin with "make" like x.makeIterator()
Take into account side-effects to name function.
Noun
When the function has no side-effects to the receiver.
x.distance(to: y) just returns distance between x and y without any changes to the x
Imperative Verb phrase
When the function has side-effects to the receiver.
x.sort() sorts x's elements directly.
Nonmutating and mutating pair functions


Mutating	Nonmutating
has side-effects to the receiver	has no side-effects to the receiver
x.sort()	z = x.sorted()
x.append(y)	
z = x.appending(y)

The verb "append" has direct object in English grammatically. So it has to have "-ing" in Nonmutating case.
y.formUnion(z)

If the nonmutationg function as a counterpart uses noun base name of the function. Append "form" before the base name.
x = y.union(z)

"union" is noun but this is natural in math like "Y union Z". We should use a noun in this situation.




Functions return Boolean
Use like this: "Receiver asserts the condition"
The earth orbits the sun.
earth.orbits(sun)
No imperative verb.
Overloading
The methods performs essentially the same things in the same domain can share their base name.
The methods share the same base name can be different classes and the methods usually do distinct things because domains are different.
If the same base name methods in the same domain do different things, make their names different.
Don't make overloading methods with different return types.
Parameter
Parameter
The parameter are not central to the function's meaning can be degraded after the first argument.
Label
When someone read it, it needs to be grammatical with a base name and be easy to make it documentation with the function signature.
If type information is not enough like NSObject, write more information to the function base name or parameter label names
addObserver(_ observer: NSObject, forKeyPath path: String)
Initializer, Factory Method
The first argument should not form a phrase.

init(with frame: CGRect)



init(frame: CGRect)



The first argument label can be omitted if the function converts another type from some types with value preservation.
let rgbForeground = RGBColor(cmykForeground)
value preservation doesn't mean that the type can show original value with its function.
value preservation example
To bigger data type from the smaller: Int32 to Int64 can preserve its "from" data in "to" data type
If parameters can't be distinguished, don't label them
min(a, b)
Preposition phrase
Use a preposition before the first parameter label when a base name matches  with its first parameter label grammatically.

// remove boxes length 12: awkward phrase

removeBoxes(_ length: 12)



// remove boxes having length 12

removeBoxes(havingLength: 12)



But if parameters are in the same abstraction like coordinator point or color value, use preposition after the base name.
moveTo(x: CGFloat, y: CGFloat)
If the first parameter value is an element of grammar phrase, it doesn't need a label

// add subview: view content view - redundant word

addSubview(view: contentView)



// add subview: content view

addSubview(contentView)



If the first argument can't be in the phrase with the base name, write a label.
dismiss(animated: Bool) - just make a label
If label doesn't exits: dismiss false - dismiss false itself ? dismiss itself is false ?
Closure
If closure is being used as API, label the arguments.
Overloading
If you use generics or other polymorphism, use label to avoid ambiguities.
The below functions has same semantic but the type is generic so that we don't know meaningful things without the label.
append(_ newElement: Element) vs append(contentsOf newElements: S) where  S.Generator.Element == Element
With contentsOf, we know append(contentOf:) appends elements of S one by one.
Consider how to explain in documentation to make natural labeling.
Label all the arguments except the above cases that tell unnecessary of labeling.
Default Value
Use default value to reduce complexity of a function.
Use default value with one function rather than function family.

func compare(_ other: String)

func compare(_ other: String, options: CompareOptions)



func compare(_ other: String, options: CompareOptions = [])



Locate parameters with default values toward the end of the parameter list.
Free function
You can define functions as Free functions in the only below cases
no self
min(x, y)
unconstrained generic
no type limitation, no inheritance, no where condition etc.
print(x)
domain notations that has existed for a long period of time
sin(x)
Protocols
Use noun if the protocol describes what something is.
Collection
Use "-able", "-ible" or "-ing" if the protocol describes a capability.
Equatable, ProgressReporting
I'd think we should consider that the protocol describes an abstract data type to name it as a noun.
I'd also think we should consider that the protocol describes some capability to do something like it can get progress value or can compare equality. In this case, this would be used to make multiple capabilities to a class or a struct.
I'm not sure when "-ing" postfix is better than "-able" or "-ible".
Properties
Properties return Boolean
Use like this: "Receiver asserts the condition"
The box is empty.
box.isEmpty
Use nouns in other cases. 
Type, Variable, Constant
Use nouns
I'd think assertion is also fine in necessary cases for variables.

Terminology
Use well-known terms
Don't use your own terms.
Don't make new non-standard abbreviations with terms that already exist.
If you work in some specific domain, you can use the domain's terms.
sin(x) in math.
Use terms well-known programming terms in the programming environment in your code.
Array is better than List in case of iOS environment.
