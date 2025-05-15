---
title: "Workflow API"
date: 2025-05-15T14:19:50+10:00
draft: true
---

# Methods

<table class="confluenceTable" data-layout="default"
data-local-id="dcbe40f9-fd5b-4b29-b0ce-bf745d514ae8">
<tbody>
<tr>
<th class="confluenceTh"><p>Method</p></th>
<th class="confluenceTh"><p>Description</p></th>
<th class="confluenceTh"><p>Notes</p></th>
</tr>
&#10;<tr>
<td class="confluenceTd"><div class="code panel pdl"
style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1"
data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence"
data-theme="Confluence"
style="brush: java; gutter: false; theme: Confluence"><pre
class="sourceCode java"><code class="sourceCode java"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="fu">forceToActivity</span><span class="op">(</span></span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a>  <span class="co">/* string */</span>  activityName<span class="op">,</span> </span>
<span id="cb1-3"><a href="#cb1-3" aria-hidden="true" tabindex="-1"></a>  <span class="co">/* record */</span>  tableRecord<span class="op">,</span> </span>
<span id="cb1-4"><a href="#cb1-4" aria-hidden="true" tabindex="-1"></a>  <span class="co">/* boolean */</span> explicitUpdate<span class="op">,</span> <span class="co">//same as a current.Update()</span></span>
<span id="cb1-5"><a href="#cb1-5" aria-hidden="true" tabindex="-1"></a>  <span class="co">/* boolean */</span> enableTriggers</span>
<span id="cb1-6"><a href="#cb1-6" aria-hidden="true" tabindex="-1"></a><span class="op">)</span></span></code></pre></div>
</div>
</div></td>
<td class="confluenceTd"><p>Forces a workflow to the specified activity.
Useful for aborting a workflow.</p></td>
<td class="confluenceTd"><p><br />
</p></td>
</tr>
</tbody>
</table>
