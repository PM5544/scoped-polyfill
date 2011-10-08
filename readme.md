# Scoped polyfill for HTML5 &lt;style scoped&gt; elements

This changes the actual &lt;style&gt; node in the DOM instead of computing the styles certain nodes might get and applying them on them inline.  
This is usefull when adding new nodes to a container which is "scoped".  
It does so by prepending the styleRules selectorText with id's to syntheticaly up the styleRules' specificity and thus overriding the styles from the root.

# Tested (and working) on:
IE 6, 7, 8 (i'll test it on IE9 soon)  
FF latest mac/Windows  
Google Chrome latest mac/Windows  
Opera latest Mac/Windows  
Safari latest Mac/Windows  


# Usage:
include scoped.js  
This will polyfill all scoped &lt;style&gt; nodes in the DOM at that point, when new ones are added later, you can call the function the constructor returns to convert that &lt;style scoped&gt; as well.  

If you're a jQuery user you can also use it as follows:
Pass in a jQuery object with &lt;style scoped&gt; nodes and it will polyfill them all.  

# Features:
Tests if scoped is supported and if it is it does nothing.  
If scoped is not supported by the browser visiting that page, an empty &gt;style&gt; element is made and appended to the body.  
This is because some browsers don't have a sheet property until appended to the DOM.  
Than it sorts out the different names browsers use to get to the same properties (like rule/cssRule and sheet/getSheet/styleSheet) and returns them into the closurre to only have to check those things once, after that you can just use the compat\[ name \] to access it.  
It also checks if the renaming of selectortext is prohibited or not because when changing the &lt;style&gt; its easier to just edit the selectorText instead of copying the rule, changing it and appending it to the &lt;style&gt; and removing the old one.  
 
 
# Notes:
This does not completely sandbox the CSS for the HTML inside the &lt;style scoped&gt;'s parentNode, it is meant to work the way scoped is going to work.  
This way you can inherit styles and override the ones you want to override without leaking those styles to the whole DOM.  




