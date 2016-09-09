---
title: Consume an OData Service with Create Option
description: Consume an OData Service with Create Option
tags: [  tutorial>intermediate, topic>html5, topic>odata, topic>sapui5, products>sap-hana ]
---
## Prerequisites  
 - **Proficiency:** Intermediate
 - **Tutorials:** [Use OData Metadata to dynamically create the columns](http://go.sap.com/developer/tutorials/xsa-sapui5-metadata.html)

## Next Steps
 - Select a tutorial from the [Tutorial Navigator](http://go.sap.com/developer/tutorial-navigator.html) or the [Tutorial Catalog](http://go.sap.com/developer/tutorials.html)

## Details
### You will learn  
Consume an OData Service with Create Option

### Time to Complete
**15 Min**.

---

1. You will begin by making a copy of the previous exercise.

	![copy](1.png)

2. Highlight the `resources` folder and right mouse click. Choose Paste.

	![paste](2.png)

3. In the copy folder dialog, give the new Name as `odataCRUD`.

	![copy folder](3.png)

4. Much of the startup logic will be the same. In the `Component.js` file change the service URL to: `/xsodata/user2.xsodata/`. We must also setup the model binding mode. Change the first part of the `Component.js` file to match the code you see here.

	```
	jQuery.sap.declare("sap.shineNext.odataBasic.Component");
	```

5. Also in the `Component.js` change the page creation to new `sap.ui.xmlview(“app”, “view.App”)`

	```
		var oView = sap.ui.view({
	```
	
6. Instead of a JavaScript view you are going to use an XML view. Therefore you can delete the `App.view.js` file and then create an `App.view.xml` file instead.

	![xml view](6.png)

7. The complete View Implementation for `App.view.xml` is provided for you as a template.  It has a table control built from the OData service  `/xsodata/user2.xsodata/` - all of which is very similar to the earlier exercise. In addition, this view has input fields for creating a new record. It also has the ability to update records in the table control; not just display them. The template can be accessed at: `http://<hostname>:51013/workshop/admin/ui/exerciseMaster/?workshop=dev602&sub=ex4_14`

	![complete view](7.png)

8. In this exercise we will focus on the implement of the event handlers – which is all done in the `controller.js` file.
9. You need to add to event handlers, `onInit`, `callUserService` (which performs the creation of new records) and `callUserUpdate` (which updates records from the table) and `onErrorCall` (and error handler). Insert the empty functions in the controller as shown.

	![add event handlers](9.png)

10. For the `onInit` you need to create an empty JSON model for our input fields and set it into the view.

	```
	onInit : function(){
	```
	
11. For `callUserService`, you first need to get access to the model object. Next you need to create a JSON object with the service fields (`PERS_NO`, `FIRSTNAME`, `LASTNAME`, and `E_MAIL`). `PERS_NO` can get a hard coded value of “0000000000”.  The other fields should be read from the screen with the bound JSON model Finally you need to set a custom header of `content-type` with the value of `application/json;charset=utf-8` in the model. Then you can call the `model.create` function for the entity `/Users`. If you need help writing this code please refer to the solution at: `http://<hostname>:51013/workshop/admin/ui/exerciseMaster/?workshop=dev602&sub=ex4_15`

	```
	callUserService : function() {
	```
	
12. The implementation of `callUserUpdate` is actually much simpler. You are using two-way model binding therefore you need only ask the model to submit any pending changes and capture the response status events. If you need help writing this code please refer to the solution at: `http://<hostname>:51013/workshop/admin/ui/exerciseMaster/?workshop=dev602&sub=ex4_16`

	```
	callUserUpdate: function() {
	```

13. In the `onErrorCall` you want to be able to parse the error body to pull out the detailed error message. If you need help writing this code please refer to the solution at: `http://<hostname>:51013/workshop/admin/ui/exerciseMaster/?workshop=dev602&sub=ex4_17`

	```
	onErrorCall: function(oError){
	```
	
14. Save the files.
15. Test your application in a web browser using the Run option. The URL would be `/odataCRUD/`. Try both creating a new record and editing existing records. Also try creating a record with an invalid email address.

	![results](15.png)
	
	![exception](15a.png)



## Next Steps
 - Select a tutorial from the [Tutorial Navigator](http://go.sap.com/developer/tutorial-navigator.html) or the [Tutorial Catalog](http://go.sap.com/developer/tutorials.html)