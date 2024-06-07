---
title: Why Didn't Google Cloud Buy HashiCorp?
full Title: Why Didn't Google Cloud Buy HashiCorp?
author: Forrest Brazeal
URL: https://newsletter.goodtechthings.com/p/why-didnt-google-cloud-buy-hashicorp
published date: 2024-04-29
category: articles
source: reader
tags: [medium/articles, author/Forrest_Brazeal, reader/reader, date/2024-05-04, area/reader]
created: 2024-05-04
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Forrest Brazeal]]
note:: 
source:: [[reader]]
url:: [articles URL](https://newsletter.goodtechthings.com/p/why-didnt-google-cloud-buy-hashicorp)
image_url:: [articles image URL](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1cc46e46-6520-427d-8209-3aae55c925d6_2048x2048.png)
category:: [[articles]]
date:: [[2024-05-04]]
last_highlighted_date:: [[2024-05-04]]
published_date:: [[2024-04-29]]
summary:: IBM acquired HashiCorp for $6.4 billion, leading to questions about IBM's future plans for HashiCorp's products. Google Cloud, despite potential benefits, did not acquire HashiCorp due to existing services, strategic considerations, and potential challenges. The acquisition by IBM may address HashiCorp's business model concerns, allowing the company to move forward under new ownership.


![rw-book-cover](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1cc46e46-6520-427d-8209-3aae55c925d6_2048x2048.png)

## Highlights
### id715155098
[[2024-05-04]] 12:21
> IBM has become such a shadowy afterthought[1](https://newsletter.goodtechthings.com/p/why-didnt-google-cloud-buy-hashicorp/#footnote-1) that I don’t think too many people have strong feelings about them anymore. The big question is whether they will ditch HashiCorp’s new BUSL licensing scheme and go back to a true open-source model for products like Terraform and Vault, and I think it speaks to people’s lack of a handle on what IBM is up to these days that a plausible sentiment is “[hey, they might do it](https://medium.com/@fintanr/on-ibm-acquiring-hashicorp-c9c73a40d20c)!”
> The main reaction from the community about HashiCorp spinning an increasingly narrow set of options into a $6.4 billion exit is “[Welp … good for them](https://x.com/adamhjk/status/1783527449554477227).” And when a community says *good for them,* it’s quite conspicuous what they’re not saying: *good for us.*
> But I want to raise a different question today: how the heck did we get to this point? Why was HashiCorp not snapped up long ago by a more viable cloud provider? Specifically: why did they not get bought by Google Cloud?
> On the surface it seems like a match made in heaven, doesn’t it?
> • Google Cloud is the number three cloud provider; a huge slice of their competitors’ customers use and love HashiCorp products every day. Seems like a chance to steal some new fans.
> • Google has historically cultivated a generous attitude toward open source. Hear those drums in the distance? That’s the cursed board game of Kubernetes floating down the river towards you *right now.* I bet they wouldn’t think twice about [donating Terraform to the Linux Foundation](https://opentofu.org/manifesto/), bringing the renegades at OpenTofu back into the fold.
> • Google Cloud has a long history of making large strategic ops acquisitions (Stackdriver, Mandiant, Chronicle). Adding Vault and friends to their product portfolio would not be out of character for them.
> • Google Cloud *already* treats Terraform pretty much as their default deployment option! (Technically they have a bespoke service called “Google Cloud Deployment Manager”, but it is deprecated in all but name and even GCP’s own evangelists will tell you to just use Terraform instead.)
> • I bet, if Google looked real hard under all the couch cushions, they could come up with 6.4 billion dollars.
> These are all superficially compelling reasons to go out and buy HashiCorp.
> But the reasons *not* to buy it are far more compelling—and, I think, underscore what a tough spot HashiCorp was in, and why I’m sure their reaction to signing the LOI with IBM was a huge sigh of relief.
> Why buy the cow when you can get the milk for free?
> This is the cynical reason. Google Cloud is grabbing close to 100% of the value of Terraform today from the OSS version. If they want a hosted Terraform service, they can just build one themselves.
> And, in fact, that’s exactly what they did. Last fall Google Cloud announced [Infrastructure Manager](https://cloud.google.com/blog/products/management-tools/introducing-infrastructure-manager-powered-by-terraform), a service that slips managed Terraform deployments right into your existing Google Cloud CI/CD pipelines.
> I was at Google when this rolled out, and a product manager on the service told me at the time that Infrastructure Manager really wasn’t intended to compete with HashiCorp Cloud Platform—after all, it was a very Google Cloud-specific solution designed to make Terraform feel like a seamless part of the GCP deployment experience.
> If you’re HashiCorp, of course, that’s the *last* thing you want: for Terraform to become an invisible substrate of the cloud providers. I happen to know that HashiCorp was NOT happy about the release of Infrastructure Manager. But there wasn’t much they could do other than change their license model.
> $6.4 billion is just the beginning
> But let’s say Google buys HashiCorp anyway, just for the PR bump and the sales talking points. That’s when you realize that $6.4 billion is just the cover charge, not the full tab.
> HashiCorp Cloud Platform (the hosted Terraform, Vault, etc that HC manages themselves, their nominal secret sauce) [runs on AWS](https://developer.hashicorp.com/hcp/docs/hcp) today. So now you’ve got to spend time and money on a huge migration, probably multiple years of planning and work.
> Also, to sell HashiCorp products into large enterprises you probably need to fund lots and lots and lots more enterprise support and solutions architects, the competencies Google Cloud is persistently the worst at.
> Oh yeah, plus—you’re already expending resources on the [Google Cloud Terraform provider](https://registry.terraform.io/providers/hashicorp/google/latest/docs). But now you’re stuck having to support and co-maintain providers for a pile of other partners, including [your biggest competitors](https://registry.terraform.io/providers/hashicorp/aws/latest). You are effectively paying for AWS and Azure to use your $6.4 billion dollar toy for free.
> IBM might be willing to take that deal if it means a snowball’s chance of being taken seriously as a for-real cloud provider, but I don’t think it really makes sense for Google Cloud.
> Which brings us to the existential question:
> Do you really, really want to be in the “hybrid cloud deployment” business?
> Like, what’s the strategic value for Google Cloud in being the Terraform fairy? People with AWS footprints aren’t going to use Google Cloud to manage state for their deployments, that’s just weird. Enormous companies have always preferred to roll their own infra platforms, meaning your real customers for managed Terraform, Consul, etc, are mostly mid-sized companies who have obnoxious price sensitivity. You’re taking on all the responsibility of keeping up with a notoriously fast-changing set of infrastructure tools while getting very unclear revenue potential in return.
> Heck, I don’t even think *HashiCorp* wanted to be in the hybrid cloud deployment business. Their recent public filings make it clear that they [couldn’t figure out](https://x.com/adamhjk/status/1783527454323462430) a SaaS business model and [weren’t confident](https://x.com/adamhjk/status/1783527460300378170) in their ability to become a services business.
> I think the only real argument for Google buying HashiCorp would come down to brand value and OSS goodwill. And as they’ve recently indicated by [firing all their Python maintainers](https://news.ycombinator.com/item?id=40171125), hard-to-quantify efforts to improve the OSS commons don’t carry the weight at Google that they once did.
> We’ll never know for sure, but I think those are the big reasons HashiCorp was never acquired by a major cloud provider.
> Anyway, HashiCorp eventually found a buyer that made sense, all these problems are IBM’s problems now, and hopefully the people who built one of the most truly remarkable and useful open-source software companies of all time can get a well-deserved night’s rest or two.
> In all sincerity: good for them.
> Cartoon of the day
> I, too, have been through an acquisition.
> [
> ![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1cc46e46-6520-427d-8209-3aae55c925d6_2048x2048.png)
> ](https://www.goodtechthings.com/acquisition-translator/)
> [1](https://newsletter.goodtechthings.com/p/why-didnt-google-cloud-buy-hashicorp/#footnote-anchor-1)
> I sometimes refer to them as “[Ichabod](https://en.wikipedia.org/wiki/Ichabod) Business Machines”. Nobody gets me.


