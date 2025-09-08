---
title: Linux in Academia, an Experiment
toc: true
breadcrumbs: false
date: 2024-09-08
---

Throughout the four years of my PhD in computational materials science at Purdue University, I've spent absurd amounts of time with my computer. A back-of-the-envelope calculation would suggest it's been over 80,000 hours! Knowing that I'll be spending this inordinate amount of time this way, and motivated by [this XKCD comic](https://xkcd.com/1205/), I've invested a lot of time reducing friction in my computer use. To name a few of these optimizations: adopting [alternative keyboard layouts](https://colemak.com/), learning [competitive typing](https://monkeytype.com/profile/allokate), using a package manager, and using tiling window managers have all saved massive amounts of time. However, like many computer geeks before me, I repeatedly find myself asking one question over and over: 

> Which operating system should I use?

The choice of operating system (OS), the base layer of my computer, underpins the entire system I use to interact with it. Arguably, it's been more debilitating to switch between OSes than it was to switch from QWERTY to COLEMAK. I've tried various operating systems the last four years, but I've never switched to Linux as my daily driver. Each time I try, I'm quickly tempted back by the convenience of macOS. To remedy this, I tried switching to Linux completely for a month, to find out what works, what doesn't, and if it's possible to survive using Linux in a competitive academic setting.

{{< callout type="warning" >}}
   [I'd just like to interject for a moment. What you're referring to as Linux, is in fact, GNU/Linux, or as I've recently taken to calling it, GNU plus Linux. Linux is not an operating system unto itself, but rather another free component of a fully functioning GNU system made useful by the GNU corelibs, shell utilities and vital system components comprising a full OS as defined by POSIX.](https://stallman-copypasta.github.io/))
{{< /callout >}}



## Previous experiences with Windows/macOS/Linux

Like most engineers, I started graduate school using Windows. It works, mostly! And if you've never explored outside it, there's not much incentive to change. I used Windows for the first year of my PhD, tinkering with a Linux dual-boot for a while but never using it for my research. A week before my preliminary exams, my Windows laptop suddenly started crashing constantly, and I bought an M2 MacBook for something that *just works* to pass my exam. It worked beautifully!

<!-- TODO: add a photo of my MacBook -->

I'd make the case that the M-series MacBook Airs are currently the best laptops you can buy for grad school. The all-metal chassis, passive cooling, and M-series chips make for extremely long battery life and snappy performance. I consistently get 12+ hours of battery life on my Mac. Beyond hardware, macOS is extremely smooth, with an intuitive UI and great package support through [homebrew](https://brew.sh/). While the devs at [Asahi Linux](https://social.treehouse.systems/@AsahiLinux) have done some amazing work to get Linux running on M1/M2 MacBooks, the limited external monitor support was a deal-breaker in graduate school, where giving presentations and seminars are a regular occurrence.

## The Experiment: Linux for One Month

This idea was motivated by the [Old Computer Challenge](https://occ.sdf.org/), which encourages us to experience older computer hardware to develop a deeper appreciation of our technology. I dug up my old laptop, installed Linux, and decided I would try to stick it out for a month. Hardware-wise, it's not exactly a fair comparison. The newer M2 Mac easily beats my Dell XPS 7950 on most benchmarks, despite having paid twice as much for my XPS. I've attempted to account for this disparity in performance in this post. Additionally, I restricted myself to only use [free software](https://www.fsf.org/), using LibreOffice for document editing and my browser for video conferencing.

<!-- TODO: add photo of XPS  -->

{{< callout type="info" >}}
  Okay, but which Linux distro? *Just choose one that works for you!* Everyone has different levels of experience, enthusiasm, and philosophies with Linux. I personally use **NixOS**; while the learning curve has been steep, reproducible and declarative builds are well worth the effort to me. For an easier time, **Fedora** is an easy-to-use distro with great package support.
{{< /callout >}}

### The Good

Immediately, I was refreshed to see how smooth the installation and configuration process was. After spending years on using high-performance computing systems running Linux, I felt at home on the CLI. Setting up my tiling window manager, desktop environment, and using my package manager were a breeze. Having that level of control over my system was extremely satisfying. Additionally, this meant that the time I spent configuring my system was often transferable to my research, unlike more OS-specific configuration done on macOS or Windows. I've since been using many utilities I discovered in this experiment for my supercomputer projects.

Despite the strict restriction of only using free software, I found that nearly all the software I frequently use was well-supported on Linux. Very rarely, I had to compile something myself. I've previously felt cognitive dissonance knowing the benefits of free software and yet using closed-source macOS. It became much easier to sleep at night after resolving this dissonance and using open-source Linux. This appeased some of my privacy concerns as well. In many cases, I was pleasantly surprised to find better software on Linux than I had on macOS; for example, the tiling window managers are significantly more limited on macOS.

### The Bad

There's an expression that goes around online Linux circles often, that *Linux is free if you don't value your time!* This experiment was an attempt to test that hypothesis; unfortunately, there proved to be some truth to it. Initially, I was forced to spend a lot of time configuring my system in ways I wouldn't have to on macOS. It's worth noting that near the end of the month, this time began to decrease and plateau. Using Linux is a commitment that requires more frequent configuration. This isn't all bad — it leads to a better understanding of your computer — but it's extra time that has to come from somewhere. In graduate school, where constant deadlines and pressure from advisors are ubiquitous, time is a rare commodity. Thinking back to the XKCD comic from earlier, I would estimate that required time investment in Linux “pays off” on the order of years or decades, not weeks or months.

While it was exacerbated by my decision to impose a free software-only constraint, there are a few packages important in graduate school which are missing or offer limited functionality on Linux. Most notably: Microsoft Office. I tried to love LibreOffice, but it fails to excite for documents with tracked changes, equations, figures, and references. It was unusable for the manuscripts that I needed to edit. Instead, I used Office online, which is flawed in its own ways. Near the end of this month, I tinkered with using Wine to install Microsoft Office, but struggled to achieve full feature parity with macOS and Windows.

### The Ugly

Coming from a passively-cooled MacBook Air, the most shocking adjustment was the battery life. Apple controls the entire device manufacturing process, and it shows. I frequently get 12+ hours of battery life on my MacBook, and charging is never on my mind. Intel and AMD machines are yet to compete with this level of efficiency. Beyond the hardware differences, using Linux on my MacBook results in about 1/2 of the battery life compared to macOS. When I was performing a typical research task on my XPS with an IDE, browser, and reference manager, my laptop ran hot and noisy. The battery life suffered: I struggled to squeeze 3-4 hours of battery life out of my machine, and a charger became my frequent travel companion. This isn't entirely awful, it's a compromise that can be made, but it's a rough adjustment when considering the other options out there for operating systems.

While my experience was generally smooth, I noticed significant degradation in performance while video conferencing. Most worrying, my computer crashed during an important virtual research meeting, and I noticed it extremely sluggish during other video conferences. Additionally, the Bluetooth compatibility of both my headphone options (AirPods and Bose QC) was limited, with microphones significantly distorted compared to macOS. It's likely that this could be fixed with more configuration, but initial debugging was not promising.

## Conclusions

Spending a month using Linux as my daily driver reminded me why I love computing, and I felt less friction with my computer. Instead, the friction came externally from graduate school pressure. Competitive academic environments fall somewhere between neutral to openly hostile towards Linux and its peculiarities. It's difficult to justify nuanced software choices and Linux-induced delays to collaborators who don't share your philosophy of free software. I'm currently writing this on my MacBook. When I'm out of grad school and under less pressure, I'd love to try again.