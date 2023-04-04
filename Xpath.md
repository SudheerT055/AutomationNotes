# Xpath 

## Aboslute Xpath and Relative Xpath

Basic syntax of the Absolute Xpath is **/html/body/div/div[0]/div[3]/a/span**

Basic syntax of the Relative Xpath is **//tagName[@attributeName='value']**

## Starts-with

Starts-with function is very usefull for the elements which has dynamic attribute value 
Basic syntax of the Starts-with function is **//tagName[starts-with(@attributeName,'startingValue')]**

## contains

contains function is very usefull if you want to locate multiple elements with attribute having some similarities.
Basic syntax of the contains function is **//tagName[contains(@attributeName,'containText')]**

## text method

text function is used to locate the any tag with the same text value
Basic syntax of the text() is **//tagName[text()='actualText']**

## 'and' 'or' clause:

and & or will be usefull when you want to club two or more attribues or functions in xpath
Basic syntax of 'and' 'or' is 
- **//tagName[@attributeName='value' and @attributeName='value']**
- **//tagName[@attributeName='value' or @attributeName='value']**

## Xpath Axes methods:

we have many axes methods in xpath.
- 1. **self**:- sytax: **//tagName[@attributeName='value']//self::tagName[@attributeName='value']**
	- self method locates the element it self
- 2. **child**:- sytax: **//tagName[@attributeName='value']//child::tagName[@attributeName='value']**
	- child method locates it's child with provided tagName/attributeName
- 3. **parent**:- sytax: **//tagName[@attributeName='value']//parent::tagName[@attributeName='value']**
	- parent method locates it's parent with provided tagName/attributeName
- 4. **descendant**:- sytax: **//tagName[@attributeName='value']//descendant::tagName[@attributeName='value']**
	- descendant method locates it's all children and all grandchildren in the current node with the tagName provided
- 5. **descendant-or-self**:- sytax: **//tagName[@attributeName='value']//descendant-or-self::tagName[@attributeName='value']**
	- descendant-or-self method locates itself and it's all children and all grandchildren in the current node with the tagName
- 6. **ancestor**:- sytax: **//tagName[@attributeName='value']//ancestor::@tagName[@attributeName='value']**
	- ancestor method locates the parent and grandparent of the current node with the privided tagName
- 7. **ancestor-or-self**:- sytax: **//tagName[@attributeName='value']//ancestor-or-self::@tagName[@attributeName='value']**
	- ancestor-or-self method locates itself and the parent & grandparent of the current node with the privided tagName
- 8. **following**:- sytax: **//tagName[@attributeName='value']//following::@tagName[@attributeName='value']**
	- following method locates all the elements after the current node with the provided tagName
- 9. **following-sibling**:- sytax: **//tagName[@attributeName='value']//following-sibling::@tagName[@attributeName='value']**
	- following-sibling method locates only the elements with the same parent after the current node with the provided tagName
- 10. **preceding**:- sytax: **//tagName[@attributeName='value']//preceding::@tagName[@attributeName='value']**
	- preceding method locates all elements with the same parent before the current node with the provided tagName
- 11. **preceding-sibling**:- sytax: **//tagName[@attributeName='value']//preceding-sibling::@tagName[@attributeName='value']**
	- preceding-sibling method locates only the elements with the same parent before the current node with the provided tagName