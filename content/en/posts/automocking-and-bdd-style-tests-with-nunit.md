---
title: Automocking and BDD style tests with NUnit
date: 2009-05-31T12:00:06+09:00
description: Automocking with NUnit takes the pain out of mocks
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tags:
  - csharp
  - tdd
---

I’m currently using context/specification style tests. While I think frameworks like J.P.Boodhoo’s are beautiful, I prefer something that works with ReSharper, TD.NET and CI without extra hurdles. I also want something my team, with limited exposure to *Unit frameworks, can easily pick up.

I’d prefer not to have the ceremony and misleading terminology of “Test” attributes, but its a trade-off I’m willing to make to more easily to integrate with team members and third party tools.

I put my testing stack along with an example test/spec project on github under the project name  [Specish](https://web.archive.org/web/20170115024708/http://github.com/ignu/specish/tree/master) .
About my tests/specs:

1 [image:3957684B-8C76-48EE-B578-702C8D248913-36973-0000019AF7B13069/resharper_navigation_thumb.png]	

*	I preface every test fixture with the name of the class I’m testing. This lets me type “PC” in the navigation window of ReSharper to get to a PatientController or any class that tests patient controller.
* Automocks allow me to change constructor signatures with no consequence, and let me only mock objects and methods necessary for setup or verification. I stole the base class for my tests from  [here](https://web.archive.org/web/20170115024708/http://code.google.com/p/moq-contrib/wiki/Automocking) .
* I usually only have one assert per test method.
* I use a  [modified version](https://web.archive.org/web/20170115024708/http://github.com/ignu/specish/blob/95905fc980d208e6391c08e2a176bc83b4ceea3c/Specish/nunit_spec_extensions.cs)  of SpecExtensions I saw  [Steve Harman](https://web.archive.org/web/20170115024708/http://stevenharman.net/)  use at Cleveland Day of .NET last year… so instead of Assert.IsTrue(true) I write the more readable true.ShouldBeTrue();
* Custom ReSharper live templates for  [test fixtures](https://web.archive.org/web/20170115024708/http://pastie.org/496274)  and  [methods](https://web.archive.org/web/20170115024708/http://pastie.org/496275)  speed things up considerably.

The result looks something like this:

```csharp
[TestFixture] 
public class PatientController_when_searching_for_patients_returns_one_result : base_automock_test 
{ 
    ViewResult result; 
    IList<Patient> patients = new List<Patient>(); 

    public override void establish_context() 
    { 
        patients.Add(new Patient{Id = 2}); 

        Mock<IPatientService>() 
            .Setup(ps => ps.Search(It.IsAny<string>(), It.IsAny<string>())) 
            .Returns(patients); 
    } 

    public override void because() 
    { 
        result = Create<PatientController>().List("Joey", "Smith"); 
    }   

    [Test] 
    public void it_returns_just_one_patient() 
    { 
        (result.ViewData.Model as Patient).ShouldEqual(patients[0]); 
    } 

    [Test] 
    public void it_returns_the_detail_view() 
    { 
        result.ViewName.ShouldEqual("Details"); 
    }  
}
```

And it shows up in the test runner as

> PatientController when searching for patients returns one result
>   * it returns just one patient
>   * it returns the detail view

 
The test runner results document exactly how my controller behaves in this context.

PatientController returns just one patient and a detail view **because** I call `List()` on a`PatientControlle` in the **context***(search the returns one result)*set in establish_context.

