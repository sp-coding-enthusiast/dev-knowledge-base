Hello guys.

We are going to continue the discussion with respect to Python.

And in this video we are going to talk about loops.

Already in our previous video we have uh, we have seen a lot of examples with respect to conditional

statements like if else if else.

And we have seen multiple examples out there right now in loops, we will be discussing about what are

the different types of loop we usually use in Python programming language, like for loop, while loop

or loop control statements like break, continue and pass.

Then we'll be discussing about nested loops, and then we'll be seeing like all these things, we will

be seeing much more in with the help of practical examples.

And what are the common errors we usually face and how to avoid those errors.

So all these things will be discussing in this particular video.

So first of all let's go ahead and work with for loop with a simple, uh, you know, syntax.

So in order to write a for loop right you need to understand what a for loop is.

A for loop is a loop right.

It is used to iterate over a sequence of numbers.

Okay.

So let's say I will give one example like for I, okay, I is just a temporary variable right now in

let's say I want to create a sequence of numbers.

Now in order to create a sequence of numbers, I will show you with the help of range.

Okay.

So what exactly is range?

Okay.

So let's say in this particular range I give five elements.

I basically want five elements over here.

So this is turn actually help us to generate numbers between 0 to 5.

Right.

So here you can see that hey I'm getting a range between 0 to 5 over here.

And let's say I want to just display all these numbers inside this right range is just giving us a sequence

of numbers between 0 to 5.

But if I want to iterate through this, all the numbers I can basically use for loop.

So if I write for I in range five, right.

And here if I go ahead and print I right now, you will be seeing that after every iteration.

First of all, when we are looping inside this sequence of numbers between 0 to 5, first it will go

ahead and display zero.

Then it will go ahead and display one.

That basically means after every iteration, this number is basically getting incremented and it is

traversing through all this range of numbers.

One important thing that you should understand that since I have used range between 0 to 5, the last

number is not going to get included.

So that is the reason you can see zero is here, one is here, two is here, three is here, and four

is here.

Right.

But the total number of elements is five over here and here.

In short I have spoken about for loop and range as a function.

Okay.

So range as a function is also given.

Let's say I want to probably use for loop with different range of numbers.

Right.

Let's say if I go ahead and write one comma six, that basically means I want the number between 1 to

6.

Six is the last number.

So we are not going to include it because at the end of the day, with respect to Python, whenever

we are seeing indexing right, it always starts with zero, right.

So I'll talk more about it as I go ahead.

Now, if I go ahead and execute this here, you'll be able to see one is getting displayed, two is

getting displayed, three is getting displayed, four is getting displayed, five is getting displayed.

So I can also call all my range of numbers with respect to or by giving numbers between one number to

the other number itself.

Right.

Now let me just give you more examples over here by using range.

So if I go ahead and write range range of one comma ten.

And let me just go ahead and give some third parameter.

Right.

So third parameter over here you'll be able to see that it is something called as step.

Now see see the syntax.

It shows start as the first parameter inside range function.

Then you have the stop parameter.

Then you have the step parameter okay.

By default step parameter is usually given as one.

Now start I'm saying hey start from one end till ten right.

And before ten I'll not say till ten but before ten and use the step size as one.

That basically means only increment one number at a time.

So if I go ahead and execute it, this will basically give me a range of value between 1 to 10.

But and the step size will be one.

Right now let me just go ahead and make it two okay.

So here you can see that I'm starting from one before ten.

It will stop.

And here the range is two.

That basically means the two numbers will get incremented.

Now let me do one thing.

Okay.

Let me just write one over here and let me use a for loop again for I in range of this.

And let me go ahead and print I okay.

Now when I'm printing I you'll be able to see that what I'm actually getting.

123456789.

Now let me make this change from step size 1 to 2.

Now what will happen?

See, after one directly three will get displayed because we are going to skip one number.

So it is just going to jump two steps ahead.

Right.

Now see this.

So now I can see 13579 right.

So I am not probably traversing to each and every number, but instead I have given a step size of two.

So it is jumping two numbers ahead.

And that is how it is basically getting printed.

Let me just show you one more example.

Let's say that I want all the numbers between 10 to 1.

But now this time I will use a step size of minus one.

Now what it is going to do, it is going to display a number between 10 to 1, and step size will be

minus one.

That basically means after ten it will become nine, then eight, then seven.

See this.

So here you can see 910 987654321 is not getting displayed as we know that last number will be skipped.

Before this all the numbers will be displayed.

One more example that we if I really want to show it to you.

So here you can see minus two if I'm using minus two.

So ten 86542642.

Right.

So I hope you have got an idea with respect to for loops.

And with the help of range how we can actually move.

Okay.

Now let me show you with respect to strings I hope everybody has learned strings.

Right.

So strings are how to probably create string.

Let's say that this is my string okay.

This is my string.

And here I am going to write Krish Nayak.

Okay.

Now if I want to traverse to this particular string.

Now see, one amazing thing about this data structure called a string is that we can traverse to each

and every character over here.

So if I go ahead and write for I in str, okay.

And uh, for in str.

And if I just go ahead and print I.

Okay.

So string is basically a data structure.

It is just nothing.

But it is a collection of characters.

Right now if I'm going to print over here, here you can see k r I s h.

Then again space and I k right.

Let's say that I am traversing to this particular string.

And I also want to do something like I may have a sentence, I may have a paragraph.

So based on that also I can print it over here.

Right.

Just to give you an idea what exactly this is, uh, because string is a collection of characters,

right?

It is a collection of characters.

And we can also traverse thing.

So the for loop main functionality is that whenever you have any collection items, like any collection

data structure, you can traverse through it very easily by just using a for loop.

Right.

So I've just given you an idea about it.

But as we go ahead, we'll be seeing more complicated example, uh, as we go ahead, right?

But just to understand the basic example, this is what a for loop is all about.

Now let's go ahead and discuss about something called as while loop.

Okay.

So while loop.

So now let's see something about while.

So now I have while loop.

Okay.

Now with respect to while loop right.

If I really want to give a small definition, this while loop is nothing, but it continues to execute

as long as the condition is true.

Okay.

That basically means unless and until this while loop, whatever condition I'm writing in while loop,

it is true it is just going to execute it.

Okay.

Now let me do one thing.

Let me create a temporary variable called as count.

Okay.

Count okay.

Now with respect to this particular count let me just go ahead and write while count is less than five

okay.

And now I have gone inside my while loop while block or while loop over here.

So I'm putting this particular condition, unless until this count is not, is less than five.

Just go ahead and print it.

Okay.

Let's say I'm going to print the count.

Okay.

And after this, if I'm executing C, I also need to increment the count over here.

So I will go ahead and write count plus one.

Okay.

So what I'm doing unless and until this count is less than five I'm going to print the count.

And for every iteration, because we have initially initialized, count is equal to zero for every iteration

I'm writing count equal to count plus one okay.

Now see what will happen if I execute this.

You'll be seeing that zero is getting displayed.

Initially I will be having zero.

So when I write while count is less than five, this is true.

It is just going to print the count.

So I'm going to get zero over here.

And then it is going to increment the count.

Now my temporary variable count will have one value right?

I'll not say temporary, but my count value from this zero has got incremented to one.

Then again this five while loop will run.

Why it will run because this condition is still true, right?

So now here you can see when one is less than five.

So one is obviously less than five.

In the second loop.

So again this will get executed.

Then again this will get incremented.

Then again it will go to the next loop.

Then this will become 234 then.

But once it becomes five right.

While five is less than five now this becomes false.

It is just going to come outside the loop, right.

So that is how you are getting displayed with 01234.

Right.

So this is a simple way of displaying or understanding about the while loop.

Okay.

Um, I may also write something like this while okay let's go ahead and write.

Count is equal to zero okay.

Count is equal to zero while.

Count while count percentile two is double equal to zero okay.

So now see this condition.

What I'm saying while count percentile two is double equal to zero.

If this is true right I will probably go ahead and print the count over here.

Right?

Right.

And let's say that I will go ahead and or let me do one thing, okay?

If I'm starting from count is equal to zero.

And this condition is basically to check whether a number is a even number or not.

Right.

So if I just go ahead and execute it, how many times this will get displayed.

See zero is getting displayed over here.

Right.

And it is continuously getting displayed.

I'll stop this.

See because I have not written any condition over here.

So let me just go ahead and write.

Count is equal to count plus one okay.

Now how many times it will get displayed.

You just see this okay.

Only one time.

Because the next time it became one this count became one.

Then one percentile two is not equal to zero.

So it is just going to come outside of the loop right of this particular loop.

This is just to show you an example over here.

But we will be seeing with more amazing examples.

First of all, let's go ahead and just see the basic syntax of for while.

And now we are going to go ahead with respect to loop control statements okay.

Loop control statements.

You'll be seeing that.

Chris.

Please give more examples.

Don't worry.

After I probably make you understand all these things, then we will be seeing more examples as we go

ahead.

Okay.

Now with respect to the loop control statement, first of all, we'll discuss about something called

as break okay.

Now if you really want to understand break I'll just go ahead and write this definition.

The break statement exists.

Exits the loop.

Permanent.

Exits the loop prematurely.

Okay.

What does this basically mean?

I will just make you understand.

Okay.

Let's say I want to write a break statement.

Now, how do I write a break statement?

So first of all, let's say I am going to run for I in range.

Okay.

Please make sure that you understand the syntax for I in range.

Range of the collection.

This is nothing, but this is collection.

It can be a list.

It can be a dictionary.

It can be range.

It can be string.

Anything it can be.

And let's say I'm writing ten.

So ten basically means it is going to iterate from 0 to 1 okay.

For one of the condition I'll say if I is double equal to five okay.

If this I is equal to five I don't want to probably or I want to come outside this particular loop okay.

I want to come outside this entire for loop.

So I will go ahead and just write break okay.

And once we probably write break okay.

It is probably going to come outside of this particular for loop itself.

Right.

Now one more thing.

If I is not equal to five at that time we just need to print I.

Okay.

So now see what is this entire code that I have actually written.

For I in range of ten, if I is double equal to five I'm saying only when I is equal to five do.

The break statement comes outside of this particular for loop.

When I is not equal to five, you just need to keep on printing the numbers okay?

So now if I go ahead and execute it here, you'll be able to see 01234.

Then when five came automatically we came outside of this particular for loop.

Okay.

And then after that, nothing is getting printed.

So we are executing this particular loop permanently.

Okay.

Permanently with the help of break over here.

But this break will only get applied on any statement on any condition as such.

Right?

So that is why we are specifically using this break statement.

Okay.

Uh, this is one of the good examples.

Uh, again, uh, now with respect to the another loop control statement, we also have something called

as continue.

Okay.

So now we will go ahead and write.

Continue.

Now what exactly continue is okay.

And you also need to know this if I really want to define continue okay.

Continue.

Statement skips the current iteration and continues with the next okay.

So that basically means let's say I'm going to write for I in range okay.

For I in range for I in range.

And let's say I write some elements over here ten okay.

And now if I go ahead and write if I modulus two right is double equal to zero okay.

And this condition is basically just to check whether the number is even or not.

If the number is even let's say that I will go ahead and write continue okay.

I will just go ahead and write continue.

And then I will just go over here print I okay.

Now in short, if I really want to make you understand, this is just like displaying all the odd numbers

between 0 to 10, right?

Do you agree with me or not?

See what I'm doing over here?

For I in range of ten.

If I percentile.

If I modulus two is equal to zero, that basically means this is an even number.

We're just going to continue.

Otherwise if it is not which is an odd number we are just going to print it.

So if I go ahead and execute this you'll be able to see that I will only get an odd number 13579 between

0 to 10.

Right.

And that is what is a continue example with respect to continue.

We are just we are just skipping the current iteration.

This will just skip.

It will even not go to the print statement.

We'll just go ahead and continue the loop.

Right.

So this is what is the power with respect to the continue statement.

There is also one more amazing flow control that we use that is basically called as pass okay.

And you should know all these things because some or the other way we will be using all these things

right.

Uh further when we'll be seeing multiple example, the pass statement is a null operation and it does

nothing okay.

It does nothing.

Nothing means nothing, right?

It will just say, hey, I don't want to do anything on a specific condition, okay?

So now if we go ahead and write for I in range for I in range of five, let's say okay.

For I in range of five.

Let's say I'm giving this particular condition okay.

I'm saying hey if I is equal to three, if I is double equal to three okay.

Then I'm saying hey just pass okay.

Do nothing okay.

I don't want you to do anything over here.

Okay.

And then we are going to print I.

Okay.

Now see what will happen in this particular case.

Whenever I say hey, whenever the number is even, just skip this for loop.

But here it is saying do nothing, just go ahead.

Right?

Just go ahead and skip it right now.

If I go ahead and execute it now, see what is happening.

Zero is getting displayed, one is getting displayed, two is getting displayed.

When I is three.

Again, I'm just saying hey, skip it.

So it has just skipped this if loop, right.

Or the best way will be to print something like this okay.

The number is okay I will write number is over here as I okay.

Now you'll be able to understand this.

Now this pass as soon as we do the pass right at that time, what will happen now?

First of all, see when I is equal to three it only this will get printed.

And we are just going to skip this okay.

Or do nothing as such.

So here you can see 0123.

The number is 334.

Right.

Pass in.

It's just like a null statement.

Suppose I don't have anything to give over here.

I will just remove this and I will just write pass.

Do nothing as such.

Okay.

So this can also be useful.

And again I will talk about it.

What exactly will be the use case over here.

Right.

But most of them if I probably consider pass continue or let's say if I'm probably defining an empty

function and if I define an empty function, and if I internally write write just pass.

That basically means that the function does nothing.

Okay.

So this is some of the amazing things that have been brought by Python.

Uh, if I talk about break, this will be very handy because on a certain condition we are just going

to break this or come out of this particular loop.

We can use break.

Then we have continue.

Then we have pass.

Right now let's talk about nested loops okay.

So let's talk about nested loops.

Nested loop is nothing but a loop inside a loop right.

Let's say I will run a loop for I in range three.

Okay.

And let's say for J in range two.

Okay.

Now what I'm doing.

And let's say I go ahead and print.

Print.

And here with respect to the print statement let me show you how you can use f string also.

So f uh f string is nothing.

But here, uh, I'm basically writing it out and here I'll write I is equal to will be equal to I and

j equal to it will be equal to j okay.

So whenever we use this f string formatted statement to display the variables we have to use this curly

braces.

And uh, in short this is just a formatting option of displaying the string.

I can use this particular string together along with, uh, you know, flower braces so that I can display

that particular variable.

Now, what is exactly happening over here?

See, it is very simple.

Uh, over here, you'll be able to see for I in range of three.

Right.

I'm iterating through another range over here.

Another iterables over here.

Then I'm also running another iteration over here.

Right.

So there are three elements over here.

So first it will run this.

Then it will go inside this.

And it will complete the inner loop.

Right inner inner loop inner inner for loop.

Then it will go to the outside for loop.

So first time when it gets displayed this is going to get executed for the two times.

Then it will going to go and increment the I to two.

Then again it is going to uh run it for two times for this particular loop.

If you don't know, if you don't understand, see over here, I'll show you with respect to the output.

So here initially you can see when I is zero J is zero.

Because initially when we are running this particular loop.

Right.

And then when we go inside this particular loop J will run for two times.

So j is running for j is equal to zero, j is equal to one.

Then you have I is equal to one.

Then again j is equal to zero, j is equal to one.

Then you, when I is incremented to two, j is equal to zero and j is equal to one.

So it is basically going to run with respect to all the inner loops.

Right.

And here this for loop, every time it will be executed based on the number of range that I've actually

given over here.

Right.

Whenever we enter the upper for loop itself.

Right.

So this is just an example of for loops over here.

Uh, sorry.

Nested loops over here right now.

Let us go ahead and see some examples okay.

And this is where we will practice multiple things.

Uh, the first examples that we are going to do is that, uh, let's say I am going to write over here,

calculate the sum of first and natural numbers using a while loop, using a while and for loop.

Okay.

So let me just go ahead and first of all show you with the help of uh while loop okay.

So first we'll see with respect to the while loop.

And then we will go ahead and see with respect to the for loop okay.

What we need to do calculate the sum of first n natural numbers.

Okay.

First n natural numbers.

Very simple.

So now I will just go ahead and say, let's say that the number of n number the natural number is ten.

Then initially I will define my sum variable to zero.

This will be my temporary variable because the addition that I'm going to do with respect to all the

natural numbers, I'm going to save it in this particular variable called as sum.

Then I will keep this temporary variable called as count is equal to one okay.

Now let's go ahead okay.

So here I'm going to write while okay count is less than or equal to n right.

Unless until the count is less than or equal to n I'm going to just go ahead and I'm going to use this

sum is equal to sum plus count right.

So what we are doing over here we keep on adding the count.

Right.

Unless and until this is not equal to less than or equal to n.

And after this we will go ahead and write.

Count is equal to count plus one.

We are incrementing the count variable also.

And finally, when this for loop is a while loop is getting completed.

I will write sum of first ten natural numbers.

Okay, natural numbers will be equal to nothing but whatever sum we are probably getting over here,

right?

Just go through the statements here.

We have initialized how many number of natural numbers we are going to consider.

Initially the sum is equal to zero.

Count is equal to one.

Now I'm saying while count is less than or equal to n, I'm going to increment this count continuously

unless and until this gets satisfied then automatically internally we are doing the sum also okay.

So here you can actually see the sum of first n ten.

Natural number is nothing but 55 perfect.

So this is just like one plus two plus three plus four plus five plus six plus seven plus eight plus

nine plus ten.

Right.

Uh, it will not go.

Yeah, it will go till ten because we have written less than or equal to n.

Okay.

Perfect.

So this was one of the example.

Let's do it the same thing with the help of for loop.

So I will write.

Uh, so let me just go ahead and define this three variables again okay.

So let's say for I in range.

And here also I can just go ahead and write till 11 because I want to probably do from zero to 0 to

10.

Okay.

And here I'll just go ahead and write sum is equal to sum plus I.

That's it.

Right.

And here I don't even have to write.

This count is equal to one okay.

Because automatically this will get integrated in incremented.

So here let me just go ahead and print the sum.

And if I go ahead and execute I'm also able to get it 55 okay.

So here I've shown you with the help of both while and for loop how you can calculate the first ten

natural numbers sum.

And here you are able to see it.

Okay.

Now let me do one thing.

Let me show you one more example.

Okay, now this time the examples will be.

Talk about the prime numbers or display the prime numbers between 1 and 100.

Now what is prime number?

Prime number are something which is divisible by one or the number itself.

Right.

Now, um, here I'll just go ahead and write it down.

And again for this I will use a for loop.

So I'll write for num in range of one comma 101.

Right.

Because we need the numbers between 1 and 100 right.

If the first condition will be that I will go ahead and write if num is greater than one, right.

Obviously the number has to be greater than one.

So one condition is over here.

We're going to use if nested if nested for loops.

And.

All right.

Please pause the video, try it by yourself and then probably see the solution.

Okay.

Now if this is true then what I'll do for I in range two comma num okay.

Uh for I in range two comma numb.

That basically means from this number from two to this particular number, whichever number we are specifically

discussing, or from this for loop, which number I'm able to increment, I will just go ahead and write

this particular condition.

If num percentile I write, I is the same number over there, right is equal to zero.

Then we are just going to break it okay.

And then we are just going to break and come outside this for loop.

And I'm going to say else print number okay.

We just need to print this.

Because if this gets satisfied right.

This is basically indicating that hey I've got a prime number.

Right.

And then it is just going to display the prime number.

So again I'm repeating first of all I'm going to check a condition.

If number is greater than one then we are going to write for I in range of two comma num okay two comma

num.

So we are incrementing the so so we are running through this particular two comma num whatever num is

there.

Let's say the num is three.

So two comma three for range in two comma three.

Then we can go ahead and write three percentile two is double equal to zero.

The answer is no right.

If it is no we are just going to go ahead and display this number right.

And if it breaks it is just going to go outside this particular for loop.

Okay.

So that basically means if this condition is becoming true right.

That basically means it is not a prime number.

Otherwise we are just going to display the number in the else block okay.

And one more thing about for loop is that along with the for loop also you can write else block right

else block if something uh you don't want to execute it, but you want to execute compulsory at the

end of the for loop.

So you can also use this else block okay.

So once I execute this here you'll be able to see two three.

So two is the prime number three is a prime number five seven is a prime number 11 1317 1923, 29.

All these are prime numbers.

You can probably go ahead and check it out okay.

Uh, these are like numbers which are only divisible by one or the number itself.

Right.

So here you can actually see the example.

Okay.

Now some more examples that you will be seeing as we go ahead where we'll be using when we learn more

about different different data structures like list and dictionary.

But at the end conclusion that I really want to give after every lesson.

Right.

And let me make a markdown cell over here.

Okay.

So conclusion is that loops are really powerful okay.

Loops are definitely very, very powerful.

Okay.

Um, in Python that allows you to execute block of code multiple times by understanding, using for

and while loops along with the loop control statement like break, continue, and pass.

You can handle a wide range of programming tasks efficiently, and you'll be seeing that when we will

be discussing about more examples.

But I really want to keep the video between 20 to 25 minutes, where I show you multiple examples where

I write each line of code in front of you so that you'll also be able to understand.

So yes, this was it from my side.

I'll see you all in the next video.

Thank you.


