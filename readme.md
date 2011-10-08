<h1>Scoped polyfill for HTML5 &lt;style scoped&gt; elements</h1> 

<p>This changes the actual <style> node in the DOM instead of computing the styles certain nodes might get and applying them on them inline.
This is usefull when adding new nodes to a container which is "scoped".<br />
It does so by prepending the styleRules selectorText with id's to synteticly up the styleRules' specificity and thus overriding the styles from the root.
</p>

<h2>Tested on:</h2>
<ul><li>IE 6, 7, 8
<li>FF latest mac/Windows
<li>Google Chrome latest mac/Windows
<li>Opera latest Mac/Windows
<li>Safari latest Mac/Windows
</ul>

<h2>Usage:</h2>
<ol>
<li>include scoped.js<br/>This will polyfill all scoped <style> nodes in the DOM at that point, when new ones are added later, you can call the function the constructor returns to convert that <style scoped> as well.
</ol>

<p>If you're a jQuery user you can also use it as follows:<br />
Pass in a jQuery object with <style scoped> nodes and it will polyfill them all.</p>

<h2>Features:</h2>
<p>Tests if scoped is supported and if it is it does nothing.<br />
If scoped is not supported by the browser visiting that page, an empty <style> element is made and appended to the body.<br />
This is because some browsers don't have a sheet property until appended to the DOM.<br />
Than it sorts out the different names browsers use to get to the same properties (like rule/cssRule and sheet/getSheet/styleSheet) and returns them into the closurre to only have to check those things once, after that you can just use the compat[ name ] to access it.<br />
It also checks if the renaming of selectortext is prohibited or not because when changing the <style> its easier to just edit the selectorText instead of copying the rule, changing it and appending it to the <style> and removing the old one.</p>
 

<h2>Notes:</h2>
<p>This does not completely sandbox the HTML inside the &lt;style scoped&gt;'s parentNode, it is meant to work the way scoped is going to work.<br />This way you can inherit styles and override the ones you want to override without leaking those styles to the whole DOM.</p>
