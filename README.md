
Created by Andrew Kelly (andrewrk) and thejoshwolfe

#### Function Overloading

No plans to support.

#### Default Function Argument Values

Andrew has indicated "probably not" this feature.  Not sure of the reasons yet, might be related to the reasons for not supporting function overloading.

#### No UFCS

https://github.com/zig-lang/zig/issues/148

Andrew explains that how UFCS would fit within Zig is not clear and it's usefullness is also not clear.

#### Type inference

You can omit the type of a variable when declaring it:
```
var x = 0;
```
For function arguments you use the `var` keyword:
```
fn foo(x : var) -> @typeOf(x) {
    return x;
}
```
In the future, this may also be supported for functions like this:
```
fn() -> var
{
    return 0;
}
```

#### Nested Functions?

#### Delegates

Haven't seen anything related to delegates.  However, member functions work differently in this languages, they are more like normal functions than in D.

#### Named function arguments Default Function Argument Values

I've talked with Andrew about this.  Here's the transcript:
```
[16:15] <marler8997> As far as "named function arguments", I haven't really used languages that have that, but I've always thought i might be a good idea
[16:15] <marler8997> D for example has a Flag type, so instead of using named arguments it has Flag!"enableSomething"
[16:15] <marler8997> void foo(Flag!"enableA" enableA, Flag!"enableB" enableB)
[16:16] <marler8997> foo(Yes.enableA, No.enableB)
[16:16] <marler8997> If it had named arguments, you could do foo(enableA:true, enableB:false) without using the Flag type
[16:16] <andrewrk> named arguments might be a good idea. you can opt in to making it be a compile error if the name is changed or parameters re-ordered
[16:17] <marler8997> right, that as well
[16:17] <marler8997> something to think about
[16:17] <andrewrk> maybe you *must* name arguments if the types are compatible
[16:17] <marler8997> ?
[16:18] <andrewrk> e.g. if you had fn foo(x: i32, y: i32)  and then later you re-ordered these parameters, all the call sites would be wrong, but silently compile successfully. unlike if the types were incompatible, you'd get compile errors
[16:18] <marler8997> ah I see
[16:19] <marler8997> I think there are cases where it's not obvious what order arguments are in, and cases where they are or it doesn't matter
[16:19] <andrewrk> feel free to make a proposal for this. if you don't I'll make one eventually
[16:19] <marler8997> add(x: i32, y:i32)
[16:19] <marler8997> Don't need names
[16:19] <andrewrk> oh yeah that's a good point
[16:19] <marler8997> power(base: i32, exponent: i32) might be a good idea
[16:19] <andrewrk> would be harmless to have to give names though
[16:20] <marler8997> Well now you have less encapsulation
[16:20] <marler8997> If the implementation changes the name of the variable, you have to change all places where you call it
[16:20] <marler8997> I might provide a way to indicate that an argument should be named
[16:21] <andrewrk> yeah but that's a lot like an API change - changing the parameter name
[16:21] <andrewrk> maybe you changed the name from length_in_inches to length_in_cm
[16:21] <marler8997> Yeay, the thing is sometimes names have no meaning in regards to the API
[16:21] <marler8997> fn compare(left: var, right: var)
[16:21] <marler8997> left and right really don't convey any information
[16:22] <marler8997> then someone might make another function, isEqual(a: var, b: var)
[16:22] <marler8997> What I've found is that sometimes it makes sense to specify the parameter name, and sometimes the name is implied from the name of the function itself
[16:23] <marler8997> If the function is operating on a group of paramters and is commutative, then no names are necessary
[16:25] <andrewrk> Yeah probably specifying names would be optional. Which is in contrast with the principle of only one way to do things, but helping the principle of Compile errors are better than runtime errors
[16:26] <marler8997> Well I was thinking you could have that controlled by the function definition
[16:26] <marler8997> Having one way of doing things is very good principle
[16:27] <marler8997> power(named base: i32, named exponent: i32)
[16:27] <andrewrk> That's an interesting idea
[16:27] <marler8997> power(base=2, exponent=8)
[16:28] <andrewrk> I'd like to run a proposal by thejoshwolfe
[16:28] <marler8997> Cool
```

