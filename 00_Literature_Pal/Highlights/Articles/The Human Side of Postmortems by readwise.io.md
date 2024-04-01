---
title: The Human Side of Postmortems
full Title: The Human Side of Postmortems
author: readwise.io
URL: https://readwise.io/reader/document_raw_content/149516274
published date: 2015-03-24
category: articles
source: reader
tags: [medium/articles, author/readwise_io, reader/reader, date/2024-03-27, area/reader]
created: 2024-03-27
assignedTo: people/pal
priority: P4
work: document
---
author:: [[readwise.io]]
note:: 
source:: [[reader]]
url:: [articles URL](https://readwise.io/reader/document_raw_content/149516274)
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article4.6bc1851654a0.png)
category:: [[articles]]
date:: [[2024-03-27]]
last_highlighted_date:: [[2024-03-27]]
published_date:: [[2015-03-24]]
summary:: 


![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article4.6bc1851654a0.png)

## Highlights
### id698706628
[[2024-03-27]] 09:15
> Often as long as novellas (see Amazon’s 5,694-word take on the same outage discussed previously in “Summary of the April 21, 2011 EC2/RDS Service Disruption in the US East Region”2
> ), they follow a predictable format of the Three Rs3:
> • Regret — an acknowledgement of the impact of the outage and an apology.
> • Reason — a linear outage timeline, from initial incident detection to resolution, including the so-called “root causes.”
> • Remedy — a list of remediation items to ensure that this particular outage won’t repeat.


### id698706482
[[2024-03-27]] 09:15
> cover two additions to outage investigations — stress and cognitive biases — that form the often-missing human side of postmortem


### id698706933
[[2024-03-27]] 09:16
> More specifically, there are four relative stressors that induce a measurable stress response by the body:
> 1. A situation that is interpreted as novel. 2. A situation that is interpreted as unpredictable. 3. A feeling of a lack of control over a situation.


### id698706979
[[2024-03-27]] 09:17
> situation where one can be judged negatively by others (the “social evaluative threat”).


### id698707577
[[2024-03-27]] 09:19
> As stress increases, so does performance, at least for some time. This is the reason that a coach gives a rallying pep talk before an important sports event — a much-parodied movie cliché that can nonetheless improve team performance


### id698707845
[[2024-03-27]] 09:20
> nce. Athletes are also often seen purposefully putting themselves in higher stress situations before competitions (for instance by playing loud music or warming up vigorously) in order to improve focus, motivation, and performance.


### id698708564
[[2024-03-27]] 09:23
> With practice, complex tasks can become simpler. For instance, driving is initially a very complex task. Because learning to drive requires constant and effortful attention, one is unlikely to be playing “Harlem Shake” at top volume or casually chatting with friends at the same time


### id698708615
[[2024-03-27]] 09:23
> we become more experienced, driving becomes more automatic and much less effortful, though we might still turn down the radio volume or pause our conversations when merging into heavy traffic. The good news is that increased experience in a particular task can make its performance more resilient to the effects of stress.


### id698716353
[[2024-03-27]] 09:55
> pragmatic approach is to estimate the potential impact that stress can have on the outcome of an outage. To enable this, I’m introducing the concept of “stress surface,” which measures the perception of the four relative stressors during an outage: the novelty of the situation, its unpredictability, lack of control, and social evaluative threat. These four stressors are selected because they are present during most outages, are known to cause a stress response by the body, and therefore have the potential to impact performance


## New highlights added March 27, 2024 at 9:56 PM
### id698899566
[[2024-03-27]] 17:50
> Two effective ways to reduce the stress surface of an outage are training and postmortem analyses.


### id698963503
[[2024-03-27]] 20:34
> not endemic to engineers: despite overwhelming evidence that inexperience is one of the main causes of accidents in young drivers, they consistently fail to judge the extent of their own inexperience and how it affects their safety9


### id698967491
[[2024-03-27]] 20:58
> further quote Kahneman, “the law of small numbers is a manifestation of a general bias that favors certainty over doubt.”


### id698967630
[[2024-03-27]] 21:00
> This fast, intuitive, and largely automatic thinking is known as System 1 thinking


### id698967646
[[2024-03-27]] 21:00
> This is the thinking celebrated in Malcom Gladwell’s 2005 book Blink: The Power of Thinking Without Thinking.


### id698967947
[[2024-03-27]] 21:00
> To do so, you used your System 2 thinking, which, compared to System 1 thinking, is slower, non-automatic, and effortful.


### id698968459
[[2024-03-27]] 21:01
> System 1 thinking has two major shortcomings. First, it is rooted in memory and experience. Unless we’ve trained for years as archeologists, and have looked at literally thousands of archeological artifacts, we won’t be able to “take in” a new artifact and quickly determine its authenticity.


### id698969423
[[2024-03-27]] 21:03
> The second shortcoming of System 1 thinking is that it is prone to making systematic mistakes, which are called cognitive biases


### id698969853
[[2024-03-27]] 21:05
> System 1 is expert at quickly jumping to conclusions. It does so by employing mental shortcuts — heuristics — “which reduce the complex tasks of assessing probabilities and predicting values to simpler judgmental operations. In general, these heuristics are quite useful, but sometimes they lead to severe and systematic errors,”3
> otherwise known as cognitive biases.


### id698970456
[[2024-03-27]] 21:09
> During postmortems we evaluate what happened during an outage with the benefit of currently available information, i.e., hindsight. As we aim to identify the conditions that were necessary and sufficient for an outage to occur, we often uncover things that could have prevented or shortened the outage. We hear statements like “You shouldn’t have made the change without backing up the system first” or “I don’t know how I overlooked this obvious step” from solemn postmortem participants.


### id698970560
[[2024-03-27]] 21:10
> When the results of an outage are especially bad, hindsight bias is often accompanied by outcome bias, which is a major contributor to the “blame game” during postmortems. Because of hindsight bias, we first make the mistake of thinking that the correct steps to prevent or shorten an outage are equally obvious before, during, and after the outage. Then, under the influence of outcome bias, we judge the quality of the actions or decisions that contributed to the outage in proportion to how “bad” the outage was.


### id698971071
[[2024-03-27]] 21:12
> Outcome bias is also implicated in the way we perceive risky actions that appear to have positive effects. As David Woods, Sidney Dekker and others point out, “good decision processes can lead to bad outcomes and good outcomes may still occur despite poor decisions”9
> .
> For example, if an engineer makes changes to a system without having a reliable backup and this leads to an outage, outcome bias will help us quickly (and incorrectly) see these behaviors as careless, irresponsible, and even negligent. However, if no outage occurred, or if the same objectively risky action resulted in a positive outcome like meeting a deadline, the action would be perceived as far less risky, and the person who took it might even be celebrated as a visionary hero. At the organizational level, there is a real danger that unnecessarily risky behaviors would be overlooked or, worse yet, rewarded.


## New highlights added March 28, 2024 at 4:07 AM
### id699031463
[[2024-03-27]] 23:17
> demonstration of the effects of the availability bias (also known as the recency bias), which causes us to overestimate (sometimes drastically) the probability of events that are easier to recall and underestimate that of events that do not easily come to mind


### id699031164
[[2024-03-27]] 23:17
> The availability bias impacts outages and postmortems in several ways. First, in preparing for future outages or mitigating effects of past outages, we tend to consider scenarios that appear more likely, but are, in fact, only easier to remember either because of the attention they received or because they occurred recently


### id699029623
[[2024-03-27]] 23:16
> especially under stress, we often fall back to familiar responses from prior outages, which is another manifestation of the availability bias. If rebooting the server worked the last N times, we are likely to try that again, especially if the initial troubleshooting offers no competing narratives. In general, not recognizing the differences between outages could actually make the situation worse


### id699035478
[[2024-03-27]] 23:20
> This sometimes manifests as sunk cost bias, for example, when engineers are unwilling to try a different approach to solving a problem even though a substantial investment in a particular approach hasn’t yielded the desired results.


### id699048605
[[2024-03-27]] 23:24
> the positive “can do” attitude on display during outages is a symptom of overconfidence in our abilities to control the situation over which, in reality, we have little or no control (think: public cloud). There’s certainly nothing wrong with maintaining a positive attitude during a stressful event, but it’s worth keeping in mind that confidence is nothing but a feeling that is “determined mostly by the coherence of the story and by the ease with which it comes to mind, even when the evidence for the story is sparse and unreliable”12
> .


### id699048655
[[2024-03-27]] 23:25
> The best we can do is a compromise: learn to recognize situations in which mistakes are likely and try harder to avoid significant mistakes when the stakes are high13
> .


### id699048882
[[2024-03-27]] 23:30
> before working on critical or fragile systems — or, in general, before starting work on large projects — we can use a technique developed by Gary Klein called the PreMortem.

- [n] Exactly similar to a production or review checklist. Premotem is needed to build solid systems.  * [View Highlight](https://read.readwise.io/read/01ht1n3s2721d9s4cdqv3pvs05)


### id699049640
[[2024-03-27]] 23:31
> bright-eyed observing curiosity. And then what follows after that is
> reasoning about what one sees and asking: what’s going on here? And in that reasoning, intensely, it involves also a skepticism about one’s own understanding. The thinking eye must always ask: How do I know that? That’s probably the most powerful question of all time. How do you know that?" 15


### id699059198
[[2024-03-27]] 23:38
> The best way to work with mental phenomena is through mindfulness. Mindfulness has two components:
> The first component involves the self-regulation of attention so that it is maintained on immediate experience, thereby allowing for increased recognition of mental events in the present moment. The second component involves adopting a particular orientation toward one’s experiences in the present moment, an orientation that is characterized by curiosity, openness, and acceptance

- [n] Being present with curiousness, openness and acceptance  * [View Highlight](https://read.readwise.io/read/01ht1njrfszp4we6z2b4ph10mv)


### id699059558
[[2024-03-27]] 23:42
> We can similarly mitigate the effects of cognitive biases through mindfulness — we can become aware of when we’re jumping to conclusions and purposefully slow down to engage our analytical System 2 thinking.


