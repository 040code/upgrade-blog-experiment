---
layout:     post
category: "General"
title:      "GraphQL"
subtitle:   "Nextbuild talk - The Next API Language"
date:       2017-05-20 23:50
authors:     [niek]
header-img: "img/radioroyaal.png"
tags:       [graphql]
---

A short post to share the slides and examples I used in my talk at the [Nextbuild](http://nextbuild.nl/) conference on May the 20th in Eindhoven.

## Slides
Below the slides that I for the talk, the slides are available as well on [GitHub](https://npalm.github.io/graphql-slides-20170520/). You can easy navigate through the slides with the spacebar.

<div style="position:relative; width:100%; height:0px; padding-bottom:56.25%;">
    <iframe style="position:absolute; left:0; top:0; width:100%; height:100%"
        src="https://npalm.github.io/graphql-slides-20170520/">
    </iframe>
</div>

To get started with GraphQL the best starting points are:
- [GraphQL.org](https://graphql.org)
- [Awesome GraphQL](https://github.com/chentsulin/awesome-graphql)

## Examples
During the talk, I demonstrated GraphQL via [graphcool](https://www.graph.cool/), which is cloud service for creating a flexible GraphGL backend. I modelled a basic model of a Talk and Person with relation speakers and visitors on graphcool. Furthermore, I modelled two basic sample implementations of a GraphQL backend in Java and JavaScript that are available via GitHub. Those implementation are more limited than the online one, but both serve the following minimal queries.

Query for the name and the title of the talks given by all persons:
```
{
  persons {
    name
    talks {
      title
    }
  }
}
```

And secondly, a query for all titles of talks with their speaker's names.
```
{
  talks {
    title
    speakers {
      name
    }
  }
}
```

### JavaScript sample
The JavaScript [sample](https://github.com/npalm/graphql-js-demo.git) is based on [Apollo GraphQL tutorial kit](https://github.com/apollostack/apollo-starter-kit).

```
git clone https://github.com/npalm/graphql-js-demo.git
cd graphql-js-demo
yarn && yarn start
```
Instead of yarn, you can use `npm install && npm start`. Once started, browse to [http://localhost:8080/graphiql](http://localhost:8080/graphiql) and play around with the GraphQL web interface. Implementing the JavaScript version was straightforward due to the many examples and good tutorials around.


### Spring Boot Java sample
The Spring Boot Java [sample](https://github.com/npalm/graphql-java-demo.git) is based on the Spring Boot Starter available for GraphQL. This starter uses a basic GraphQL java library as well the Java annotation library for GraphQL.
```
git clone https://github.com/npalm/graphql-java-demo.git
git checkout nextbuild
cd graphql-java-demo
docker build -t graphql-java-demo && docker run -it --rm -p 8080:8080 graphql-java-demo
```
Alternatively, you can build and run via gradle. Once started, browse to [http://localhost:8080/](http://localhost:8080/) to play around with the GraphQL web interface. The Java version implementation was not as easy as expected. The GraphQL Spring Boot starter dependencies requires the GrahpQL java annotation library, which seems to be broken after an update in the Java GraphQL base library. I am not sure if the annotation library is still supported. To get the GraphQL Spring Boot library working I have to add a mandatory mutation to the scheme. And downgrade the Java GraphQL, see `gradle/depedencies.gradle` to get the annotation library to work.

Many languages already have support, so feel free to try out your favourite language. Currently the support on JavaScript looks like by far the best.

## Updates

### Refactored Java implementation (June 20, 2017)
I have updated the Spring Boot implmentation, upgrade all libraries and removed the annotations for graphql resolving. The annoation are replaced [java-graphql-tools](https://github.com/graphql-java/graphql-java-tools). Which looks a better way to ingrate graphql in a Java service. You will see the implementation will have a lot of similarities with the javascript one.

### Developers.nl meetup Rotterdam (June 28, 2017)
On June, the 28th I have presented the GraphQL talk at the [developers.nl Meetup](https://www.meetup.com/Developers-nl-Meetup/events/240419508/) in Rotterdom. I have used a slightly minimal version for the slides, which can be found [here](https://npalm.github.io/graphql-slides-20170628/). Comparing the to the presentaton on the nextbuild I have also walked through the code examples mentioned above.
