---
layout: page
title: Syllabus
---
# DESMA 158: GAME ENGINE

Course Name & Number: DESMA 158  
Course Title: Game Engine  
Academic Term: Spring 2023  
Location: Broad 4240  
Day and Time: Tuesday and Thursday: 9 – 11:50am

Instructor: John Brumley (He/Him)  
Office hours & Location: Tuesdays 1-2pm / Game Lab  
Email: jtbrumley@g.ucla.edu

Teaching Assistant: Vincent Roca (He/Him)
Office hours & Location: Tuesdays 1-2pm Room 4240  
Email: vroca@g.ucla.edu

## Course Description

This course introduces the fundamentals of programming interactive projects in game development software. Classwork focuses on familiarizing students with game engines, computer programming concepts, player experience, and other skills that are foundational to making digital games. Lectures, exercises, and class projects teach skills needed to create digital games including custom rules, interactive physics systems, vectors, generative or randomized levels, save data, custom input systems, score-keeping, and sound. This course is offered in parallel with the concurrent courses, Game Design and Interactive Animation.

## Prerequisites

DESMA 24 Interactivity. Unity is a complex software that relies heavily on scripting. We will revisit many of the same concepts covered in Interactivity, but using the C# scripting language with the Unity scripting API.

## Learning Outcomes

By the end of this course, you will be able to create a real-time game with custom rules, generative or randomized levels, save data, responsive controls, physics, sound, and simple animation. The skills you will learn in this class translate well to immersive media, generative animation, and other modes of human-computer expression.

## Course Outline

```text
See the [schedule](schedule.md) for a more detailed breakdown of each class.
```

**Weeks 1–2**  
Introduction to game development tools, programming basics, keeping score, visual language, and level design.

[Project 1: Rolling Ball Game (Due: Week 2)](project-1.md)  
Create a 3D game that uses keyboard controls to maneuver a physics-based sphere through space and gather collectables. This simple game serves as an introduction to game development tools.

**Weeks 3–6**  
A focus on vector fundamentals, physics, and persistent data.

[Project 2: Arcade Game (Due: Week 6)](project-2.md)  
Remake a classic 2D arcade game, such as space invaders, pong, or breakout. Experiment with the structure of the game, apply new knowledge about interaction design, keeping score, physics, and colliders.

**Weeks 7–10**  
Using randomness, arrays and lists, and instantiating game objects.

[Project 3: Generative Game (Due: Week 10)](project-3.md)  
Create a game with randomized game objects, levels, and/or dynamic or unpredictable systems. Use prefabs, the instantiate function, and modular game objects.

## Assignments & Grading

### Grading Breakdown

> - Project 1: 20%
> - Project 2: 30%
> - Project 3: 30%
> - Participation / Attendance : 20%
> - Extra Credit !✨%

### Evaluation

Approach each project with your own level of skill and comfort in mind. You should work to expand your technical skills, but also lean into your strengths. If you’re good at drawing, use a bunch of 2D drawings! If you’re into photography, use photocollage to build your game world!

Creative projects and proposals are graded based on these parameters:

- Submitting on time.
- Completing project deliverables.
- Attention to detail/craft. Does the project run? Are there unintended bugs, glitches, etc.
- Project scope / ambition / aesthetic and technical ambition. Are you doing the bare minimum, or are you pushing yourself technically or aesthetically?
- Creative risk taking and resourcefulness. Are you bringing something unique and fresh to your design? Sometimes a simple, hacky solution works best!

Reading and lecture responses are pass/fail. As long as you thoughtfully complete them, you’ll get full credit.

### Submitting Projects

```text
See Submission Guidelines for more details
```

#### PROJECT SUBMISSION

Finished projects will be submitted along with:

- At least **one** screen recording of gameplay (No desktop, no editor, only your game!)
- At least **two** other screenshots of the project.
- A **brief** description detailing the basic premise of the game and how to play the game
- A Windows build of your game **and** an exported package of your scenes

#### DESIGN DOCUMENT

Each project will begin with a short game design document detailing the concept of the game. This document will include a title, descriptions of win/lose states, the challenge of the game, inputs and controls, and illustrations of levels, characters, items, etc. We will use these as tools for developing prototypes and giving feedback as projects are developed.

#### LATE WORK

Projects are due at the beginning of class on their respective due date. After this time, a full letter grade will be deducted from the project grade for each week that the assignment is late (two weeks late == two letter grades deducted).

Extra time will not be given for work lost due to save issues, editor errors, computer crashes, etc. Unity projects are complicated and can be annoying to backup. Make sure to save often and occasionally create a backup of your scenes. I recommend [exporting a unitypackage](how-to-submit-projects.md#Exporting%20Unity%20Packages) of your project and storing the package on an external drive or cloud backup. If you are comfortable with version control, there are a number of options as well ([1](https://unity.com/solutions/version-control) , [2](https://youtu.be/_ewoEQFEURg)).

If you anticipate that you won’t be able to complete the work by the due date, please contact us **before** the due date so we can discuss options.

#### ATTENDANCE

Please come to class on time at **9:00am**. If you are more than 15 minutes late, you will be marked as late. Three late marks results in an unexcused absence. Any disputes should be discussed with the TA within two weeks.

If you must miss class, email the TA prior to the class. Absences will not be excused after the fact except in extreme circumstances. You get **one** unexcused absence without it affecting your grade. Each unexcused absence after that will result in one full letter grade deduction from your participation / attendance score.

#### APPROPRIATION, FAIR USE, AND GENERATED CONTENT

Because the aim of the course is to explore the techniques and processes for using game engines, it is perfectly acceptable to use assets that you did not create yourself for developing early stage prototypes and testing mechanics. **However**, you should strive to develop your own assets for your project submissions, but if major portions of the project have been borrowed or generated, particularly audio, visual, and textual content, please discuss with us ahead of time.

## Resources

### Discord

We will be using Discord as a communication channel for the class. This is a place to share links, references, ask/answer questions, and generally communicate (instead of email). Please check the discord regularly for updates and announcements.  
  
If you have a project-related question outside of office hours, please use the _“tech-help”_ channel of the discord rather than sending us direct messages. We can make a separate thread in the channel for each question.

### Required and Recommended Tools:

- [Unity](https://unity3d.com/get-unity/update) – We recommend that you **install with Unity Hub**, and get the latest LTS version (currently 2021.3)
- Visual Studio – **Install visual studio with unity hub while you are installing unity**. (If you already have Unity working with VS Code or another text editor / IDE, feel free to use that)
- A three-button mouse
- 2D and 3D production software of your choice. Some options:
    - [Krita](https://krita.org/en/) – powerful open source digital paint tool
    - [Blender](https://www.blender.org/) – fully featured open source 3D art and animation tool
    - [Piskel](https://www.piskelapp.com/) – free pixel art app
    - [Aseprite](https://www.aseprite.org/) – inexpensive pixel art / animation tool
    - [Sculptris](http://pixologic.com/sculptris/) – “A gateway into the exciting world of 3D.”
    - [Crocotile 3d](https://prominent.itch.io/crocotile3d) – A tool for creating 3d scenes with 2d tiles.
    - [Mixamo](https://www.mixamo.com/) – Free, but requires a login- community sourced walk cycles and 3d animations which you can apply to any model that can T-pose.

[Exhaustive list of cheap and free tools compiled by Everest Pipkin](https://github.com/everestpipkin/tools-list#making-assets---images-models-sound-video)

### Recommended Readings

There are no required readings for the course, however there may be the occasional short reading, listening, or video to check out between classes. These will be shared throughout the quarter through the discord.

The official [Unity User Manual and Scripting API](https://docs.unity3d.com/Manual/index.html) is an indispensable reference, keep it handy.

Books about game development (we have copies!):

- Anna Anthropy. _Rise of the Videogame Zinesters : How Freaks Normals Amateurs Artists Dreamers Dropouts Queers Housewives and People Like You Are Taking Back an Art Form_. Seven Stories Press 2012
- Jesper Juul. _Handmade Pixels : Independent Video Games and the Quest for Authenticity_. MIT Press 2019.
- Katie Salen Tekinbaş and Eric Zimmerman. _Rules of Play : Game Design Fundamentals_. MIT Press 2004.
- Brian Schrank and J. David Bolter. _Avant-Garde Videogames : Playing with Technoculture_. MIT Press 2014.
- Steve Swink. _Game Feel : A Game Designer’s Guide to Virtual Sensation_. Morgan Kaufmann Publishers/Elsevier 2009.

Programming and Unity Support

- Robert Nystrom – [Game Programming Patterns](https://gameprogrammingpatterns.com/contents.html) (ebook)
- Keith Burgun – [3 Minute Game Design](https://www.youtube.com/playlist?list=PLFFUZ_uHAWMU44iAlkVoXKnsOefNYdsaK) (youtube)
- Brackeys [Unity Tutorials](https://www.youtube.com/channel/UCYbK_tjZ2OrIZFBvU6CCMiA) (youtube – no longer updated)
- [Game Maker’s Toolkit](https://youtu.be/XtQMytORBmM) (youtube)
- [Code Monkey](https://youtube.com/playlist?list=PLzDRvYVwl53vxdAPq8OznBAdjf0eeiipT) (youtube)
- [Unity Youtube](https://www.youtube.com/playlist?list=PLX2vGYjWbI0RQ3O-nAuJd2LWm7lH5htrL)
- [O’reilly books](https://www.oreilly.com/library-access/)

### COVID-19

It is important that everyone stay safe and avoid coming to class if you have any concerns about your health status.  
  
If you find that external struggles and/or COVID related challenges are affecting your ability to attend class, please reach out to us. We want you to be successful in the class, but we care about your wellbeing more than anything else. Open communication with us is most important in this regard, and we will be very open to accommodating every reasonable request.

Students must adhere to the current campus directives related to COVID-19 mitigation, and refusal to do so may result in the student being asked to leave the classroom or referred to the Dean of Students. For more information about COVID-19 requirements on campus, please visit: [https://covid-19.ucla.edu/information-for-students/](https://covid-19.ucla.edu/information-for-students/). 

### Land Acknowledgement

The University of California, Los Angeles occupies the ancestral, traditional, and contemporary Lands of the Tongva and Chumash peoples. Our ability to gather and learn here is the result of coercion, dispossession, and colonization. We are grateful for the land itself and the people that have stewarded it through generations. While a land acknowledgment is not enough, it is the first step in the work toward supporting decolonial and indigenous movements for sovereignty and self-determination. Read more about what land you’re occupying: [https://native-land.ca/](https://native-land.ca/) 

### Commitment to Diversity & Safer Spaces:

We understand the classroom as a space for practicing freedom; where one may challenge psychic, social, and cultural borders and create meaningful artistic expressions. To do so we must acknowledge and embrace the different identities and backgrounds we inhabit. This means that we will use preferred pronouns, respect self-identifications, and be mindful of special needs. Disagreement is encouraged and supported, however our differences affect our conceptualization and experience of reality, and it is extremely important to remember that certain gender, race, sex, and class identities are more privileged while others are undermined and marginalized. Consequently, this makes some people feel more protected or vulnerable during debates and discussions. A collaborative effort between the students, TA, and instructor is needed to create a supportive learning environment. While everyone should feel free to experiment creatively and conceptually, if a class member points out that something you have said or shared with the group is offensive, avoid being defensive; instead approach the discussion as a valuable opportunity for us to grow and learn from one another. Alternatively, if you feel that something said in discussion or included in a piece of work is harmful, you are encouraged to speak with the instructor or TA. _*Statement adopted from voidLab at:_ [_https://github.com/voidlab/diversity-statement_](https://github.com/voidlab/diversity-statement) 

### Center for Accessible Education (CAE)

The UCLA Center for Accessible Education (CAE) is responsible for ensuring students with documented disabilities have access to an inclusive, supportive learning environment. Students with disabilities or other needs requiring academic accommodations should speak with me as early in the quarter as possible to be sure they get the support they need.

Students needing academic accommodations based on a disability should contact the Center for Accessible Education (CAE) at (310) 825-1501 or in person at Murphy Hall A255. When possible, students should contact the CAE within the first two weeks of the term as reasonable notice is needed to coordinate accommodations. For more information visit [www.cae.ucla.edu](http://www.cae.ucla.edu/). 

### Academic Integrity and Information on Student Conduct

UCLA is a community of scholars. In this community, all members including faculty, staff and students alike are responsible for maintaining standards of academic honesty. As a student and member of the University community, you are here to get an education and are, therefore, expected to demonstrate integrity in your academic endeavors. You are evaluated on your own merits. Cheating, plagiarism, collaborative work, multiple submissions without the permission of the professor, or other kinds of academic dishonesty are considered unacceptable behavior and will result in formal disciplinary proceedings usually resulting in suspension or dismissal. As specified in the [UCLA Student Conduct Code](https://www.deanofstudents.ucla.edu/studentconductcode), violations or attempted violations of academic dishonesty include, but are not limited to, cheating, fabrication, plagiarism, multiple submissions or facilitating academic dishonesty. When a student is suspected to have engaged in academic dishonesty, Academic Senate regulations require that the instructor report the allegation to the office of the Dean of Students. For more information, see the [UCLA Student Conduct Code](https://www.deanofstudents.ucla.edu/studentconductcode).

### TITLE IX

UCLA prohibits gender discrimination, including sexual harassment, domestic and dating violence, sexual assault, and stalking. If you have experienced sexual harassment or sexual violence, there are a variety of resources to assist you.

### Confidential Resources

You can receive confidential support and advocacy at the CARE Advocacy Office for Sexual and Gender-Based Violence, 1st Floor Wooden Center West, [CAREadvocate@careprogram.ucla.edu](mailto:CAREadvocate@careprogram.ucla.edu), (310) 206-2465. Counseling and Psychological Services (CAPS) also provides confidential counseling to all students and can be reached 24/7 at (310) 825-0768.

### Non-Confidential Resources

You can also report sexual violence or sexual harassment directly to the University’s Title IX Coordinator, 2241 Murphy Hall, [titleix@conet.ucla.edu](mailto:titleix@conet.ucla.edu), (310) 206-3417. Reports to law enforcement can be made to UCPD at (310) 825-1491. These offices may be required to pursue an official investigation.

Faculty and TAs are required under the UC Policy on Sexual Violence and Sexual Harassment to inform the Title IX Coordinator—A NON-CONFIDENTIAL RESOURCE—should they become aware that you or any other student has experienced sexual violence or sexual harassment.

### Psychological Health, Well-Being and Resilience

UCLA is renowned for academic excellence, and yet we know that many students feel overwhelmed at times by demands to succeed academically, socially and personally.  Our campus community is committed to helping all students thrive, learn to cope with stress, and build resilience. Remember, self-care is a skill that is critical to your long-term success.  Here are some of the many resources available at UCLA to support you:

- **Counseling and Psychological Services (CAPS):** [https://www.counseling.ucla.edu/](https://www.counseling.ucla.edu/) Provides counseling and other psychological/mental health services to students. Walk-in hours are Monday-Thursday 8am-4:30pm and Friday 9am-4:30pm in John Wooden Center West. Crisis counseling is also available 24 hours/day at (310) 825-0768.  
    
- **Ashe Student Health and Wellness Center**: [http://www.studenthealth.ucla.edu](http://www.studenthealth.ucla.edu/) Provides high quality and accessible ambulatory healthcare and education by caring professionals to support the academic success and personal development of all UCLA students.  
    
- **Healthy Campus Initiative (HCI):** [https://healthy.ucla.edu](https://healthy.ucla.edu/) Provides links to a wide variety of resources for enhancing physical and psychological well-being, positive social interactions, healthy sleep, healthy eating, healthy physical activity and more.  
    
- **Campus and Student Resilience**: [https://www.resilience.ucla.edu/](https://www.resilience.ucla.edu/) Provides programs to promote resilience and trains students to help support their peers.  
    
- **UCLA Recreation**: [https://www.recreation.ucla.edu/](https://www.recreation.ucla.edu/) Offers a broad array of services and programs including fitness, yoga, dance, martial arts, meditation, sports, and much more.  
    
- **Equity, Diversity and Inclusion**: [https://equity.ucla.edu/](https://equity.ucla.edu/) Committed to providing an equal learning, working and living environment at UCLA and supports a range of programs to promote these goals campus-wide.
- **UCLA GRIT Coaching Program:** [https://www.grit.ucla.edu/](https://www.grit.ucla.edu/) GRIT stands for Guidance, Resilience, Integrity and Transformation. In this program, UCLA students receive individualized support from trained peer coaches to manage stress, foster positive social connections, set goals, and navigate campus resources.

### Resources for Students Dealing with Financial Stress 

- **Economic Crisis Response**: [https://www.studentincrisis.ucla.edu/Economic-Crisis-Response](https://www.studentincrisis.ucla.edu/Economic-Crisis-Response) provides support and guidance to students who have self-identified, or are identified by UCLA faculty or staff, as experiencing a financial crisis that impacts their academic success at UCLA.  
    
- **Bruin Shelter:** [http://www.bruinshelter.org/](http://www.bruinshelter.org/) provides a safe, supportive environment for fellow college students experiencing homelessness by fostering a collaborative effort between universities, community-based organizations, and service providers.  
    
- **The CPO Food Closet:** [http://www.cpo.ucla.edu/cpo/foodcloset/](http://www.cpo.ucla.edu/cpo/foodcloset/) provides free food for any UCLA student who may be experiencing hunger and/or struggling to attain food due to financial hardships.