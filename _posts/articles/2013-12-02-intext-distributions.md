---
layout: post
title: In-text distributions
description: "In-text distributions using LaTeX."
category: articles
tags: [LaTeX, Sparklines]
modified: 2013-12-02
image: 
  thumb: intextdistributions_thumb.png
  homepage: intextdistributions_thumb.png
comments: true
share: true
---

<figure>
	<a href="/images/intextdistributions_1_hists.png"><img src="/images/intextdistributions_1_hists.png"></a>
	<figcaption>Example of an intext histogram from my thesis.</figcaption>
</figure>
 
Example in-text distribution from my first year report.

Recently I picked up Tufte’s first book on displaying data, which features his in-text
 [sparklines](http://en.wikipedia.org/wiki/Sparkline). As always, a LaTeX package already exists.

Almost all health data has just too much variance in it for a normal sparkline,
 meaning some sort of kernel density function needs to be applied to smooth the data. 
 This is annoying – because when using it in-text, you don’t want to have to describe 
 how the line was smoothed.

Brilliantly though, the package authors also included a command to create histograms.
 I feel a lot more confident with these, as readers can clearly count the bins, and when 
 applied in-text the lack of y-axis isn’t important, as it’s obvious you are only 
 interested in the shapes. The best bit – the package is super simple to run (see below)!

{% highlight latex %}
\documentclass[12pt]{article}
 
\usepackage{sparklines} % makes inline curves
 
\begin{document}
 
Ten-year modelled CVD risk was 27.3 (SD 13.9, histogram 
    \begin{sparkline}{4} % start first sparkline
        \sparkspike .083 .69 % first is x spacing, second is height
        \sparkspike .25 .97
        \sparkspike .417 .42
        \sparkspike .583 .15
        \sparkspike .75 .04
        \sparkspike .917 .01
    \end{sparkline} % end of sparkline
) rest of sentance.
  
\end{document}
{% endhighlight %}