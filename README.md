# Service Portal Documentation
This reference guide contains documentation for Service Portal Developers.

>This site is nonofficial and not endorsed by ServiceNow.

### Index
[Widget Dependencies](/Widget_Dependencies.md)

[Widget Server Script](/widget_server_script.md)

[Widget CSS](/widget_css.md)

[Widget HTML](/widget_html.md)

[Widget Client Script](/widget_client_script.md)



### Service Portal
Service Portal contains of two parts: 
- *Framework*: a set of APIs and [Angular.js](https://angularjs.org/) services and directives that help to render portals.
- *Portals*: a group of pages linked by their pageId. For example: `sp_config` is a Portal contains a set tools to help you configure and create and mantain widgets.

### Portal Configuration

| Property | Description |
| :------ | :----------- |
| Title   | Page `title` |
| Url Suffix | helps to namespace the portal from other portals. |
| Homepage    | The first page that the portal will load |
| Knowledge base | Default knowledge base |


### Page
A page is a collection of containers rows and columns that contain widgets built using the Service Portal Designer. Pages are referenced by their Page ID. Pages can be used on multiple portals.

### Widget
A widget is a superset of an Angular 1.x directive that is tightly coupled to a server-side JavaScript code block powered by the Rhino engine under the ServiceNow platform.
Since widgets are `read-only` to benefit from future updates, you can't update their code. If you need to make major changes,
clone the widget and give it another `name` and `id`.

### Widget Instance
A widget instace is a reference to a widget that contains: location, properties and CSS especific for that instance. A widget used multiple times in the same page, will use multiple instances.


### Embeded Widgets
The spWidget directive takes a widget model and renders the compiled widget exactly where you put it in your HTML Template. 

```html
<sp-widget widget="c.myCatItemWidget"></sp-widget>
```


### $sp API
Service Portal provides a set of convenience methods found on the global `$sp` object, which is available in any widget server script.

<table width="100%">
	<tr>
		<th valign="top" colspan="3" align="left"><a href="#props" name="props">$sp</a></th>
	</tr>
	<tr>
		<th valign="top" width="120px" align="left">Method</th>
		<th valign="top" align="left">Description</th>
	</tr>
	<tr>
		<td valign="top"><code>getPortalRecord()</code></td>
		<td valign="top">Returns the portal's GlideRecord</td>
	</tr>
	<tr>
		<td valign="top"><code>getValue(/*String*/ name)</code></td>
		<td valign="top">Returns the value of the specified field. Null if the request does not exist or has no such parameter, the instance does not exist or has no such parameter, or the portal is null or has no such parameter</td>
	</tr>
	<tr>
		<td valign="top"><code>getWidgetParameters()</code></td>
		<td valign="top">Returns the widget's parameters in an object, or an empty object if the widget has no parameters.</td>
	</tr>
	<tr>
		<td valign="top"><code>getDisplayValue(/*String*/ name)</code></td>
		<td valign="top">Returns the display value of the specified parameter. Returns an empty string if the request, instance, and portal do not exist. Returns null if the request exists but has no such parameter, or the instance exists but has no such parameter.</td>
	</tr>
	<tr>
		<td valign="top"><code>getValues(/*Scriptable*/ data, /*String*/ names)</code></td>
		<td valign="top">Copies values from the request or instance into the data parameter. Returns void.</td>
	</tr>
	<tr>
		<td valign="top"><code>getValues(/*Scriptable*/ data)</code></td>
		<td valign="top">Copies values from the instance GlideRecord into the data parameter. Returns void.</td>
	</tr>
	<tr>
		<td valign="top"><code>getRecordValues(/*Scriptable*/ data, /*GlideRecord*/ from, /*String*/ names)</code></td>
		<td valign="top"Copies values of the specified field names into the data parameter. Returns void.></td>
	</tr>
	<tr>
		<td valign="top"><code>getRecordDisplayValues(/*Scriptable*/ data, /*GlideRecord*/ from, /*String*/ names)</code></td>
		<td valign="top">Copies display values of the specified field names into the data parameter. Returns void.</td>
	</tr>
	<tr>
		<td valign="top"><code>getRecordElements(/*Scriptable*/ data, /*GlideRecord*/ from, /*String*/ names)</code></td>
		<td valign="top">Copies the record element's name, display value, and value into the data parameter. Returns void.</td>
	</tr>
	<tr>
		<td valign="top"><code>getWidgetScope(/*String*/ instanceID)</code></td>
		<td valign="top">Used for including a widget inside another widget (eg. menu inside header). InstanceID can be a widget instance sys_id or ID. Returns a widget, or an empty object if the instanceID is empty or invalid.</td>
	</tr>
	<tr>
		<td valign="top"><code>getWidgetFromInstance(String instanceID)</code></td>
		<td valign="top">Returns a widget from the specified instance.</td>
	</tr>
	<tr>
		<td valign="top"><code>getWidget(/*String*/ widgetID, /*Object*/ widgetParams)</code></td>
		<td valign="top">Used for including a widget inside another widget without a instance.<pre>var w = $sp.getWidget('widget_id', {p1: param1, p2: param2});</pre></td>
	</tr>
	<tr>
		<td valign="top"><code>getRelatedList(/*String*/ tableName, /*String*/ foreignKey)</code></td>
		<td valign="top">Gets the related list of data for a instance. Returns [{}, {}, ...]</td>
	</tr>
	<tr>
		<td valign="top"><code>getParameter(/*String*/ name)</code></td>
		<td valign="top">Returns the value of the specified parameter from URL, JSON Body.</td>
	</tr>
	<tr>
		<td valign="top"><code>getRecord()</code></td>
		<td valign="top">GlideRecord for instance / input parms. Returns null if the GlideRecord cannot be found.</td>
	</tr>
	<tr>
		<td valign="top"><code>getVariables()</code></td>
		<td valign="top">Returns the table's variables.</td>
	</tr>
	<tr>
		<td valign="top"><code>getFilterBreadcrumbs(/*String*/ table, /*String*/ query, /*String*/ fixedQuery)</code></td>
		<td valign="top">Returns an array of objects where each object contains the breadcrumb label, value, and flags for if fixed and if removed.</td>
	</tr>
	<tr>
		<td valign="top"><code>getRecordVariables(/*GlideRecord*/ gr)</code></td>
		<td valign="top">Returns the task variables.</td>
	</tr>
	<tr>
		<td valign="top"><code>getVariablesArray()</code></td>
		<td valign="top">Returns the tables variables.</td>
	</tr>
	<tr>
		<td valign="top"><code>getRecordVariablesArray(/*GlideRecord*/ gr)</code></td>
		<td valign="top">Returns the records variables</td>
	</tr>
	<tr>
		<td valign="top"><code>getStreamEntries()</code></td>
		<td valign="top">Get activity stream entries by the instance context.</td>
	</tr>
	<tr>
		<td valign="top"><code>getStream()</code></td>
		<td valign="top">Get the activity stream by the instance context.</td>
	</tr>
	<tr>
		<td valign="top"><code>getStream(/*String*/ table, /*String*/ sys_id)</code></td>
		<td valign="top">Get the activity stream for a record.</td>
	</tr>
	<tr>
		<td valign="top"><code>getListColumns(/*String*/ tableName)</code></td>
		<td valign="top">Returns list of columns for the specified table's mobile view</td>
	</tr>
	<tr>
		<td valign="top"><code>getListColumns(/*String*/ tableName, /*String*/ view)</code></td>
		<td valign="top">Returns a list of the specified table's columns in the specified view</td>
	</tr>
	<tr>
		<td valign="top"><code>getUserInitials()</code></td>
		<td valign="top">Returns the user's initials as a string</td>
	</tr>
	<tr>
		<td valign="top"><code>getField(/*GlideRecord*/ gr, /*String*/ name)</code></td>
		<td valign="top">Returns the field's information</td>
	</tr>
	<tr>
		<td valign="top"><code>getFields(/*GlideRecord*/ gr, /*String*/ names)</code></td>
		<td valign="top">Checks the specified field names, and returns a comma seperated list of valid names.</td>
	</tr>
	<tr>
		<td valign="top"><code>getFieldsObject(/*GlideRecord*/ gr, /*String*/ names)</code></td>
		<td valign="top">Checks the specified field names, and returns an object containing the valid names.</td>
	</tr>
	<tr>
		<td valign="top"><code>logStat(/*String*/ type, /*String*/ table, /*String*/ id, /*Optional String*/ text)</code></td>
		<td valign="top">Adds a record to the Service Portal statistics log</td>
	</tr>
	<tr>
		<td valign="top"><code>logSearch(/*String*/ table, /*String*/ terms, /*int*/ count)</code></td>
		<td valign="top">Adds a record to the Service Portal statistics log, specifically for a search</td>
	</tr>
	<tr>
		<td valign="top"><code>canSeePage(/*String*/ pageID)</code></td>
		<td valign="top">Determines if the user is allowed to see the specified page</td>
	</tr>
	<tr>
		<td valign="top"><code>canReadRecord(/*GlideRecord*/ gr)</code></td>
		<td valign="top">Determines if the user can read the specified GlideRecord</td>
	</tr>
	<tr>
		<td valign="top"><code>canReadRecord(/*String*/ table, /*String*/ id)</code></td>
		<td valign="top">Determines if the user can read the specified GlideRecord</td>
	</tr>
	<tr>
		<td valign="top"><code>getCatalogItem(/*String*/ itemID)</code></td>
		<td valign="top">Returns the catalog item</td>
	</tr>
	<tr>
		<td valign="top"><code>getForm(/*String*/ table, /*String*/ sys_id, /*Optional String*/ encodedQuery, /*Optional String*/ view)</code></td>
		<td valign="top">Returns the form</td>
	</tr>
	<tr>
		<td valign="top"><code>getKBCategoryArticles(/*String*/ category, /*Optional int*/ limit)</code></td>
		<td valign="top">Returns KB articles in the specified category, includes all subcategories.</td>
	</tr>
	<tr>
		<td valign="top"><code>getKBSiblingCategories(/*String*/ categoryID)</code></td>
		<td valign="top">Returns KB categories with the same parent as the specified category.</td>
	</tr>
	<tr>
		<td valign="top"><code>getKBCount(/*String*/ knowledgeBaseID)</code></td>
		<td valign="top">Returns the number of KB articles</td>
	</tr>
	<tr>
		<td valign="top"><code>getSubCategories(/*String*/ categoryId)</code></td>
		<td valign="top">Returns the KB subcategories of the specified category</td>
	</tr>
	<tr>
		<td valign="top"><code>getKBTopCategoryID(/*String*/ catId)</code></td>
		<td valign="top">Returns the top category in the hierarch containing the specified category.</td>
	</tr>
	<tr>
		<td valign="top"><code>getKBRecord()</code></td>
		<td valign="top">Returns KB record for the portal's knowledge base with workflow_state = published in the query</td>
	</tr>
	<tr>
		<td valign="top"><code>getSCRecord()</code></td>
		<td valign="top">Returns the service catalog record for the portal's catalog with proper class name and active = true in the query</td>
	</tr>
	<tr>
		<td valign="top"><code>stripHTML(/*String*/ html)</code></td>
		<td valign="top">Removes non breaking spaces from the specified string</td>
	</tr>
	<tr>
		<td valign="top"><code>getMenuItems(/*String*/ sys_id)</code></td>
		<td valign="top">Returns the menu items for the specified instance</td>
	</tr>
	<tr>
		<td valign="top"><code>getMenuHREF(/*GlideRecord*/ gr)</code></td>
		<td valign="top">Builds the href (?id=) portion of the URL for the specifed page</td>
	</tr>
	<tr>
		<td valign="top"><code>log(/*Object*/ message)</code></td>
		<td valign="top">Sends the message to the console log</td>
	</tr>
</table>
---
## Widget Dependencies
In Service Portal, it is possible to link Javascript and CSS files to widgets. This allows developers to create dependencies between their widgets and third party libraries, external style sheets, and angular modules. Dependencies are only fetched from the server at the time that they are needed, which keeps initial page loads very fast. 

Following is a step-by-step guide on creating new dependency packages and associating them with widgets.

### Creating a Dependency Package
A dependency package is a collection of Javascript and CSS files that can be then connected to a widget. Dependencies can be found in the table `sp_dependency`, or by navigating to the Service Portal module in the navigator and selecting the Dependencies submodule.

In a dependency record, you will define the following: 

1. Name - The name that your dependency will be referred to by (Useful for selecting a dependency from a dropdown list)

2. Include on page load - Select if you want your dependency to be loaded onto the page on initial page load of Service Portal, or leave unchecked to load the dependency only when the linked widget is loaded onto a page.

3. Angular module name - Only necessary if the linked Javascript is an Angular module. Provide the name of the Angular module name that you are loading in, so that it can be injected into the Service Portal angular application. Leave blank if not applicable.

Once these fields are defined, you can start creating records in the `sp_js_include` and `sp_css_include` table and adding them to the JS Includes and CSS Includes related lists in a dependency record.
