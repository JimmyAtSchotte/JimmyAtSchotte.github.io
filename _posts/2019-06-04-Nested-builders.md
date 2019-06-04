---
title: Nested builder-pattern
description: How to build a builder that starts another builder
categories: blog
ingress: About six months ago, I faced a task where I wanted to chain multiple builders after eachother (a chain of 3 builders actually). I completed the task, but the implementation were real ugly. Today I refactor that code, using this pattern.
---
# Nested builder
About six months ago, I faced a task where I wanted to chain multiple builders after eachother (a chain of 3 builders actually). I completed the task, but the implementation were real ugly. Today I refactor that code, using this pattern.

## First, what is a builder?
The builder pattern is responsible to create an object and set it's properties. It's quite simple in it's simple form, where you have set methods for the properties of an private variable and every method just return itself (this). Finally you have a Build method that returns the object that has been built with the set methods.

```csharp
//Entity
public class Person
{
    public string Firstname { get; set; }
    public string Lastname { get; set; }
}

//Builder
public class PersonBuilder 
{
    private readonly Person _person;

    public PersonBuilder()
    {
        _person = new Person();
    }

    public PersonBuilder SetFirstname(string firstname)
    {
        _person.Firstname = firstname;

        return this;
    }

    public PersonBuilder SetLastname(string lastname)
    {
        _person.Lastname = lastname;

        return this;
    }

    public Person Build()
    {
        return _person;
    }
}

//Implementation
var person = new PersonBuilder()
                        .Firstname("John")
                        .Lastname("Doe")
                        .Build();
```

## Adding nested builders
Consider that we want to add children to the Person entity above. It can be accomplish by having a Set method with `Action<PersonBuilder<>` as an argument:

```csharp
//Entity
public class Person
{
    ...
    public List<Person> Children { get; set; }
}

//Builder
public class PersonBuilder 
{
    ...

    public PersonBuilder AddChild(Action<PersonBuilder> builder)
    {
        var personBuilder = new PersonBuilder();
        builder(personBuilder);

        _person.Children.Add(personBuilder.Build())

        return this;
    }
}

//Implementation
var person = new PersonBuilder()
                        .Firstname("John")
                        .Lastname("Doe")
                        .AddChild(child => {
                               child.Firstname("Jane")
                                    .Lastname("Doe")
                        })
                        .Build();
```

## Final word
In my PersonBuilder example, I reuse the same builder. I did so to keep this post a bit shorter, but you can use this pattern to chain any type of builder. 
