---
layout: post
title: "Bare Minimum Software Development Infrastructure in Air Gap"
tags:
- Air Gap
- Infrastructure
---

Over the last decade, software development socieities experienced a paradigm
shift towards the idea that software development is a social activity as well
as an engineering decipline. This was in fact not a new idea and had been
proven successful over a quite a long time in various software development
cultures including Free Software Movement started in 1980s by Richard Stallman.
Even though the concept of Free Software, which is "free as in freedom of
speech, not free as in free beer", stayed as a conservative social movement
that refuses the use of any non-free software, it further encouraged Open
Source Software, which is more of a software development strategy for financial
concerns rather than freedom concerns. Open Source completely changed the way
companies and individuals develop software. I *highly* recommend listening to
or reading [Richard Stallman and The History of Free Software and Open
Source][1] for the full story. It is incredibly well-prepared and gives a taste
of a documentary about software development cultures and and their histories.

The success of Open Source is no surprise as it brings the reusability goal of
software components together with the power of sharing, which paves the way for
innovation and agility. Aside from high-quality, innovative software components
and tools, Open Source also led to a culture of best practices shaped over the
years. The culture also affected the notoriously closed-source companies. To
understand what Open Source changed in the world, please look at Microsoft's
pride and happiness on their contribution to Open Source [here][2]. Microsoft
open-sourced many of its [products][3] on GitHub and they maintain them in an
Open Source culture. For any software company, immersion into Open Source is
ineviable and that is why BAE Systems is looking for a [candidate][4] with
"Good knowledge of Open Source tools and technology platforms". Why do you
think NASA supports and [contributes][5] to Open Source?  It seems while all
the famous software developing companies are openly involved in Open Source,
not-yet-famous ones are probably the ones which have not yet shown interest in
this breakthrough.

There are three questions I can think of you should ask yourself before using a
piece of open source software.

- Does the software component techinically qualifies and satisfies your needs?

- Does the license of the software legally allows you to distribute your
  product the way you plan to? For example, GPL let you modify the code for
  your needs, but when you decided to distribute your modified version, it
  requires you to deliver all the rights you received with the code to your
  customers. You may want to see [this page][6] to familiarize yourself with
  the licenses.

- Do you have access to the software?

The last question might sound funny to many developers, but it should not to
the ones developing software in an air-gapped network, which gives no direct
internet access to developers' computers and  commonly employed in financial,
governmental and military systems for the sake of security measures.

In the modern world, software is installed, removed and upgraded by the help of
package managers in an automated, unattended fashion. No more clicking here and
there to deal with software. There are two kinds of package managers: System
package managers and language-specific package managers. All package managers
have their repositories which host most of the packages that you can install on
your computer. One solution to the air gap could be exploiting package
repositories by mirroring them into the private network and configuring the
corresponding package managers to access to the software packages on the local
mirror. This is also what JFrog Artefactory suggests on their blog [post][7].
The figure below demonstrates how the network should look like.

{% include figure.html path="blog/minimal-infrastructure/proposed-network.png" alt="Minimal Infrastructure" %}

Given that `download.company.com` has two network interfaces, interface 1 for
the internet and interface 2 for the private network which are controlled by
switch 1 and switch 2, respectively. You can mirror the package repositories
into `download.company.com` from the internet by closing switch 1 and opening
switch 2.  You can copy the mirrors from `download.company.com` to
`external.company.com` in the private network by opening switch 1 and closing
switch 2. When the repositories are copied to the private network, you can open
both switches. If you don't want to close switch 2, an alternative is to carry
the repositories into `external.company.com` using an external storage, which
cold be more tedius if you like to update your mirrors frequently. The
mirroring frequency is totally up to you. Package managers in developer and
other server machines should be configured to use the repositories from
`external.company.com`. Note that `external.company.com` should be read-only
from the private network side. It should only be accessed from the package
managers to download packages and switch 1 and switch 2 should never be closed
at the same time. I am by no means a security expert, but if you can guarantee
that third party software comes from only through `external.company.com`, you
can hopefuly improve your security with less effort. It at least makes more
sense than allowing arbitrary person to install software from an unknown source
using authorized or unauthorized USB stick which previously plugged into a
machine with internet access in an instance like [this][8].

As stated earlier, the use of open source software per se is not enough to
develop good quality and innovative software. You should also enforce open
source best practices, habbits and culture in your company. For instace, bring
blogging culture to your company. Let people share their experience, thoughts
and worries through their personal blog posts where the other people can also
comment on the post. In the long run, having `blog.company.com` helps your
company develop a culture and history. Many developers write blog posts and no
one ever forces them to do so.

I cannot image a developer who has never used StackOverflow. Software
developers need Q&A platforms like StackOverflow. `answers.company.com` should
help your developers with their especially company-specific questions. More
often than not a problem deserves a more structural how-to description rather
than a quick answer. This is where `wiki.company.com` shines in. Answers to
those questions in `answers.company.com` should provide a link in
`wiki.company.com`.

There is really no substitute for git as a version control system. Modern
software developers use GitHub, GitLab, Phabricator, BitBucket or a few others
to colloborate with other developers. Many startups develop their software in
private or public GitHub repositories. You should absolutely have your private
instance of `git.company.com` in your facility.

Automated build, automated testing, automated packaging, and even automated
deployment is now integral part of and software development process. There are
great Continuous Integration(CI) applications to help your team automate their
software development life cycle. Having a `ci.company.com` and several slave
nodes to it is invaluable. For example, let's assume `slave1.company.com` has a
powerful GPU. It trains and tests your deep learning models when you asks it to
do so through `ci.company.com` and when it is done, you get your model and its
performance metrics from a web page on `ci.company.com`.

Similar to `external.company.com` you should create your private packages and
publish them in your private repositories on `internal.company.com`. People
have a reason to ship software in packages. You should follow the same
principle and package your own software.

Office documents seem to lose their usage in software development to web
applications. People tend to prepare Markdown-based presentations and write
documentations either with GitBook-like tools or directly build documentation
right from the code using Doxygen or similar tools. When people really need to
use an office suite, they tend to use a cloud-based office suite like Google
Docs.  [draw.io][9] seems to be getting more popular for drawing various types
of diagrams including UML among the others. Good news is that draw.io can be
easily installed on-premise using its docker image. An open source alternative
to Google Docs could be the cloud version of LibreOffice. In the end,
`office.company.com` is also nice to have.

Note that you do not have to have separate web applications such as Wiki, Q&A
forum, blogging software and machines for each as depicted in the drawing
above. GitLab comes with a wiki support, an issue tracker and a CI tool.
Phabricatory also features Q&A forum, blogging and many more amenities but its
workflow is slightly different than the mainstream repository hosting services.

The machine in the drawing could be either physical or virtual. Servers should
be Linux powered machines. Developers could also need GNU/Linux machines most
of the time if they are working on specific projects such as IoT for which even
Microsoft had to [leave][10] Windows in favor of Linux. In addition, Windows 10
features a Linux shell in its developer mode. This should have a reason. May be
developers really needed it and Microsoft eventually came to the conclusion
that they were right?

Sadly, installing all these tools are still not enough. Your team members
should adopt and internalize this culture if they have not yet. Don't get me
wrong, I don't mean your should open source all your projects. It is your
development strategy how much you open source or contribute to Open Source. But
there is no excuse for inability to use Open Source even when it is technically
and legally convenient to you.

These are all my personal ideas. I am still in search of better ways to improve
software development experience in an air-gapped network. Comments and
suggestions are more than welcome.

[1]: https://www.cmpod.net/all-transcripts/history-open-source-free-software-text/
[2]: https://www.youtube.com/watch?v=LXu80xXwFY0
[3]: https://github.com/Microsoft
[4]: https://jobs.baesystems.com/global/en/job/37091BR/GIS-Data-Manager-Open-Source-Tools-and-Evaluation
[5]: https://code.nasa.gov
[6]: https://tldrlegal.com/
[7]: https://jfrog.com/blog/using-artifactory-with-an-air-gap/
[8]: https://www.theverge.com/2014/12/30/7467809/south-korean-nuclear-plant-finds-malware-connected-to-control-systems
[9]: https://www.draw.io/
[10]: https://www.youtube.com/watch?v=o_FSuy8mVA4
