---
question: "Do you have an application template?"
---
{% assign month = "now" | date: "%-m" | plus: 0 %}
{% if month >= site.gsoc_switch_month %}
# Matrix {{ "now" | date: "%Y" | plus: 1 }} Application Template
{% else %}
# Matrix {{ "now" | date: "%Y" }} Application Template
{% endif %}

```
Student Info
------------

- Name:
- GitHub username:
- Alternative-/Nickname:
- Email:
- Matrix ID: (i.e. @cadair:cadair.com)
- Which country will you reside in during the project?
- Time Zone:
- GSoC blog RSS feed URL: (You will have to write a blog post every
  week during GSoC.)


Code Sample
-----------

Link all your contributions to matrix and any other open source project here.

You may also mention specific issues/commits using the commit id if you want
us to take a look at that.


Project Info
------------

- Which project from http://matrix-org.github.io/gsoc are you applying for?
  If you have your own idea, please add it to our projects list:
  https://github.com/matrix-org/gsoc

- What is the final goal for this project? What would make it a total
  and perfect success?

- Are you already engaged with the project's possible mentors and do
  you have any preference for a particular mentor?
  We will try to get you your first choice for a mentor, usually it will
  be the first listed mentor as primary and another as secondary.
  All projects will have a primary and a secondary mentor.

- What parts of the matrix ecosystem do you have to work with in order to complete
  this project? What else are you planning on using?

- Why are you the right person to work on this project?

- How do you plan to achieve completion of your project?
    - Please provide a schedule with dates and important
      milestones/deliverables (preferably in two week increments).
      This is a great help in evaluating your own progress and helps you
      achieving your goal as it forces you to plan your work preemptively.

Add all ideas you have to solve the project here.


Other Commitments
-----------------

- Do you have any other commitments during the GSoC period,
  May 27th to August 19th?

    - We don't penalize students for needing adjustments to schedule if
      they're up-front about them and have a plan to mitigate any issues.
      However, we *will* fail students for lying about their availability
      and subsequently falling behind in their work. Be honest!

    - Do you have exams or classes that overlap with this period?

    - Do you have plans to have any other job or internship during this
      period?
        - This is __NOT RECOMMENDED AT ALL__ as GSoC is intended to be a
          full time job. But can be worked around if it only a small overlap.

    - Do you have any other short term commitments during this period?
        - e.g. family wedding, conferences, volunteer projects, planned
          vacation days

- Have you applied to any other organizations? If so, to whom and do you have a
  preferred project/org? (This will help us in the event that more than one
  org decides they wish to accept your proposal.)


Extra Information
-----------------

This additional information isn't needed but can help us to learn
more about you. All fields in this section are optional.

- Link to openhub account:
- University info
    - University name:
    - Major:
    - Current year and expected graduation date:
    - Degree:
- Other Contact info:
    - Alternate contact info in case primary mail above stops working:
    - Homepage:

- We love having twitter handles so we can tell people publicly about your
  great project and successes at https://twitter.com/matrixdotorg!
  (Not required but recommended.)

- Anything else you want us to know:

```
