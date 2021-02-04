# Functional design document #
## for "Tembo" (initial release: version 1.1.0)

Author: [Josh Senyak](mailto://josh.senyak@quicksilverconsulting.com) at [Quicksilver Consulting](https://quicksilverconsulting.com)

Document version: 1.0

Date: 2/4/21

Latest version available here: [https://github.com/jsenyak/tembo/blob/main/docs/Tembo%20-%20Functional%20design%20document.md](https://github.com/jsenyak/tembo/blob/main/docs/Tembo%20-%20Functional%20design%20document.md)

Document license: ![](https://i.creativecommons.org/l/by-nc-sa/4.0/80x15.png) This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.



----------

Contents of this document:

1. [About this document](#AboutThisDocument)
1. [Summary description of Tembo](#SummaryDescription)
1. [Vocabulary](#Vocabulary)
1. [Summary of features](#SummaryOfFeatures)
1. [Interview process - detail](#InterviewDetail)
1. [Description of a Tembo application](#ApplicationDescription)
1. [Features for future versions](#FeaturesForFuture) 
1. [Questions outstanding](#QuestionsOutstanding)

----------

### 1. <a id="AboutThisDocument"></a>About this document
This Functional Design Document describes the functionality of “Tembo,” a software package now under development. In this document we describe functionality for the initial release of Tembo. 

This document does not describe the underlying implementation (code, routines, data structures) by which Tembo will accomplish this functionality.

Since Tembo is an open source project, suggestions and improvements to this document are gratefully solicited. 

This document describes the functionality of the initial release of Tembo (version 1.1.0). This version of Tembo is intended as a proof of concept, that is, as the simplest possible version that can accomplish the overall purpose  of the Tembo software. In addition, this document includes [notes on functionality](#FeaturesForFuture) suggested for future versions. 

### 2. <a id="SummaryDescription"></a>Summary description of Tembo
Tembo is a WordPress plugin that allows a user (the "developer") to create web-based relational database applications quickly and easily. 

Tembo creates the new application as a WordPress plugin, making it extremely easy to install, deploy and share. 

Once the application has been completed, a developer may simply use it for personal purposes. Or the developer may share it with other users of the developer's own WordPress site. More ambitiously, a developer could distribute the application widely to a general public.

* ***An example***: 

    A developer who enjoys birdwatching might use Tembo to create a database application to track favorite local hiking trails and the various birds spotted at different times along each trail. The developer would install Tembo as a plugin on a personal Wordpress site, then use Tembo to create a "Trails and Birds" application as a separate plugin on the same site.

    This application might be only for the developer's personal use. Or the developer might choose to share the database with a group of other local birdwatchers, to build up a shared data resource. Either way, the developer could integrate the application with the developer's main WordPress site if desired (for example, creating a widget on the home page showing the number of new bird species seen in the past 30 days). Most ambitiously, the developer could then distribute the "Trails and Birds" application like any other WordPress plugin, so that other birdwatchers anywhere in the world could install the plugin into their own WordPress sites and keep their own shared, local databases of hiking trails and birds seen.

Tembo walks the developer through the development process using an interview-style work flow. A developer must have a basic grasp of the meaning of database tables, fields and relations. (Instructional materials will be available for developers who are new to these basic database concepts.) Beyond that, the developer is not expected to have any knowledge of database theory or software coding. When the interview process is complete, Tembo builds out the application as a complete WordPress plugin.

Tembo implements the [Web Monetization](https://webmonetization.org/) protocol, giving developers the option to monetize some or all of their application. Usually, web monetization involves very small amounts of money transferred from the visitor to the creator of a web site. For example, certain parts of the application may be reserved for users who have implemented Web Monetization in their browser.

After Tembo has built out the application, a developer who is experienced in database design and web development may customize the application with additional features which aren't available through the standard Tembo interface.   

Tembo is licensed under the GNU GPL v3.0. Applications built out by Tembo are considered variants of a Tembo-specific template and are likewise licensed under the GNU GPL v3.0.



### 3. <a id="Vocabulary"></a>Vocabulary
This section clarifies the specific meaning of certain terms as used in this document.

**Tembo** is a WordPress plugin that lets an average user develop relational database applications for the web.

A **developer** is anybody who uses Tembo to create an application. The developer must have admin access on the development site.

The **development site** is the WordPress site on which Tembo is installed, and where development takes place.

A **Tembo application** (or simply "application") is an application that the developer creates using Tembo. All Tembo applications are deployed as WordPress plugins. They use the WordPress site's mySQL database as their back end. 

A **Tembo project** (or simply "project") is an application under development in Tembo. It holds all of the developer's specifications for a Tembo application. A "complete" project is one in which the project has been completely defined and is ready to build out. Tembo is capable of managing any number of projects concurrently. A project is not the same as an application; it can be thought of as the blueprint or representation of the application, as stored and modified using Tembo.

The **project interview** (or simply "interview") is the guided process by which a developer defines a project in Tembo - its tables, fields, forms, etc. 

**Building out** is Tembo's process of turning a completed project into an application. When the interview is finished, the developer has Tembo build out the project into an application, by generating all necessary files (in PHP, Javascript and CSS) to create the application plugin.

**Customization** is the process by which a developer revises a Tembo application manually (i.e., without using Tembo) after the application has been built out. Developers who understand the Tembo codebase are free to customize in any way they choose. Customization usually requires skill and experience in WordPress, PHP, Javascript, SQL, and/or CSS.  


An **installation** is the deployment of a Tembo application on any particular WordPress site. There is nothing to prevent an application being installed on any arbitrary number of sites. Note that Tembo itself does *not* need to be installed on the site; the application is self-contained.

The **installation site** is the WordPress site where the application is installed. It may be the same as the development site.

An **admin** is the person who installs and configures a Tembo application on an installation site. 

A **user** is the end user of a Tembo application on an installation site. (If a developer creates an application for personal use only, the developer might well be the admin and the only user for the application, as well.) 

A **data entry form**, in either Tembo or a Tembo application, is a page or a section of a page that collects data (usually multiple inputs) from the user for creating a new record or revising an existing record.

A **selection form**, in either Tembo or a Tembo application, is a page or a section of a page that presents a list of data records to choose from. In some cases the user may filter or sort the choices using controls given on the form. In a **single-record selection form**, the user is prompted to choose only one record; in a **multiple-record selection form** the user may select any number of records. 

A **tabbed form**, in either Tembo or a Tembo application, is a navigation interface that organizes related sets of information which would be impractical to present on a single web page. The different sets of information are indicated by a set of "index tabs" along the top of a display area. When the user clicks on one of the tabs, the selected information (a data entry form, a selection form, or other) is shown in the display area, much like a physical document pulled in front of related physical documents and blocking the others from view.   

A **pop-up form**, in either Tembo or a Tembo application, is a rectangular display area that pops up, when needed, to present a data entry form or a selection form. The pop-up form largely covers the rest of the screen and is not resizeable or movable. Usually the user can dismiss the form only through a "Cancel" button or a button labeled "Save" or "Continue" (or, in the case of a single-record selection form, by making a selection).

A **pop-up data entry form**, in either Tembo or a Tembo application, is a rectangular area of data entry that pops up, when needed, to collect data (usually multiple inputs) from the user. The form largely covers the rest of the screen and is not resizeable or movable. Usually the user can dismiss the form only through a "Cancel" button or a "Save changes" button.

A **pick list** is a list of options for a data field. For example, in a data field called "Today's weather" a pick list might provide options such as Sunny, Rainy, Snowy, Overcast and Other. Typically a pick list populates the choices in a drop-down box or a set of radio buttons. 

A **parent table** is a table on the one side of a one-to-many relationship.

An **ancestor table** is a table which is the parent, grandparent, etc. of another table.

**Monetization** is the use of the Web Monetization protocol described by [Coil's web specification](https://webmonetization.org/specification.html). This specification refers to a particular API used for transferring small amounts of money from website visitors to content creators. In the current document, the term does not refer to advertising revenue, paid subscriptions or any of the many other meanings of "web monetization."  


### 4. <a id="SummaryOfFeatures"></a>Summary of features 

1. Tembo can be installed on any standard WordPress site hosted on an independent host (i.e., not wordpress.com). It will be compatible with the latest stable version of WordPress at time of release. It is not intended for multi-site use. (\** **Enhancement:** Multi-site capability.)

1. We don't plan for Tembo to depend on third-party plugins or software outside the Tembo package itself. (To be revisited during the software development phase.)   

1. The Tembo interface, and the applications developed using Tembo, will use the English language. (\** **Enhancement:** Internationalization of both Tembo and its applications.) 

1. The Tembo interface, and the applications developed using Tembo, will be best viewed on a standard-size monitor. (\** **Enhancement:** Developers can choose an option to develop for mobile or responsive, and the interview and application will be developed accordingly.)

1. **Preferences:** Upon installation, Tembo will prompt the developer to enter system preferences (such as a prefix for Tembo-specific names, tables and classes, in order to avoid conflicts with other existing plugins and style sheets;  default developer's name, email address and website; etc.)


1. **Projects:** The developer can create, delete, maintain and edit any number of projects. 
   
	When the developer creates a new project, or edits a project that has already been built out, all sections of the Interview process (see below) are set to "In process." This ensures that each section in turn can be checked as needed before the developer can proceed to the next section.

	When the developer returns to edit a project that has already been built out, Tembo requests selection of "Save data already entered" (Default) or "Recreate data from scratch." If the developer chooses "Save data already entered," Tembo gives a warning to backup, as data may be lost in the rebuild process.

1. **The Interview:** Tembo will guide the developer through project development using an interview process, presented in a series of sections. The developer may return to completed sections at any time, but in general cannot jump ahead, since later sections depend on choices made in earlier sections. 

1. Sections of the interview process will be described in the detail section, below. In summary, those sections will be:
   - General set-up

   - Tables and fields

   - Pick lists

   - Assign tables to forms

   - Forms

   - Reports


1. The interview process is automated as much as possible. Tembo will apply a highly opinionated design philosophy to ensure that novice developers can build applications quickly and easily by making only necessary choices and accepting default options. 

1. The developer's choices, collected in the interview process, will be saved in Tembo. In this way projects can be maintained indefinitely and new projects created from old. 

1. **Data table relationships and relational integrity:** Tembo enforces a simple relational model among tables in the application. The developer relates Table B to Table A by defining Table A as a "parent record" (in other words, a foreign key) field in Table B. A table may have multiple parent records, which means it can serve as a join table for many-to-many relationships. Relational integrity is not enforced through the back end, although the front end includes features to protect relational integrity.

1. **Build out:** When a project interview is complete, the developer may use Tembo to build out the project into a complete application, deployed as a plugin on the current WordPress site. The developer may then configure the application and begin to use it.
 
1. The build-out process also creates a .zip file which contains the entire plugin, ready to be installed on any other (properly updated) WordPress site.

1. **Customization:** Nothing prevents developers from customizing a built-out application (that is, adding functionality, theming, etc. via software changes not made through Tembo). But Tembo will not detect such customizations, and if the developer builds out the project again, customizations may be overwritten. 

1. **Versions:** If the developer edits a project that has already been built out, Tembo will request a new version number, but will not otherwise enforce versioning or track versions. Building out a revised project will overwrite the old project. 

1. **User management:** Users of the application will be managed via WordPress's user management tools. WordPress user roles will be mapped to specific roles roles within the application, with different permissions to read, write, create and delete records. (See discussion [below](#UserRoles).)   
   


### 5. <a id="InterviewDetail"></a>Interview Process - Detail
For each project, Tembo guides the developer quickly and easily through the minimum set of decisions needed to create a relational web database. The heart of this development process is an interview-style data collection. In this section we describe the details of the interview process. 

Here is a [diagram of the interview process](https://github.com/jsenyak/tembo/blob/main/docs/TemboInterview.1.0.jpg):
![](https://raw.githubusercontent.com/jsenyak/tembo/main/docs/TemboInterview.1.0.jpg)

 

There are six sections in the interview. Each section has a status of either "In process" or "Complete." At the beginning of the interview, the status of all sections is "In process." The developer must start at the first section and complete it before moving to the second section, and so on. The developer may return to any of the completed sections at any time, but (in general) if changes are made to a section, the status of all subsequent sections of the interview is changed to "In process." This ensures that each section is checked for validity and consistency with previous sections.  

1. **General setup**

    In this section, the developer provides basic information such as the application's name; an application website; the developer's name, email address and website; preferred date format (mm/dd/yy, mm/dd/yyyy, dd/mm/yy, dd/mm/yyyy); default maximum length of pick list option text (default value: 25); application-specific prefix for tables, tags and style classes. (Changes to this section do not change the status of subsequent sections.)

1. **Tables and fields** 

    This section shows a list of any tables which have already been defined for the project. Each table is displayed in a row, showing the table's name; the number of fields defined for the table; the status of the table ("In progress" and "Complete") and "Edit" and "Remove" buttons. This section also provides a single "Create new table" button and a single "Finished defining tables" button.

	The "Edit" button takes the developer to the "Define `[TABLE NAME]` table" screen for the selected table.

	The "Remove" button requests confirmation before removing the selected table. 

    The "Create new table" button prompts the developer to enter the new table name. Suggested names are converted to a conventional form (see SQL style guide) for storage. If the converted name hasn't been used in the project yet, Tembo takes the developer to the "Define `[TABLE NAME]` table" screen. 

	The "Finished defining tables" button is grayed out if there are no tables or if any of the tables have an "In progress" status. When it is clicked it takes the developer to the next section of the interview, which is "Pick lists." 


    *  **"Define `[TABLE NAME]` table" screen**

        This screen shows 

		* The name of the table

		* A brief description of the purpose of the table (optional)  
		
		* A list of fields that have already been defined for the table. The list starts with a field called `[TABLE NAME]`_ID (an autonumbered integer), which can't be moved or removed on this screen. (This field is the primary key for the table.) For each field on the list there is a row displaying:

			* An up/down control to change the row's position in the list by drag/drop

			* The name of the field

			* The type of the field (e.g. "Text")
			
			* The type details of the field (e.g. "Width: 10")
			
			* An "edit" button. This takes the developer to the "Define `[FIELD NAME]` field" screen as a pop-up form.
			
			* A "remove" button. System requests confirmation before removing the field.
			   
		* An "Add new field" button. This button prompts the developer to enter the new field name (caption) and, if the name hasn't been used in the table yet, opens the "Define `[FIELD NAME]` field" pop-up form. 

		* A dropdown control, containing all the fields currently defined, labeled "This table is best defined by:" No duplicates will be allowed on this field. It could be the primary key, but a better choice would be a field holding values that are reasonably unique and also recognizable to the user (like the full name of a person, a product code like "CORNCHIP3", etc.) (This field is called the "easy identifier" field elsewhere in this document.)
		 
		* A field for "Maximum number of records expected in this table." This number will be helpful in later interface design. 
		
		* A "Save table" field. This saves any table-specific options entered on this screen. 

        * A "Finished defining fields" button. If there are no fields defined besides the `[TABLE NAME]`_ID field, the developer is alerted, but can confirm to continue, and Tembo takes the developer back to the "Tables and Fields" section.  
 
		
    *  **"Define `[FIELD NAME]` field" pop-up form**

        This screen shows the properties for the selected table field:

		* Caption. Up to 30 characters are allowed. (Further detail for the user can be given in the "explanatory text" for the field.)

		* Field name. Up to 30 characters are allowed. If no field name has been entered yet, the field name is generated automatically as the developer types in the caption; it is a conversion from the developer's Caption to a field name according to the SQL style sheet. (For example, an entered caption of "First Name" would be converted to a field name of "first_name".)  
		 
		* Field type. Options are:

		     * Text 

		     * Integer (number)

		     * Date

		     * Decimal (two places, i.e. 1,234.78)

		     * Long text/memo

		     * Checkbox

		     * Parent record

		     * Pick list

		     * Floating point (allows arbitrary number of decimals, i.e. 3,454.29875)
		     
		* Field type detail.
 
			* For text, specify maximum length. (Default: 40)

			* For parent record, specify the parent table from a picklist, or allow developer to enter the name of a table yet to be created. Also specify "On deleting parent record..." with options "Delete related `[TABLE NAME]` records", "Leave related `[TABLE NAME]` records alone" (Default), and "Don't allow deletion if there are related `[TABLE NAME]` records"  

			* For pick list, specifiy from list of existing pick lists, or allow developer to enter the name of a pick list yet to be created. 

		* Explanatory text. Up to 50 characters are allowed. Text can be entered here as needed for guiding users.
		
 
1. **Pick lists**

    This section shows a list of any pick lists which have already been created, whether through this section or simply by being referenced in a "pick list" field type in a table field in the previous section. Each pick list is displayed in a row, showing the pick list's name; the number of options defined for the list; and "Edit" and "Remove" buttons. This section also provides a single "Create new pick list" button and a single "Finished defining pick lists" button.

    The "Edit" button takes the developer to the "Define `[PICK LIST NAME]` pick list" screen for the selected pick list.

    The "Remove" button requests confirmation before removing the selected pick list. If the pick list has been referenced in a field of "pick list" field type, it cannot be removed; instead Tembo alerts the developer of the field(s) where the pick list is referenced. 

    The "Create new pick list" button prompts the developer to enter the new pick list name. Suggested names are converted to a conventional form (see SQL style guide) for storage. If the converted name hasn't been used in the project yet, Tembo takes the developer to the "Define `[PICK LIST NAME]` pick list" pop-up form.

    When the developer clicks the "Finished defining pick lists" button, Tembo checks to see if there are pick lists with no options. If so, the developer is alerted, but may still choose to continue. Tembo then sets the "Pick lists" section status to "Complete" and takes the developer to the next section of the interview, which is "Assign tables to forms." 

   *  **"Define `[PICK LIST NAME]` pick list" pop-up form**

        This form shows a list of options that have already been created for the selected pick list. For example, for a pick list "Pet type," the options might be "Dog", "Cat", "Goldfish" and "Other". Each option is a row on the list, and each row shows the autonumbered primary key of the option, the option text, a "Remove option" button and an "Edit option" button. 

        The form also presents a field for "Maximum length for option text" (the default for which is set in "General settings"); a single "Add an option" button; a single "Save" button; and a single "Done with this pick list" button.
      
        * The Remove option button prompts developer for confirmation (with a warning), then removes the selected option.

        * The "Edit option" button opens the "Edit option" pop-up form on top of the "Define `[PICK LIST NAME]` pick list" pop-up form. This form shows the option text and a "Save" button and a "Cancel" button. The developer may now edit the Option text. The new text is limited to the length specified in the pick list definition. An option text cannot be saved if it is blank or if it is exactly the same as the text for any other option in the pick list.

        * The "Add an option" button opens the "Edit option" pop-up form, as above, with a blank option text. If a legitimate option text is entered, it is saved as a new option for the pick list.

        * The "Save" button saves any data the developer may have changed on the form (currently, only the "Maximum length for option text").

        * The "Done with this pick list" button closes the pop-up form, revealing the Pick lists section underneath.  

   
1. **Assign tables to forms**

    For a given table, Tembo can generate three different types of forms automatically:

    * *Selection form*. This form allows the user to find and select a record for the given table, perhaps using user-specified filter and sort options. This form may be used to navigate to a particular record to review or edit it, or it may be used to select a particular record from the table (for example, to choose a parent for a child record).
    
    * *Data detail form*. This form is used to review the details of a particular record in the table, and/or to edit the data in that record.
    
    * *Subform*. This form is for child tables only. It is displayed within the Data detail form of the parent record, and it lists all the child records that are children of the parent. (For example, imagine a parent table  "Countries of the world" and a child table "Cities." When looking at the data detail form for the country Egypt, a subform on that form could list the related cities Cairo, Alexandria, Port Said, etc.) The subform is used to create new child records and to drill down to the data detail of one particular child record.
    
    The "Assign tables to forms" screen allows the developer to select the forms to create for each of the tables.

	The screen presents a subsection for each table, and within the subsection a list of possible forms, with check boxes, for that table. Each form listed has a build status: *required* (the check box is checked and cannot be unchecked), *recommended* (the check box is checked by default but can be unchecked), or *optional* (the check box is not checked by default but can be checked). Tembo's rules for assigning forms and build status to each table:

	* A selection form is required for each table that has no parent table. (Otherwise there would be no way for the user to navigate to a specific record in the table.)    

	* A data detail form is required for each table. (Otherwise there would be no way for the user to change the data of a record.)
	
	* A table that has a parent table may have a subform (for the parent table's detail form) and/or a selection form. If the  "maximum number of records expected" for the two tables indicate that there may be a very large number of subform records (more than about 50), the selection form is recommended and the subform is not recommended; otherwise the reverse.
	
    The developer reviews the checkboxes on this screen and may check or uncheck forms as needed. When done, the developer clicks the "Done with assigning forms to tables" button. Tembo checks to ensure that each table has at least one subform or a selection form (if not both). Tembo then takes the developer to the next section of the interview, which is "Forms."
  
1. **Forms**

    This section shows:

 	* A list of the forms that were selected in the "Assign forms to tables" section. Each form is a row on the list. Each row shows the form name; the table name; the status of the form ("In process" or "Complete"); and an "Edit form" button.
 	
 	* A button: "Done defining forms." (This button is grayed out if any form has a status of "In process.") Takes the developer to the next section of the interview, which is "User roles."

    The "Edit" button takes the developer to the "Define `[FORM NAME]` form" screen for the selected form. Note that this form has three different appearances, depending on the type of form selected (Data Detail, Selection or Subform)

    Note that forms are *not* created or removed in this section, but in the "Define forms for tables" section.

    *  **"Define `[FORM NAME]` form" screen - for a Data Detail form**

        The developer uses this form to define the appearance of a "Data detail" form based on the selected table. This screen shows: 

        * A "Fields" list on the left of the screen, showing all fields in the relevant table which have not yet been assigned to the form. The developer may drag fields from this list to the "Fields in this form" list. This list also includes "Vertical space," "Horizontal line" and "Text," which the developer may drag into the field list as if they were table fields. 
        
        * A section of options for the form as a whole. Options include:
        
          * Captions: "Left justified" (default), "Right justified" 
        
          * Form name.
     
        * A "Fields in this form" list in the center of the screen. On first editing the form, the list shows all the fields in the table, in the order they appear in the table. Each field is displayed on a row of the list. Each row gives:
        
           * Controls to drag and drop the field up or down in the list 
           
           * The name of the field
           
           * The field type
           
           * The field type details
           
           * A "Remove field" button     
        
        * A "Properties" pane giving the properties for the currently highlighted field. The properties shown in this pane are:
        
           * The field name (read-only).
        
           * The caption for the field for this table. Default is the caption entered in the table section, but this can be overridden.
        
           * Explanatory text for this field. Default is the Explanatory text entered in the table section, but this can be overridden.
        
           * The field type (read-only).
        
           * Field type details (read-only).
           
           * Pick list fields appear as dropdown boxes, with options in alphabetical order. 

        * The form appears in the application as a tabbed page control. All controls (other than subforms) appear on the first tab page. Each subform appears on a separate tab page. 
                 
        * A button: "Done defining this form." Validates the selections on the screen and takes the developer back to the "Forms" section.

    *  **"Define `[FORM NAME]` form" screen - for a selection form**

        The developer uses this form to define the appearance of a "Selection" form based on the selected table. This screen shows: 

        * A filters set-up area. On the left of the area is a list of fields from the selected table which have not yet been used as filter options. ("Parent table" fields are not shown unless the "Estimated maximum records" is 50 or less. Memo fields are not shown.) The developer may drag any of these these into the "Filter options" area on the right, and may drag them up and down within this area, and drag them out of the area to remove them. See Application description for explanation of use of Filter options.
        
        * A selection list set-up area. On the left of the area is a list of fields from the selected table which have not yet been used in the list. (Memo fields are not shown.) The developer may drag any of these into the "list columns" area on the right, and may drag them left and right within this area, and drag them out of the area to remove them. (Unlike most of the options of this type in Tembo, the "list columns" area is organized left-to-right, not up-and-down.) The table's ID field and "easy identifier" field are shown by default but may be removed. The developer is warned if the selected list columns are likely to exceed a reasonable width for the form.   
        
        * A button: "Done defining this form." Validates the selections on the screen and takes the developer back to the "Forms" section.

1. **Reports**

    This section shows a list of any reports which have already been defined in the project. On first accessing this section, there is a report created by default for every table in the project (so long as the table has either pick list fields or numeric fields). These reports are all "Complete" on creation.

    Each report is displayed in a row, showing the report's name; the report's status ("In process" or "Complete"); an "Edit" button and a "Remove" button. This section also provides a single "Create new report" button and a single "Finished defining reports" button.

    The "Edit" button takes the developer to the "Define `[REPORT NAME]` report" screen for the selected report.

    The "Remove" button requests confirmation before removing the selected report. 

    The "Create new report" button prompts the developer to enter the new report name. If the name hasn't been used in the project yet, Tembo takes the developer to the "Define `[REPORT NAME]` report" screen. 

    The "Finished defining reports" button is grayed out if any report has a status of "In process." Otherwise, if clicked, and if all other sections are complete (which should be the case), alerts the developer that the project is complete and can now be built out.

    *  **"Define `[REPORT NAME]` report" screen**

        The developer uses this screen to define the appearance of a Report. This screen shows: 

        * Editable field for the name of the report.

        * Editable field for a description of the report. (Up to 255 characters)

        * A drop-down box with the name of all tables in the system. The developer must choose a table to continue.

        * An area for defining "hard-coded filters" - filters that are *always* applied to the report. On the left side of the area is a list of fields (pick list only) from the selected table, and from all its parent (and grandparent, etc.) tables. The developer may drag and drop fields from this list to the "hard-coded filters" list in the center of the area. When a field is dropped, the developer then chooses an existing pick list value to complete the hard-coded filter. The developer may choose any number of fields for hard-coded filters (but, logically, no field may be used twice).

        * An area for defining "runtime filters" - filters that the *user* will specify when running the report from the finished application. On the left side of the screen is a list of fields (all field types except memo and parent record) from the table and all its parent (and other ancestor) tables. The developer may drag and drop fields from this list to the "runtime filters" list in the center of the area. In this case the developer does not choose a value for the field, since the user will choose the value(s) at runtime. 
        
        * A button: "Done defining this report." Validates the selections on the screen and takes the developer back to the "Reports" section.


### 6. <a id="ApplicationDescription"></a>Description of a Tembo Application
1. **Scale:** A typical Tembo application may have in the order of hundreds of users, perhaps half a dozen data tables (although technically Tembo will allow many more(, and tens of thousands of data records.

1. **Accessibility:** Users of the application are not expected to have previous familiarity with WordPress or Tembo. The application should be almost as immediately intuitive as (say) an online shopping site or airline reservation system.   

1. <a id="UserRoles"></a>**User roles:** User roles in the application are not quite the same as user roles in WordPress. 
   - User roles in the application are:

      - **Admin**: can set preferences and options; can edit pick list options; has all privileges of Record owners. (WordPress Administrators or Superadmins are assigned to this role and can't be removed from it.)

      - **Record owners**: can view, edit, create and delete records. (By default, WordPress Editors are assigned to this role.)
 
      - **Record creators**: can view, edit and create records, but cannot delete. (By default, WordPress Authors are assigned to this role.)
 
      - **Record updaters**: can view and edit all records, but cannot create or delete. (By default, WordPress Contributors are assigned to this role.)

	   - **Readers**: can view all records, but cannot change data. (By default, WordPress Subscribers are assigned to this role.)
 
   - The application admin may map WordPress roles to application roles in other than these default configurations. Visitors (users who have not signed in to the site) *may* be assigned to the "Readers" role, but may not be assigned to other privileges.

1. **Navigation:** The user navigates the application primarily through buttons presented on on-screen forms. There is a top menubar that allows navigation to key parts of the application.

1. **Menubar:**  The application comes with a standard menu bar with the following menu items:

   * Login/Logout (via WordPress)
   
   * A menu item for each of the Selection forms
   
   * Reports (navigates to the reports menu)
   
   * Admin (visible only to admin-level users; navigates to the admin menu)

1. **Forms:** Besides the controls defined in the "Forms" section, every form comes with certain features by default:

   * *Selection forms:*  
      * If the developer has defined "Header filters," those filters appear at the head of the selection form, so that the user may filter the records in the underlying table.
      
         * If the filter is for a field of numeric or date type, it appears here with the option to select >, < or =, and the user may enter a value.
         
         * If the filter is for a field of pick list or parent table type, it appears here as a pick list.
         
         * If the filter is for a field of text type, a text field appears here. The user may use wildcard characters "%" and "?" for matching.
         
         * Includes "Apply filters" button to apply the filter(s) that have been entered. 
      
      * Every column header can be clicked to sort the data results ascending (and then, if clicked again, descending). An up/down arrow icon shows the direction of the sort.
      
      * Includes "Cancel" button, in case no selection can be made. 
      
   * *Data detail forms:*  

      * Text fields are justified left; numeric and date fields are justified right. Date fields include a date-picking widget.
      
      * The data detail form always shows the record in editable form if the user's permission allows editing of the record; otherwise the data is shown in read-only format.  
       
      * If the ID (primary key) field for the table is shown, it is always shown read-only.  
      
      * Includes "Save record" button (if user permissions allow) 
      
      * Includes "Delete this record" button (if user permissions allow)
      
      * Includes "Go to related [parent]" button for every parent table.
      

   * *Subforms:*
   
      * Clicking on any item takes user to the data detail form for the selected record.
      
      * Includes "Create new `[TABLE NAME]` record" button (if user permissions allow)    

1. **Admin functions:** Every application comes with an "Admin functions" menu item allowing the admin access to features including:

   - Maintaining pick lists
   
   - Installation-specific preferences, such as identifier for the admin's Web Monetization wallet (if the owner of the installation wishes to monetize the installation)
   
   - Mapping WordPress user roles to application user roles, as described above 
   
	- Backing up and downloading the application data tables in a single mysqldump file.


1. **Reports:** All reports are listed, with descriptions, on a reports menu. When the user runs a report, the "runtime filters" are offered for user's input. User  also must choose between "summary report" (default) and "download detailed data." 
   
   - The "summary" version is provided with a header giving report name and describing all filters (both hard-coded and user-defined). The report gives:
   
      - The count of records in the filtered group 
      
      - Frequencies (both numeric count and percentage) for all pick list fields
      
      - Sum and average of all numeric fields and count of non-blank values.

   - The "download" version is provided with a header giving report name and describing all filters (both hard-coded and user-defined). The "easy identifier" for each ancestor field is given, along with all fields in the selected table. Pick list fields in the selected table are shown as both code values and text values. The data is uploaded to user as a .csv file.
 	
1. **Theming:** Every application will come with a very bare-bones "generic theme." On initializing the application, the admin can choose to use either the application site's selected theme or the generic theme. (A proficient admin may customize the "generic" theme as desired.) 

1. **Protecting updates in a multi-user environment:** User-initiated record updates use optimistic concurrency. If User A and User B both select the same record for editing, and user B updates before user A, application will alert user A that their changes have not been saved.

### 7. <a id="FeaturesForFuture"></a>Features for future versions

Here, in no particular order, are features which may be desirable for future versions of Tembo.

1. Allow a splash screen and/or launch screen for the application

1. **User roles**: Developer defines distinct roles for the application (e.g. "Customer", "Sales associate", "IT Admin", "Manager"); defines general system-wide default privileges for each of these roles for read, write, create, and delete; may define overriding privileges for specific tables and reports; sets default mapping of WordPress roles to application roles. However, the application admin is given tools to redefine these roles, permissions and mappings as desired. (Ideally even custom user roles on the installation site could be used in mapping to application roles.) - Possibly also allow admin to map application user roles to specific WordPress users, rather than to WordPress roles? 

1. When building the application, Tembo creates documentation describing the particular tables and PHP scripts that correspond to the "friendly names" of forms and reports in the application. 

1. When defining runtime filters for reports, developer chooses between "User MUST enter criteria" and "User may leave criteria blank for broader scope" (default)

1. A context-sensitive help system for Tembo

1. A context-sensitive help system for the application, with text provided by the developer

1. Tembo allows the developer to enter their level of proficiency; the interview gives different levels of support and explanation depending on developer's proficiency

1. Tembo allows users to add code snippets on events such as "record save" or "form open" or "field update," for greater development functionality. Certain constants (e.g. the user ID of the current user) must be available for this code.

1. Tembo offers hooks, filters and/or templates, similar to WordPress itself, so that properly implemented customizations aren't lost if the application is updated.

1. Tracking of project versions for the developer. Possibly project versions can be saved, exported to and restored from text files. Such files would probably be saved along with the application plugin code.)

1. Management of versions (even automatic updates?) of the application for the application admin; ability to upgrade the application without overwriting data (where backwards compatible)  

1. The "Tables" section of the interview allows view of a simplifed entity relationship diagram, displaying all the relationships implied by developer's definition of "Parent record" fields. The developer should be able to rearrange the diagram by dragging and dropping tables, and Tembo should allow storage of the new arrangement.

1. In table design:

	1. Allow developer to add/delete index on field
		
	1. Allow developer to add/delete constraint on field
		
1. In field definition:

	1. Allow option for "Check for duplicate on data entry/edit," with options "Don't check" (default), "Allow with warning", "Never allow")

	1. Allow option for "Require a value on data entry/edit," with options "Don't check" (default), "Allow blank with warning", "Never allow blank"

1. In pick list option definition:
	1. Include an optional "Order" field (type: numeric), to allow custom order. (Pick list items will always be sorted first by Order, then alphabetically, allowing many useful presentation styles for the application admin.) 

	1. With "order" included, allow developer choice to number the order field manually OR to order all by drag and drop. 

	1. Include a checkbox for "Inactive." (When an option is flagged as inactive, it is sorted to the bottom of a drop down control and "(Inactive) " is prepended to the option text.)

1. In "Assign forms to tables": 

	1. the developer will have the option to duplicate and rename forms shown in this section (and, in the Forms section, edit their design for useful purposes). For example, an electrician might want two different "data detail forms" for a Client table - a short form, filled out when receiving a phone call from a new client, and a long form, filled out after the first job for that client is complete.) 

	1. In "Assign forms to tables," the developer will have options for other useful standard form types (besides the three already given), such as "Merge duplicate records," "Assign selected records to a second parent," etc. 


1. In form design:

	1. Fields that can be added include a "checkbox group" which is a container for a set of checkboxes related to a single question - e.g. "Check all that apply".)

	1. Option to number  or not number (default) the controls on the form.  
          
	1. Option for placement of subforms: "Separate tab" (Default), "Underneath fields"
          
	1. Options for other standard command buttons, e.g. "Go to [grandparent table]" or "Duplicate this record" (with developer-defined options of which fields to duplicate).

	1. Developer can add/remove form tab pages and can move controls (including subforms) to different tab pages.   

	1. Developer can choose between "drop down box" (default) and "radio buttons" for user editing of a pick list field on Data Detail form
        
	1. In overall design for selection forms, developer may define a SQL-style filter, so that only selected records are shown.)

1. In form field definition:

	1. Developer can define validation values - e.g. an entered date must be after a certain specified date.
           
	1. Developer can limit permissions for individual fields.)

	1. Additional field types supported. Most would actually be formatted text strings - e.g. SSN, ZIP+4, telephone number, email, etc. Also allow time; date and time; fixed point decimals which are not only two decimal places.

	1. Allow field type "Calculated field," probably using SQL syntax. 

1. In report design: allow application admin to create custom reports using PHP and add these PHP scripts to the reports menu. These custom reports should not be overwritten by default during an upgrade.

1. When an application report is opened and a runtime date filter is offered: 
	
	1. include option for "between".
	
	1. Values include option for "last month", "last year", "YTD", etc.

1. Add an admin function to download the data tables as zipped .csv files.   
	
1. Add an admin function to run SELECT SQL queries against the application tables?

1. Allow developers to build and include custom themes for the application.


  
### 8. <a id="QuestionsOutstanding"></a>Questions outstanding
1. Is it possible to configure monetization to reward two recipients simultaneously? Specifically, could an application be configured to pay the developer's wallet as well as (to a lesser degree) the wallet of the Tembo development project?

1. To remove a component from a drag-and-drop area - is it better to use a drag-out or to use a "remove" button? Is it important to be consistent with this behavior or does it depend on context?

1. Will there be a "Save" button on all/most interview sections and forms to save entered options, or should it be automatically updated?   
