---
layout: post
title: "Beyond The Code: PyTennessee 2016 Keynote"
description: ""
category: development
tags: [pytennessee,python,development,programming]
---
I was invited to give the closing keynote at PyTennessee 2016. Jason Myers,
Denise Myers, Will Golden, and the crew of volunteers continue to do an amazing
job putting on this conference. I'm grateful for all the work that Jason, in
particular, puts into this conference. I got front-row seats during his work on
the first conference, so I got to see how much work is involved in making a
regional conference happen. It's a herculean effort.

<div class="pull-right img"><img src="/img/2016-keynote-250.jpg"><small>Image credit: <a href="https://twitter.com/egdelwonk/status/696479086093459456">Will Golden</a></small></div>
I owe a huge thanks to Jason Myers for giving me the opportunity to speak. I owe
another thank you to all of the folks who stuck around for my talk - it was, after
all, the final talk of a long weekend and it bumped up right against the Super
Bowl.

Here is the text of my talk. I did not use any slides, other than rotating
through some nice Impressionist art.

### We Are All Creators

In the spring of 1928, Walt Disney and Ub Iwerks were at the end of their
rope. Six months ago, they had created one of the most popular animated films in
the country - rivaling Felix the Cat and Koko the Clown. The problem, however,
was that the film's main character did not belong to them.

The character, Oswalk the Lucky Rabbit, belonged to Universal Studios.

Since Universal owned the character, they could demand a lion's share of the
profit. Walt made the trip to New York City to try to strike a bargain with
Universal - he wanted his company to enjoy a more significant share in the
Oswald's success.

Universal, however, would not budge. If Walt walked away from the character,
they threatened to poach all his employees and continue marketing Oswald without
him.

On his trip back home, Walt came up with an idea for another character: Mickey
Mouse. In May of 1928, Disney and Iwerks released the cartoon they had
been working on in secret: Mickey Mouse's "Plane Crazy." It immediately surpassed
Oswald the Lucky Rabbit in popularity and the Disney company went on to become
what we know today.

What can we learn from this story?

Cesar Hidalgo of MIT (author of "Why Information Grows") wrote about this story,
saying, "Oswald’s story teaches us that what is most valuable in an economy
is not what authors make, but their ability to make it. [...] While legally,
Universal owned Oswald, technically they did not own the capacity to author
characters like Oswald. That capacity was embodied in the minds of Disney and
Iwerks, and this was the key factor that set the duo apart."

That capacity - the capacity to create something unique - exists in all of us.
Whether you create with a brush and an easel, a drafting board, vim, or emacs,
you're creating something out of nothing: castles in the sky.

The author of "The Mythical Man Book:  Essays on Software Engineering" Fred
Brooks ruminated on the joys of our craft. The very first thing he mentions is
"the sheer joy of making things" (p. 8). There is a joy in creation.

Fred goes on to point out that beyond an innate joy in creation, there is a
joy in the creation of "things that are useful to other people." We pour much
of our souls into our sky-castles and there's nothing quite so demoralizing
as seeing our effort come to nothing as they crumble from neglect.

(As a parenthetical [hey, it's a keynote, I'm allowed a parenthetical] I have one
PHP application that I wrote back in 2004 that is still happily tracking real
estate appraisals for a small firm in east Tennessee. I take no small
satisfaction in knowing that my simple little application has afforded a small
company to continue growing for over a decade now.)

### The Joys and Woes of Software Development

But, as Fred Brooks points out in his classic book, not all is unicorns and
puppies. There are woes in our craft, too. Some of the woes that Dr Brooks
mentions:

- Computers do exactly what we tell them to do. This is true in that each
  incantation must be uttered with utmost specificity and clarity. If we don't
  communicate our intentions correctly, we introduce all kinds of errors.

- "Other people set our objectives, provide our resources, and furnish our
  information." We are at the mercy of those who are communicating requirements
  to us, often filtered through third or even fourth parties.

Dr Brooks wrote about these joys and woes over forty years ago, in 1975. What's
remarkable to me is that any modern developer can affirm that these joys and woes
still apply to our day-to-day work.

What I also notice about these woes, in particular, is that they are completely
unrelated to your choice of language, platform, editing tool, operating system,
library, or any of the other things that we spend an inordinate of our time on.

In fact, I would argue that it's easy to fall into a trap of spending _too_ much
time on these things. We work in a trade that emphasizes self-directed learning
as an absolute necessity. It attracts those that are intellectually curious.
We're always looking for ways to improve our ability to build better programs.
This is all well and good - our intellectual curiosity leads us to hone our
skills and build new and useful tools or make improvements to existing ones.

However, I think it's easy to get stuck in the technical weeds. This is akin to
a painter spending a majority of his time debating which kind of paintbrush to
use, or which brand of canvas he should employ.

Resources: 

  - [Think Like an Author, Not an Owner](https://hbr.org/2015/10/think-like-an-author-not-an-owner)

### The Development Forest

Fred Brooks wrote another famous essay in 1986 titled "No Silver Bullet." In it,
he makes the bold claim that "there is no single development, in either
technology or management technique, which by itself promises even one order of
magnitude of improvement in productivity, in reliability, in simplicity."

Brooks puts the tasks of software development into two buckets, _essential_ and
_accidental_.

- Our essential task is building the detailed conceptual structures that make
  up the business rules. These are the same regardless of your chosen
  architecture, language, or library.
- Our accidental task is representing these abstract structures in a language
  the machine can read and execute.

Brooks argues that "the hard part of building software [is] the specification,
design, and testing of the conceptual construct, not the labor of representing
it and testing the fidelity of the representation." That is to say, most of our
work occurs in the essential task of gathering requirements, building
specifications, etc. Less of our time is spent in the accidental task of
representing those specifications in machine-readable language.

Peopleware, a book that Brooks described as "one of his two favorite books on
software engineering" puts it this way:

> The business we are in is more sociological than technical, more dependent on
> workers' abilities to communicate with each other than to communicate with
> machines. (p. 105)

If this is indeed true, then this means that
improvements to existing languages and libraries are incremental at best. We
should be putting more of our efforts into building other skills that allow us
to become better at dealing with the _essential difficulties_ of software
development.

This is not to say that spending time improving our ability to handle the
accidental difficulties is a waste. Indeed, as we are getting started in the
trade this is the best place to invest our time and effort. Our first hurdle is
to write instructions that a machine can understand. From there, we perhaps move
on to writing clearer, more maintainable code with fewer errors. (Books like
["Code Complete" by Steve McConnell](http://amzn.to/1lxvc8m) and ["Clean Code"
 by Bob Martin](http://amzn.to/1S5UeZ0) are excellent
treatises on improving these skills.) Eventually, we add additional languages to our
arsenal, giving us the added benefit of looking at the languages we already know
in new ways.

From there, however, things become unclear. What takes us from a developer that
writes great code to a developer that builds amazing products? To put it
simply, what happens when a junior developer becomes a senior developer?

Indeed, what makes a _good_ developer? Is it writing clean, maintainable,
error-free code? Or, perhaps, could we take a step back from that and ask
ourselves: Are we building the right program? That is to say, do we even have
the right specifications?

Here we see ourselves debugging not the code, but the specifications. Our
ability to communicate with our stakeholders (our users, our team members)
becomes much more important.

Perhaps we can zoom out from simply debugging the specifications.

What can we as team members and, perhaps, team leaders encourage strong teams
where the whole is greater than the sum of its parts?

Or, zooming out even further: how do we encourage communities that foster
great developers, great teams to work with, and great companies to work at?

How do we encourage a trade that embraces a long-term outlook - a trade that
values ethical decisions over financial gain?

It may seem as if I've gone off the rails here, but I believe that this macro
vision has a profound effect on the micro level. The macro is the trade we work
in, the community in which we live, the employer we work for, and the team we
work together with. It sets the context for us to perform our work. It sets the
tone for our work and determines our ability to feel connected, valued, and
fulfilled as humans.

If you accept that this is true, then you must agree that it is important that
each of these layers work well in ways that push the roots of software development
(that is, the building of conceptual structures that we then translate into
machine-readable instructions) to succeed.

Imagine the accidental complexities of software development as the tips the
roots of a tree, deep in the soil. We could imagine the rest of the essential
difficulties as a tree.

A tree is insufficient. It's bigger than that. It's an entire forest.

What I want to talk about today is our place in that forest.

How can we *leave the place better than we found it*?

Additional resources:

- [Programming Language Productivity
  Comparison](http://www.connellybarnes.com/documents/language_productivity.pdf)
- [No Silver Bullet, Fred
  Brooks](http://worrydream.com/refs/Brooks-NoSilverBullet.pdf)

### Mapping the Forest

If we had a map of this forest, what would it look like?

- Ourselves
- Teams
- Employers
- Community
- World

Each of these are building blocks - they are interdependent on one another.

### Ourselves
-------------

The number of ways to grow as a software developer is equal to the number of
developers. As I was working on this talk I thought about talking about all
kinds of different things here: how to improve cognitive performance (learning
to learn), avoiding cognitive biases, becoming a craftsman...  ultimately none of
these fit the talk because this is a talk about the social side of software
development: relationships.

You have daily interactions with your immediate team members. You talk to folks
in other departments about what they need from your team. Hopefully you also
find time to talk to your end-users.

All of that talking requires some serious communication skills. Before we can
get started on our sky castles, we need a conceptual model of what they're going
to look like. It seems silly to say this because it's listed as a requirement on
nearly every job out there, but good communication skills are pretty vital to
our trade. A software developer with no ability to communicate is going to have
a pretty hard time building anything useful for anyone other than herself.

How do we get better at communicating?

- Ask more questions and seek feedback. Good software developers are great
  listeners. They are not only listening to the words that are being said, but
  they are reading between the lines looking for clues as to what their users
  really need. Even when talking to a product manager or designer, they listen
  and ask clarifying questions about the specifications as they are being
  delivered. When you first get started in a software development career, you
  may not even know what questions to ask, but as you grow in the trade you find
  that you can sense design gaps long before you start writing actual code.
  This requires a nice dollop of humility.
- Communicating well requires minimizing distractions. I confess that this is
  a constant struggle with me.  As a millennial (also known as a snake person)
  I, like you, was born into an environment that is constantly
  demanding context switches. It's easy for us to lull ourselves into thinking
  that we can pay attention to someone talking while we're answering a text
  message or scrolling through Twitter. The science is pretty solid on this:
  when we spread our attention across several things, we do none of them well.
  Furthermore, [multi-tasking damages our ability to
  focus])http://news.stanford.edu/news/2009/august24/multitask-research-study-082409.html).
  It is terrifying to think that this habit can destroy focus - arguably one of
  the most important abilities of a software developer.
  It also sends a signal to the person or persons that you're talking to that
  their time is not valuable.
- I won't spend a lot of time on this because I know Scott Burns did a great job
  covering it in his talk, "Empathy as a Service." The ability to listen is
  great. To read between the lines, though, you often have to be able to place
  yourself into the shoes of others. We had a client once who told us that that
  he was having a terrible time updating his reports after we published some new
  data. We asked to see what the trouble was, and he showed us how he would
  print out Excel spreadsheets onto 14" long legal paper, whipped out a
  calculator, and proceeded to write down a cumulative sum in one of the
  columns. With a pen. It was easy for me to immediately wonder how this person
  got out of bed in the morning, but one of my colleagues was gracious enough to
  point out that this fellow had no experience with analysis. Due to some staff
  cuts, he was a marketing person who had been shoe-horned into a position he
  knew nothing about. Knowing that I was able to step away from my momentary
  shock and dismay and take a moment to help this person do their job.

Enough about ourselves. Let's start talking about how we interact with the
forest around us.

### Teams
---------

Working with a team is one of the most complex things a software developer will
do. People are complicated. Every person is different, therefore every team is
different.

First, what does a team look like? A "team" is more than just a group of
people who have the fortune (or perhaps, misfortune) to work together. What
makes a group a team?  Tom DeMarco and Timothy Lester call it "jell."

> A jelled team is a group of people so strongly knit together that the whole is
> greater than the sum of the parts. The production of such a team is greater
> than that of the same people working in unjelled form. Just as important, the
> enjoyment that people drive from their work is greater than what you'd expect
> given the nature of the work itself.

These kinds of teams rarely happen by happy chance. Does that mean that a
manager can build a jelled team? Au contraire. Management can create an
environment that allows a team to jell, but they can't make it happen.
Furthermore, when it does happen, good management knows to get the heck out of
the way - their time is better spent moving obstacles out of the team's way than
goading them on with sticks or carrots. Even _Peopleware_'s DeMarco and Lister
couldn't come up with a list of six ways for managers to encourage great teams.
Instead, they ended up building a list of six things *not* to do.

Good teams are grown, not built. This follows nicely with our forest analogy,
doesn't it? Just as you can't force a seed to germinate, you can't force a team
to jell. You can create an environment for it to happen. Furthermore, just as a
plant requires food and water to grow, a team requires ongoing effort to stay
jelled.

You may be thinking: I'm not a team lead - what can I do to help my team jell?
The ability to encourage good teams is not limited to just team leaders.

First, you can *embrace and welcome team diversity*. I'm not just encouraging
this for altruistic reasons. There is real research (detailed by
[NPR](http://www.npr.org/2014/03/21/292225798/does-diversity-on-research-team-improve-quality-of-science))
that suggests that diverse teams perform better. In this study they found that
research papers written by teams with diverse ethnic backgrounds received more
citations than papers written by authors with a similar ethnic background. As
Harvard economist Richard Freeman pointed out:

> Ethnic diversity is an indication of ideas' diversity. People who are more
> alike are likely to think more alike and one of the things that gives a kick
> to science is that you get people with somewhat different views.

If science can get a kick from a team with ethnically diverse backgrounds, is it
much of a stretch to assume that diverse software development teams would
receive the same benefit?

DeMarco and Lister also point out in _Peopleware_ that a diverse team can send
a "clear signal that it's okay not to be a clone, okay not to fit into the
corporate mold of a Uniform Plastic Person."

Of course, to encourage diversity on your team it certainly helps to have some
diversity in our trade. We'll talk about that later.

Next, teams should *discourage hero worship*. Perhaps you've been on the team
where there's one person that everyone is in awe of. They sling code that no one
else understands, rescue projects that have fallen behind, and they enjoy a
level of autonomy that no one else on the team seems to get.

There are a couple of reasons to avoid having this mentality on your team.
One is that hero worship is a symptom of a fixed growth mindset.
A fixed growth mindset makes the assumption that a hero got that way because
they have innate talents that you can't replicate. [Allison
Kaptur](http://akaptur.com/blog/2015/10/10/effective-learning-strategies-for-programmers/)
did a great job of [explaining this at Kiwi
Pycon](https://www.youtube.com/watch?v=Mcc6JEhDSpo).
A fixed mindset has a detrimental effect on the ability of individuals to
learn and grow. A growth mindset, on the other hand, helps us remember that
skills are not innate, but can be grown with applied effort. This dovetails into
the oft-talked about "imposter syndrome." As Allison puts it:

>  Julie Pagano did a great talk at PyCon 2014 about impostor syndrome, and one
>  of her suggestions for a way to combat impostor syndrome was "kill your
>  heroes." Don’t put other programmers on a pedestal, don’t say "that person is
>  so different from me."

The second issue is that it gives too much weight to the hero's voice while
disenfranchising those who may have less experience. To illustrate this point,
I'm going to tell another story.

In 1977, the Citicorp Building (now known as Citigroup Center) was completed. It
features some startling architectural features, particularly at the base of the
building ([here's a
photo](https://en.wikipedia.org/wiki/Citigroup_Center#/media/File:Citigroup_center_from_ground.jpg).
The entire 59-story building is elevated on stilts, but not just any stilts. Due
to a church in one corner of the property that could not be removed, the 9-story
stilts were placed in the center of each wall. This created some challenges in making
sure the building was structurally sound. The building is built with chevron
braces, which made it lighter than a normal skyscraper. This made it more
vulnerable to wind. To deal with that, the architect added a tuned mass damper
- one of the first ever built.

A year after it's completion, a student at Princeton University, Diane Hartley,
was reviewing the project as part of her civil engineering studies. She found
that the building architects had run all of their tests with wind coming
directly against the building faces (north, south, east, and west). What they
had not tested, however, was wind coming from one of the corners. By her
calculations, a strong wind against a corner would cause the building to lose
it's structural integrity.

That is, the building would topple over.

Now, I don't know about you but when I walk down the streets of Manhattan I
certainly don't expect a building to tumble down in a strong wind.

Ms. Hartley did not believe that her calculations could be correct, so she
brought them to her professor. Her professor then passed them along to the
building architect, William LeMessurier. Fortunately, LeMessurier realized he
had made a glaring mistake and rushed to correct it.

Without informing the citizenry of New York, the problem was corrected by adding
some additional bracing to the building, and a major disaster was averted.

This entire story remained unknown until a _New Yorker_ expose was published
in 1995. There's also a great podcast about it from [99 Percent
Invisible](http://99percentinvisible.org/episode/structural-integrity/).

LeMessurier was a great architect but if it were not for the voice of a student
lives could have been lost. If the student had engaged in hero worship and had
not alerted the architect to the issue, the story could ended very differently.

That's one kind of hero: the hero as the unquestioned expert. Another kind of
hero, the corporate hero, might look a little different. We've probably all seen
it - the one person who spent a whole weekend saving a project that went awry.
That kind of hero worship has an awful tendency to encourage bad
incentives. If someone has to spend all weekend knocking out an overdue project,
something went terribly wrong. That contribution should be appreciated, but
there needs to be some discussions what went wrong. Was the deadline
unrealistic? Were the specifications incomplete? Something else? If someone is a
corporate hero, that's a great opportunity for some management introspection.
Why did we need a hero?

The third thing you can do to create an environment for your team to grow is to
*encourage a culture of craftsmanship*. It's very difficult for a team to form
around the idea of "good enough" work. Indeed, poor quality work has a long-term
human cost in that team members become less and less enthusiastic about their
work with each slapdash project.

Craftsmanship doesn't necessarily mean that we're building cathedrals of
perfection. Gold plating can be just as harmful as leaving work unfinished.
We still live and work in a market society that has to ship projects
before our competitors. What it does mean, however, is balancing speed of
delivery with sound development practices.

One way to encourage this culture is to encourage *peer coaching*. If a team has
a culture of craftsmanship, team members feel it is acceptable to consult one
another for development advice. As DeMarco and Lister point out, the team lead
can't know everything and often team members have a mix of complimentary skills.

For peer coaching to thrive, however, you need an environment where members don't
feel inadequate for asking for help. A highly competitive atmosphere among team
members will discourage knowledge transfers that are important to the longevity
of the team.

There are a number of other ways to encourage the growth of good teams, but
these three will go a long way. If you're interested in this subject, I highly
recommend Tom DeMarco and Timothy Lister's book _Peopleware_.

Other resources:

- [How to Grow Effective Teams](https://www.thoughtworks.com/insights/blog/how-to-grow-effective-teams)

### Employers
-------------

One afternoon when I was returning from a lunch-time run with my colleague Matt
George. Our new office was still under construction and the facade was covered
up with scaffolding. As we rounded the corner to the front of the building I was
looking up at he scaffolding in order to assess if we could get through the
front door or if we were going to have to circle around to the rear entrance. As
I was looking up, I took two steps into the wet concrete that had just been
poured for the new sidewalk.

My colleague, thankfully, was not looking up and managed to stop short of the
mess.

The general contractor was considerably annoyed by my misstep.

"What kind of an idiot," he vociferously inquired, "doesn't know what wet
concrete looks like?"

My co-founder, Jason Moore, said "Every person is an idiot outside of their
context."

Now, leaving aside the fact that the contractor didn't properly leave any kind
of visual signage that would have warned me about that wet concrete, Jason's
response stuck with me.

One of the most grevious errors I've seen from developers in general is making
the assumption that non-developers are inferior beings. You've probably seen it
before. It's so common that it has become a trope. You've probably seen the SNL
"Nick Burns, Computer Guy" sketch. Jimmy Fallon treats his idiot co-workers with
acute disdain, declaring "MOOOOOVE" as they try to explain the problem.

Most developers may not be this bad, but it's easy to fall into this trap of
dismissing the input from non-techies. You'll get a taste for what this feels
like if you travel to a non-English speaking country. Even if you have learned a
little of the language you struggle to communicate advanced concepts. Generous
locals will help you out, but the ungenerous ones may just assume you're an
idiot.

This attitude of superiority is, of course, a cancer. It's counter-productive to
successfully interpreting the needs of your non-technical colleagues. There have
been a few great talks on how important empathy is for software developers. That
applies here, too.

Company culture is admittedly difficult for one person to change. Indeed, even
those in a position of company leadership find it difficult to do so. Even
though it's a challenge, it's worth your consideration for two reasons:

- Your voice, along with others, can encourage change in the long term. At
  worst, your change may be limited to your department or team, but if you
  affect change, it's worthwhile in that it increases your satisfaction with
  your work as well as those around you.
- You may come to find yourself in a leadership position to encourage change
  (perhaps you already find yourself there).

But what is company culture, exactly? If you've worked in industry for long
you've probably heard the term. Have you ever tried to define it? It's pretty
difficult. Some interpret it to mean "company values" or the habits, attitudes,
and processes that exist within a company. That's a pretty broad brush stroke.
It also discounts the fact that culture is something that is a constant state of
change. It changes in ways that are not always easy to observe, but companies
are, after all, made up of people. People are not known to behave in constant
ways. They are constantly changing, thus companies change.

So what is culture? [One writer in Harvard Business
Review](https://hbr.org/2015/04/why-company-culture-is-a-misleading-term) put
it this way:

> I was interested in a paycheck and in order to get that paycheck, I had to
> align my identity with the patterns of behavior and thought expected by those
> who had power over me. (John Traphagan)

That certainly puts it in stark terms. I think it's pretty accurate, though.
Some companies make habits of trotting out platitudes of values for their
employees to consume like some sort of religious wafer:

- We believe in transparency and openness. (Possible interpretation: we read
  your email and watch what websites you visit.)
- We believe in working as hard as we play. (Possible translation: you're going
  to be working long hours, but we have a ping pong table!)

Some companies have the best intent, but I am quite confident that any employee
at a company that is disingenuous about their values will catch on very quickly
as to what their _true_ values are.

If we indeed place value on an idea, our actions will communicate that. If a
company really believes that "their employees are their greatest asset" then you
will see them make significant investments of time and money into their personal
development.

Culture, then, is how a company acts, not what a company says.

Earlier I mentioned that there is research that indicates that a diverse team
performs better than a homogeneous team. That is true, but to really enjoy the
benefits of diversity team members need to feel like they can speak up without
negative consequences.

That, fundamentally, means embracing a *culture of inclusivity*. That means not
only having a diverse set of backgrounds on your team, but also making sure that
their voices are heard and included when making important decisions.
Furthermore, research indicates that this additional step has a huge impact on
the ability of a company to respond to market opportunities that they may be
blind to.

A recent example of this was highlighted by Sylvia Hewlett of the "Center for
Talent and Innovation":

> At Standard Chartered, for example, the insights of one Indian female banker
> translated into innovation that boosted net sales at two branches by 127% and
> 75% within two years. Her insight? Local women—wage-earners, entrepreneurs,
> and purse-string holders—were looking for a more welcoming, less condescending
> experience when they went to deposit money, apply for credit, choose savings
> and investment products, and ask for financial advice. Management endorsed her
> proposal to make over the New Delhi and Kolkata branches into
> all-women-staffed banks. Today, Standard Chartered is the go-to bank for women
> in South Asia.

Sylvia calls this "speak-up culture." Many companies have a tendency to
disparage ideas from people who don't look like them, and this costs them in the
long run. Collaboration suffers, innovation suffers, and risk-taking is
discouraged.

You may not be in a position of leadership, but there are still things you can
do to help encourage voices of others to be heard:

- Don't drown them out. Give them an opportunity to speak.
- Resist the temptation to "well, actually..."
- Encourage management to listen (restate their views, if necessary, with proper
  credit).

One of the experiences that stuck out for me in 2015 was visiting a high school
in north Nashville to talk to a group of students interested in programming. I
was joined by a panel of other developers. Most of the class was made up of
Hispanic and African-American students. The panel was all white guys, save for
one white woman. One of the students, a sixteen year old girl, was not afraid to
name the elephant in the room:

"Looking at this panel full of white guys: do we even have a chance?"

The question made my heart sink. The only answer I could give was that our
industry desperately needs them. Our trade consists mostly of young, white males
and it shows in the kinds of applications that we develop and celebrate. Most of
it targets young, white males. If our businesses are to continue growing, we
need diverse voices like the ones I saw in that room to feel welcome and
participate.

If you _are_ in a position of leadership, then you are obviously in a better
position to make cultural changes. I encourage you to take risks: real
leadership consists of more than just successful project or companies, but also successful
people. The projects you're working on will come and go, but the members of your
team are going to to remember your management style even after they've parted ways.
If our trade is going to include the marginalized, it will start with you.

Now I want to transition into two areas that might get a little more heavy. I
say that because while I've got strong opinions about how we spend time on
ourselves and our teams, I have even stronger opinions on our interactions with
our community and our world. These go beyond just being a better developer. They
are where we become better humans. I argue that these things cannot be
approached independently - a terrible human is not a great software developer.
When you shuffle off that mortal coil how will you be remembered? Will it be
that absolutely fantastic open source library that you wrote? Or will it be how
you treated those you came into contact with?

The one person that really brought this reality home for me was Jim Weirich. MR.
Weirich was the creator of rake and a very active speaker in the Ruby community.
I got to see him speak at Ruby Hoedwon not long after I moved to Nashville. His
approachability was immediately noticeable. He was happy to answer questions,
even questions that others might dismiss as rudimentary. When he passed away in
February 2014 there was an outpouring of gratitude from those who had come into
contact with him. Sure, he was a great programmer and he had built some amazing
tools in the Ruby community. His lasting contribution, though, wasn't his code.
It was his patience, kindness, and wisdom. That's something to aspire to.


### Community
---------------

- "Community doesn't just happen [...]. It has to be made. The people who make
  it are the unsung heroes of our work experience."
- We have a deep longing for community built into the human DNA.
- Supportive communities welcome new members.
- Communities contain embedded knowledge that accumulates over time.

In the middle of the 19th century, Great Britian one of the world's dominant
countries. It held sway over 10 million square miles. It was a world center
of science and progress.

In 1845, a Royal Navy officer, Captain Sir John Franklin, embarked to explore
the Arctic north of Canada. It was an ill-fated expedition. Later voyages found
the graves of the men and discovered that they had suffered from pnuemonia,
tuberculosis, lead poisoning, and scurvy. Furthermore, scratches on the bones
indicated that in their final days they had resorted to cannibalism.

In that same harsh climate in which they perished, however, you would have found
tribes of native Inuits who had survived for thousands of years.

The Inuits would have been labeled primitive by most 19th century standards. The
British certainly would have said as much.  Why would they have survived in a
climate that a crew of capable English explorers could not?

The answer is that the Inuit community was embedded with the knowledge of how to
survive the cold. This kind of communal knowledge is both tacit and cumulative.

One of my favorite podcasters, Russ Roberts, points out that if the Inuits had
written books about how to survive in the wilderness, the English would still
have had a very difficult time adapting because much of the knowledge existed
in cultural practices and habits.

Furthermore, this knowledge was cumulative: The Inuit community had accumulated
survival techniques over generations: this is the kind of knowledge that would be
very difficult for one person to accumulate in a lifetime.

Community can happen anywhere. You have a community in your company, a community
in your neighborhood, perhaps a church community. You also have a community of
those who work locally in your trade. That community has embedded knowledge,
too. Knowledge about best practices, great places to work, what are "options"
and what do I do with them, how to run a conference...  I have no idea how
how to put on a good conference. I've never done it before. This knowledge is,
however, embedded in the community in people like Jason Myers, Jacques Woodcock,
Will Golden, Ben Ramsey, and many others. (All we need to do, then, is harvest
their brains and... I'm just kidding!)

Much of what I covered in regards to teams and companies can be applied to
communities. If knowledge in a community is cumulative, then adding diversity to
our communities gives us a huge opportunity to grow that knowledge in new
directions. Every time we add a new member to our community, we add the
potential to grow the communities accumulated know-how. That's one reason it's
so important to make sure that our community is welcoming to newcomers.

How can we be welcoming to newcomers? One way is to make ourselves available for
knowledge sharing, or peer coaching.  That's fundamentally what user
groups are about - knowledge transfers and collaboration that encourage the
growth of an overall community. Developing the community's professional skills
leads to companies setting up shop which encourages further growing of the
community's professional skills which leads to... it's a positive feedback
cycle.

Making it welcome to newcomers also means embracing diversity. I don't just mean
demographic diversity, but a diversity of thought and background. That means
welcoming people who not only look like us, but maybe also don't act like us or
think like us. That pushes our community to grow knowledge not only vertically
(writing "better" code) but also horizontally (what kinds of things are we
building, what needs are we serving).

Earlier I talked about how you can't make a team jell. You can create an
environment for it, but you can't force it. Communities, on the other hand, *are*
built. They don't just happen.  As DeMarco and Lister point out, "The people who
make [community] are the unsung heroes of our work experience." This includes everyone
from the folks running the conference to those telling me when my time is up
and I need to leave the podium.

Indeed, what is more often missing in a community is _you_. Yes, you. You, like
me, have a multitude of other commitments that you must prioritize. Family,
work, etc. Or perhaps you find yourself imbued with a lack of confidence: how
can _I_ contribute? I'm still swimming over here on the shallow end. In that
case, come talk one of the user groups about what you're learning and how you're
learning it.  There are others who are right there with you and they'd like to hear
about your approach.

Opportunities to make an impact on the community level are often richer than the
opportunities found on a team or inside a
company. On a team or in a company your efforts may be stymied by management or
by the culture that is slow to change. On the community level, however, the
leaders tend to be those that show up regularly and give generously of their
time. There are endless opportunities to jump in and lend a hand - from speaking
at local user groups to volunteering at conferences to sponsoring.

### World
---------

Most mature trades (legal profession, doctors and nurses, financial advisors)
have a well-defined code of ethics. In the mid 20th-century, in particular, many
trades and organizations created a code of ethics that still apply today.

Our trade has one, too. The Association for Computing Machinery first made a
stab at writing a code of ethics for programmers in 1972. It still actively
maintains a set of ethical principles that was also approved and adopted by the
IEEE (Institute of Electrical and Electronic Engineers).

What makes a code of ethics necessary? Often it is a response to market forces
(an attempt, for example, to avoid regulation by declaring, "Look! We're self
regulating!"). I don't think that was the case in the computing industry.
Regardless, it serves several purposes:

- It signals to the rest of the world that we can be trusted. Mark Frankel wrote
  an oft-cited paper, "[Professional Code: Why, How, and with What
  Impact?"](http://www.jstor.org/stable/25071878?seq=1#page_scan_tab_contents)
  and he put it this way:
  "it will help persuade the public that professionals are deserving of it's
  confidence and respect, and of increased social and economic rewards."
- It communicates a list of ideals that we stand for. It is aspirational.
- It "balances the risk of individuals with the risk of society" (see Jacob
  Metcalf's great report, "[Ethics Codes: History, Context, and
  Challenges](http://bdes.datasociety.net/council-output/ethics-codes-history-context-and-challenges/)
- It offers a method of self-retrospection: Am I, as a human, meeting these
  standards that others in my profession have agreed are the standards?

The first principle: "*Contribute to society and human well-being*." That's a
pretty heavy ask.  This isn't just a call to avoid hurting others (that
principle comes next), but to actively contribute to society and human well-being.

In a 1992 paper, the ACM put it this way, "[we have] an obligation to protect
fundamental human rights and to respect the diversity of all cultures. [...]
computing professionals must attempt to ensure that the products of their
efforts will be used in socially responsible ways."

If we, as a collective trade, abdicate our duty to protect fundamental human
rights (like the right to privacy) we will experience, as a trade, a collective
loss of public trust. If we lose that trust we will no longer enjoy the freedom to
build whatever we like, however we like. The trade could become stifled with
regulations and bureaucratic processes. It won't happen all in one day or even one
year or even one decade. If you have worked in the healthcare or financial
industry, you probably have already had a taste of what this would look like in
the form of HIPAA and Sarbanes Oxley. Those regulations were a response to
developers and other computing professional that abdicated their responsibility
to the rest of humanity and betrayed their trust.

But this isn't just about "not doing harm." It goes beyond that. It's
suspiciously close to what the popular HBO series "Silicon Valley" riffed on
during it's first season: every startup had a variation on how they were going
to "make the world a better place."

That may have become a platitude, but here we find it in original glory. As
professionals, it is up to each of use to evaluate our work and decide if it
meets the standard of "contributing to society and human well-being."

The second principle may, at first glance, seem to be a subset of the first.
*Avoid harm to others.* The ACM elaborates on this by defining "harm" as "injury
or negative consequences." They give examples like physical injury, loss of data
or property," intentional or unintentional. This means we are to "carefully
consider potential impacts of [...] decisions made during design." This is
another opportunity for self-reflection during the specifications and design
phase.

There's a scene in "Tron" (both the new and old versions) in which one of the
programs (Tron himself, I believe) says, "I fight for the users." As the
architects of the sky castles, it's our responsibility to fight for the users.
If necessary, we may even have to blow the whistle when we see harm being done.
It's our professional responsibility.


Principle three: *Be honest and trustworthy.* Among other things, this applies to
our discussion earlier about an environment where team members don't feel inadequate
when they ask for help. An honest developer isn't ashamed to admit his or her
limitations. You can't know everything, and pretending that you do is a
disservice to both your team and those that use your application.


Principle four: *Be fair and take action not to discriminate.* I like that this
principle doesn't say "don't discriminate." This is a proactive declaration. We
all are guilty of discriminating in different ways (it often happens without any
self-awareness). This is urging us to take action to be inclusive, to take
action when we observe discrimination, to fight for equality when we find the
opportunity before us.

*Give proper credit for intellectual property.* Those licenses you see on
software packages are important. We're obligated to respect the restrictions
placed on software by others, even if we don't like them.

*Respect the privacy of others.* This one is particularly fascinating to me
because I've been reading Bruce Scheier's "Data and Goliath." As Scheier puts
it "surveillance is the business model of the internet." Content is only
valuable in that it attracts eyeballs that can be sold to advertisers. The more
advertisers know about those eyeballs, the better. Google knows everything there
is to know about me - everything I say (thanks, voice control!), how many steps
I take, the places I visit. The potential for abuse of this information is
significant. I certainly hope that the developers at Google have read the ACM's
code of ethics and decided that respecting the privacy of others trumps padding
their wallets.

The ACM elaborates on this principle by saying, "This imperative
implies that only the necessary amount of personal information be collected in a
system, that retention and disposal periods for that information be clearly
defined and enforced, and that personal information gathered for a specific
purpose not be used for other purposes without consent of the individual(s)."

This is not something that most companies today are doing. Often we can
only guess about what information is being collected, how long it will be
retained, or how it will be used. Again, this could end badly if we abdicate
our professional responsibility of respecting the privacy of our users.

That ties into the last principle: *Honor confidentiality.* As developers we often
have access to a pile of information that most people don't. Betraying that trust
cheapens our trade.

### Conclusion
--------------

One of my favorite feminist writers, Dorothy Sayers, wrote the following in her
essay "Why Work?":

> We should ask of an enterprise, not "will it pay?" but "is it good?"; of a
> man, not "what does he make?" but "what is his work worth?"; of goods, not
> "Can we induce people to buy them?" but "are they useful things well
> made?"; of employment, not "how much a week?" but "will it exercise my
> faculties to the utmost?"

A tree without sturdy roots will not make a healthy forest. I acknowledge that
we need to spend a significant portion of our time focussing on our ability to
develop better software. Some of that time will be spent making sure that we are
capable of being the best developer we can be.

Beyond that, though, is so much more. Imagine you're telling your grandchildren
stories about your adventures as a software developer in the first half of the
twenty-first century. Will you regal them with stories of the clever one-liners
you wrote in Rust? Perhaps you'll tell them about the time you saved a company
by making an algorithm faster, or cleaner, or more maintainable (perhaps all
three!). Maybe you'll elaborate on how you took the test suite from 50% code
coverage to 90% code coverage.

Perhaps you would tell these stories, and perhaps your grandchildren would be
duly impressed. I am willing to bet, however, that it will be stories about your
_relationships_ in the trade that stand the test of time.

Would not you rather tell them about how you, with your privileged status as a
white male with straight teeth, worked to with your team members to welcome the
marginalized into your company, giving them a voice to contribute their ideas?

Wouldn't you rather tell them about how you joined that team and worked closely
alongside an amazing group of people to build something that contributed to the
betterment of humanity?

Wouldn't you rather tell them about the community that you were part of, how you
coached the newcomers and challenged them to become better developers,
contributors, and humans?

I don't know about you, but that's the legacy that I'd like to leave behind.

Let's leave that forest thriving.

Thanks for your time.
