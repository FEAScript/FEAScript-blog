---
layout: post
title: "FEMail from FEAScript (July 2026)"
date: 2026-07-07
categories: [News]
tags: [FEAScript, FEAScript Studio, OpenFOAM, Newsletter]
mathjax: false
---

_This is the first issue of the FEAScript mailing list. [Subscribe here](https://mailchi.mp/e29600955ffe/join-the-mailing-list) to get future updates directly in your inbox._

---

Hi **FEAScript-ers**!

I would like to thank you for joining the mailing list. In this mail, I want to share some news and a few thoughts regarding [FEAScript Studio](https://feascript.com/studio.html), starting with… **OpenFOAM**!

In the early versions of OpenFOAM, the developers offered an official GUI called **FoamX**. It allowed users to visually modify the -most of the time vague- input text files. Although the idea of such a GUI seemed reasonable considering the large number of keywords and dictionaries, it was quickly abandoned. What happened?

It may seem quite strange, particularly if you are not part of the open-source CFD community, that **OpenFOAM users favored editing text files over clicking buttons**. In trying to interpret this behavior, I would say that editing text files gives much more control over the software. Today, there is also another advantage to using text files: LLMs can create and modify them (though with ambiguous results). This is, however, another story, and I don't think OpenFOAM users back in ~2009 (around when FoamX was abandoned) could have ever imagined that development.

So, how does this connect to FEAScript Studio? Seeing how much engineers love text files made me wonder: **is the fate of all simulation GUIs to vanish under the shadow of their core engines?** It's a question that has haunted me. What are the true advantages of having a GUI, considering that writing code offers version control, easy automation, and weightlessness, among other benefits?

Well, if nothing else, I have learned some **valuable lessons**. For example, a GUI should be modular so that new core engine capabilities can be easily incorporated. Also, hosting the GUI online avoids a versioning hell between FEAScript-core and Studio versions. Ultimately, the Studio will support, among others, no-code simulation (via Blockly), an integrated code editor (Monaco), cloud saving and version control. More news coming soon!

![Ceramic tile drawing from the 21st OpenFOAM Workshop in Guimarães](https://dim.mcusercontent.com/cs/83b4dec50b84e136c2e82c6a4/images/ae2a8521-736d-d4cc-67ab-35036c6b3cee.jpg?dpr=2&rect=0%2C484%2C4000%2C1860&w=660&h=307)

PS 1: How did I come up with this connection? I recently participated in the **21st OpenFOAM Workshop in Guimarães**, Portugal, where I was busy thinking of how to make FEAScript conquer the open-source world (kidding!). Bonus info: the organizer of the workshop, Miguel Nóbrega (amazing organization by the way), had the brilliant idea to let us create a collective work of art by drawing on ceramic tiles. Please forgive my sloppy drawing above, but I hope it works as a good luck charm!

PS 2: Of course, I am not comparing the massive community and development level of OpenFOAM with my tiny project. However... _Don't Stop Believin'_!

All the best,
Nikos
