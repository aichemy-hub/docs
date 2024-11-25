AIchemy Software Engineering Blog: Data Management at the Imperial NMR Facility
===============================================================================

Hello, dear reader, and welcome to the first AIchemy Software Engineering Blog
post. As you may know, AIchemy is the UK's new AI for chemistry hub, tasked
with developing and supporting the use of AI in chemistry research. As you may
imagine, in order to effectively use AI in chemistry, a couple of requirements
have to be met. Namely, we need an awful lot of data, and we need a way to make
this data easily available to researchers. Fortunately, this is exactly the
sort of thing the software engineering team (currently of size 1) is here to
support.

Before looking into what exactly we did, it may be worth giving a brief
overview of the data management practices currently at Imperial College, where
I am currently based, and which are fairly representative of other universities
in the UK. Experimental researchers use a variety of independent, college or
department owned, facilities to collect experimental data. For example, say I
synthesised a new compound and would like to determine the molecular structure
inside of my solution really looks like. Well, I will take my sample to the NMR
facility, and take an NMR spectrum and I will take my sample to the mass
spectrometry facility and collect a mass spectrum. The facilities provide me
with the machines and training to use the machines, and will give me the output
data of these machines. When it comes to publishing my results I have to ensure
I kept all my data in a safe place, correctly labelled and in a format that can
be read by other people (though often not without substantial effort on their
part).

This is essentially the state-of-play now, so let's examine some of the issues
researchers are starting to run into to motivate some of our work at AIchemy.
Firstly, this workflow delegates data management to researchers. This may work
on a small scale but data management is not an easy task. If you want to do
your own data management, here's just a small number of questions you may need
to consider, off the top of my head:

1. Which database should you use? SQL? NoSQL? PostgreSQL? MySQL? SQLite?
2. What will your schema look like?
3. How are data backups handled?
4. Where should data be stored? Locally? On the cloud? How will this be paid
   for?
5. How will data be accessed? SQL? A Python library? A web app?
6. How will data be shared with others? Will this depend on external vs
   internal collaborators?
7. Will changes to the data have an audit trail?
8. How will schema changes be handled?

And so on ... These questions are not just numerous, they also do not have
obvious answers, and choices come with trade-offs. In an age where
where FAIR (that is Findable, Accessible, Interoperable,
Reusable) data principles are gaining traction, answers to these questions
become increasingly important.

Sometimes, people are advised to gain additional training to help them answer
these questions, however, I think its more important to ask why a person
interested in chemical research should be considering these questions at all.
The fact is delegating data management to individual research groups means that
good data management practices will likely be inconsistently applied, less time
can be spent on research, the same work is repeated over and over across
different research groups and smaller groups are disadvantaged as they do not
have the resources to build and maintain their own data management solution.

At AIchemy, our aim to ensure that research data is always FAIR, from the
moment it is collected up to the point that it is published. Consider if
instead when you visit a facility to collect your data, instead of being given
data straight from the machine, you are given access to a database which not
only gives you the data from the machine, but also metadata, such as how the
data was collected, which processes were used for collection, who collected it,
which chemicals were involved, etc. and all in a FAIR way. Finally the facility
can allow you to publish your data to a DOI in the click of a button.
Importantly for us at AIchemy, having data organized in this way removes much
of the overhead from applying it in machine learning, removing much of the
barrier to entry. As more people use this system, datasets which can be used
for machine learning will grow larger and the performance of models can be
expected to improve.

Work at the NMR Facility
------------------------

With the preamble out of the way, let's look at some of the work we have done
at the Imperial College NMR facility, in conjunction with the two facility
managers Stuart Elliot and Pete Haycock.

The NMR facility has 4 main Bruker instruments, each of which is connected to a
computer. The computers on each machine are disconnected from both the College
network and from the general internet. When data is collected, it is
transferred to a shared drive
