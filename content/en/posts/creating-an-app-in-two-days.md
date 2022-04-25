---
title: "Creating software in two days: Lansing GiveCamp Retrospective"
date: 2009-05-24T12:00:06+09:00
draft: false
tags:
  - tdd
  - agile
image: /images/posts/two-days/two-days-software-icon.png
---

At [Lansing GiveCamp](https://web.archive.org/web/20100424092250/http://lansinggivecamp.org/) I was chosen to lead a team tasked with creating a guest registration system for [Ronald McDonald House of Mid-Michigan](https://web.archive.org/web/20100424092250/http://rmhmm.org/) . Ronald McDonald House wanted to get off their current system, paper, to streamline their processes and report on their data. The event started around 7:00PM on Friday and ended with 3:00PM on Sunday. That’s 44 hours.

At first it seemed too simple and I wondered if Microsoft Access wouldn’t have been sufficient for their needs. That is until [Jay Harris](https://web.archive.org/web/20100424092250/http://twitter.com/jayharris) met with the client/charity and hammered out the Business Requirements. Whew, there were a lot.

![Talking over the ERD](/images/posts/two-days/software-in-two-days.png)

Friday night came and we start the project. First, we defined the domain entities. We had no time to lose so with the domain defined Jay started creating business entity classes while I talked with [Dave Giard](https://web.archive.org/web/20100424092250/http://www.davidgiard.com/) and [Eric Vogel](https://web.archive.org/web/20100424092250/http://twitter.com/vogelvision) more about the system architecture.

With the business entities ready and three developers wanting to get started at once, how do we get everyone productive? There’s no database, no DAL… This is where Inversion of Control paid out nicely. I whipped up some fakes to return some hard-coded objects so the team could consume those until the actual database was ready. 

```csharp
  public class FakeStaffMemberService : IStaffMemberService {
    private List<StaffMember> staffMembers = new List<StaffMember>() {
      new StaffMember() {Id=1, UserName=“JSmith”, FirstName=“John”, LastName=“Smith”, 
        Type=StaffType.Admin},   
    // …
   
    public IList<StaffMember> GetAll() {return _staffMembers; }
    
    // …
```
 
Then I told our IoC Container, StructureMap, to return a FakeStaffMemberService whenever an IStaffMemberService was requested. And yes, with proper Inversion of Control and TDD, it doesn’t matter that the database doesn’t exist in your controllers and middle-tier classes, but we had a lot of views and JavaScript to get written so it was important to hit F5 and see our website.

For the Data Access Layer, I grabbed Fluent NHibernate and fumbled getting automapping to do what I wanted. It was one of those situations where I couldn’t tell if I was five minutes or five hours away from getting the thing to work… so I tossed it and went with normal Fluent NHibernate mappings. It was somewhat tedious but a predictable and manageable task. With a Greenfield database, Fluent NHibernate is perfect. Were we dealt existing schema, I would’ve feared a situation arising I couldn’t map with Fluent, but this wasn’t an issue here.  Fluent NHibernate makes the mappings strongly typed and [trivial/beautiful](https://web.archive.org/web/20100424092250/http://code.google.com/p/rmh/source/browse/trunk/RMH.DataAccess/Mappings/StayMap.cs) while providing helpers for [testing your mappings](https://web.archive.org/web/20100424092250/http://code.google.com/p/rmh/source/browse/trunk/RMH.IntegrationTests/Repository/PatientRepositorySpecs.cs) . Along with that, I created a “ [test](https://web.archive.org/web/20100424092250/http://code.google.com/p/rmh/source/browse/trunk/RMH.IntegrationTests/Repository/CreateSchema.cs) ”, set to run explicitly, to create the schema and populate the database. This let us never need to open SQL Server or even think about its existence.  In order to persist a new property, we simply had to add it to the mapping and add a line in our integration test for verification. This led to a less than ideal schema but functioning software was our concern. Later, when the dust settled and product was delivered, Eric and I wrote a [script to optimize the schema](https://web.archive.org/web/20100424092250/http://code.google.com/p/rmh/source/browse/trunk/RMH.DataAccess/AdoNet/Scripts/DDL-Update.sql) .

<!-- TODO: put the ERD back here? -->
<!-- [image:6A9DB9E4-4834-47FA-91BA-118884317A66-36973-0000026015BE5B75/Attachment.png] -->


This infrastructure allowed us to just rip through code all day Saturday… which was good because we were hindered by multiple power outages, a restocking trip required by myself to replace clothes and toiletries stolen from my car the night before and some fumbling trying to figure out an ASP.NET MVC binder solution.
With an hour and a half to go to our demo, I realized I had well over two hours of work to do. The main feature of our application, recording a patient’s support people and their stays was not going to be complete. I still had to code the binder and the JavaScript to handle multiple support people.

I was sure trying to explain what I needed to someone would be insufficient for them to comprehend and return what I wanted. I started plowing through it, hoping maybe I could come in under the wire when I saw an out. I knew what the Act and Assert was in my Unit Test. I wrote them, checked it in and asked [Dennis Burton](https://web.archive.org/web/20100424092250/http://twitter.com/dburton) for an hour of his time to fill out the Arrange part of the test along with the implementation. There were three failing tests and I needed them all to be green. He downloaded the project and because of our use of Inversion of Control he did not need to set up the database or know anything about the rest of the domain. An hour later he checked in the code and because all of the tests passed I didn’t even care about looking at his implementation. Dropping it into the project was the missing piece and we were done with about fifteen minutes to spare.

![Presentation](/images/posts/two-days/two-days-presentation.png)

--

[Photos by David Giard High-Quality Photography](https://giard.smugmug.com/)

