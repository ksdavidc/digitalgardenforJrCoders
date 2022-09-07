---
{"dg-publish":true,"permalink":"/prep-notes/how-to-show-scratchblocks-inline/","dgHomeLink":true,"dgPassFrontmatter":false}
---


none of these render code in preview.
What I really want it for them to render markdown in both preview and reading.

# 1
<div><span >This is super simple, a **div** and a *span* and a pre and a code, with no style info at all, except the code is class="scratchblock language-scratchblock" <pre ><code class="scratchblock language-scratchblock">move (1005) steps</code></pre> in a sentence. The problem is it won't display markdown.</span>
</div>




## 2
This markdown seems to work. It is the same as the above, but no div. But it is not inline.

Somehow, <span style="display: inline;" markdown=1>This is a span then a pre both with display set to inline, markdown=1, and no div. It renders the *markdown* and the **scratchblock** code in reading and preview but <pre style="display: inline;" markdown=1><code class="scratchblock language-scratchblock">move (1005) steps</code></pre> the problem is only the following text is inline.</span>
  

<span >This is same as above, but without the displays set to inline, i.e. a span without display set to inline, and no div. It renders the *markdown* and the **scratchblock** code <pre style=""><code class="scratchblock language-scratchblock">move (1005) steps</code></pre>but only the following text is inline.</span>



## 3
<div>this is a div, a pre, and a code of class="*scratchblock language-scratchblock*" with scratch code such as <pre ><code class="scratchblock language-scratchblock">move (1005) steps</code></pre>all in a sentence. The markdown does not render in reading, but does in preview, but the code renders in reading, not in preview.</div>

# 4
These both render very badly in preview.
<p style="display: inline;" markdown=1>This is a p with **display** set to *inline*, instead of a div.<span style="display: inline;" markdown=1> Inside is a span that doesn't render the *markdown* even with markdown set, but renders the **scratchblock** code<pre style="display: inline:"><code class="scratchblock language-scratchblock">move (1005) steps</code></pre>and all the text is inline.</span></p>

<p markdown=1>This is the above without **display** set to *inline*. The priro text doesn't render inline, as expected.<span >Inside is a span that doesn't render the *markdown* even with markdown set, but renders the **scratchblock** code<pre ><code class="scratchblock language-scratchblock">move (1005) steps</code></pre>but only the following text is inline.</span></p>

# 5

<div markdown=1><span style="display: inline;" markdown=1>This is a span with display set to inline, markdown=1, and a div. It doesn't the *markdown* but the **scratchblock** code <pre style="display: inline:"><code class="scratchblock language-scratchblock">move (1005) steps</code></pre>is fine and all the text is inline.</span></div>