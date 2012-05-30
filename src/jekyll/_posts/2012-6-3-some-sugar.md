---
layout: default
title: ""
published: true
data:
  x: 1600
  y: -450
  z: 980
  rotate: 60
---

# Some sugar#

<div class="highlight"><pre><code class="scala"><span class="k">def</span> getStatistics(user<span class="kt">: User</span>)<span class="kt">: Future[Statistics]</span> = {
  <span class="k">val</span> projects<span class="kt">: Future[Seq[Project]]</span> = api.projects(user)
  <span class="k">val</span> requests<span class="kt">: Future[Seq[PullRequest]]</span> = <span class="k">for</span> {
       ps <span class="k">&lt;-</span> projects
       requests <span class="k">&lt;-</span> Future.traverse(projects)(api.pullrequests)
    } <span class="k">yield</span> requests.flatten
  <span class="k">val</span> watchers<span class="kt">: Future[Seq[User]]</span> = ...
  <span class="k">for</span>((r,w) &lt;- requests zip watchers)
  <span class="k">yield</span> Statistics(user, r, w)
}
</code></pre></div>