
# Anypoint Template: MS Dynamics CRM to Salesforce Contact Migration

+ [License Agreement](#licenseagreement)
+ [Use Case](#usecase)
+ [Considerations](#considerations)
	* [Salesforce Considerations](#salesforceconsiderations)
	* [Microsoft Dynamics CRM Considerations](#msdynamicsconsiderations)
+ [Run it!](#runit)
	* [Running on premise](#runonopremise)
	* [Running on Studio](#runonstudio)
	* [Running on Mule ESB stand alone](#runonmuleesbstandalone)
	* [Running on CloudHub](#runoncloudhub)
	* [Deploying your Anypoint Template on CloudHub](#deployingyouranypointtemplateoncloudhub)
	* [Properties to be configured (With examples)](#propertiestobeconfigured)
+ [API Calls](#apicalls)
+ [Customize It!](#customizeit)
	* [config.xml](#configxml)
	* [businessLogic.xml](#businesslogicxml)
	* [endpoints.xml](#endpointsxml)
	* [errorHandling.xml](#errorhandlingxml)


# License Agreement <a name="licenseagreement"/>
Note that using this template is subject to the conditions of this [License Agreement](AnypointTemplateLicense.pdf).
Please review the terms of the license before downloading and using this template. In short, you are allowed to use the template for free with Mule ESB Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case <a name="usecase"/>
As a Salesforce admin I want to synchronize Contacts between MS Dynamics CRM and Salesforce in a one-time manner.

This Template should serve as a foundation for setting an online migration of Contacts from MS Dynamics CRM to a Salesforce instance. Everytime the HTTP endpoint is triggered, the integration will migrate all contacts from the MS Dynamics CRM instance in manner of one time integration and it will be responsible for updating or inserting the Contacts on the target Salesforce instance.

Requirements have been set not only to be used as examples, but also to establish a starting point to adapt your integration to your requirements.

As implemented, this Template leverages the [Batch Module](http://www.mulesoft.org/documentation/display/current/Batch+Processing).
The batch job is divided in Input, Process and On Complete stages.

The integration is triggered by a HTTP endpoint defined in the flow that is going to trigger the application, querying the MS Dynamics contacts matching a filter criteria and executing the batch job.
During the Process stage, each MS Dynamics Contact will be filtered depending on if it has an existing matching Contact in the Salesforce instance.
The last step of the Process stage will group the Contacts and insert/update them in Salesforce.
Finally during the On Complete stage, the Template will log output statistics data into the console and send an email with the results.

# Considerations <a name="considerations"/>

To make this Anypoint Template run, there are certain preconditions that must be considered. All of them deal with the preparations in both source (MS Dynamics) and destination (Salesforce) systems, that must be made in order for all to run smoothly. 
**Failing to do so could lead to unexpected behavior of the template.**

This particular Anypoint Template illustrate the migration use case between MS Dynamics and Salesforce, thus it requires both instances to work.



## Salesforce Considerations <a name="salesforceconsiderations"/>

There may be a few things that you need to know regarding Salesforce, in order for this template to work.

In order to have this template working as expected, you should be aware of your own Salesforce field configuration.

###FAQ

 - Where can I check that the field configuration for my Salesforce instance is the right one?

    [Salesforce: Checking Field Accessibility for a Particular Field][1]

- Can I modify the Field Access Settings? How?

    [Salesforce: Modifying Field Access Settings][2]


[1]: https://help.salesforce.com/HTViewHelpDoc?id=checking_field_accessibility_for_a_particular_field.htm&language=en_US
[2]: https://help.salesforce.com/HTViewHelpDoc?id=modifying_field_access_settings.htm&language=en_US


### As destination of data

There are no particular considerations for this Anypoint Template regarding Salesforce as data destination.





## Microsoft Dynamics CRM Considerations <a name="msdynamicsconsiderations"/>

### As source of data

You need to install Java Cryptography Extensions to be able to connect to MS Dynamics. Please [choose](http://www.oracle.com/technetwork/java/javase/downloads/index.html) a relevant version according to your Java installation.



# Run it! <a name="runit"/>
Simple steps to get MS Dynamics CRM to Salesforce Contact Migration running.
See below.

## Running on premise <a name="runonopremise"/>
In this section we detail the way you should run your Anypoint Template on your computer.


### Where to Download Mule Studio and Mule ESB
First thing to know if you are a newcomer to Mule is where to get the tools.

+ You can download Mule Studio from this [Location](http://www.mulesoft.com/platform/mule-studio)
+ You can download Mule ESB from this [Location](http://www.mulesoft.com/platform/soa/mule-esb-open-source-esb)


### Importing an Anypoint Template into Studio
Mule Studio offers several ways to import a project into the workspace, for instance: 

+ Anypoint Studio generated Deployable Archive (.zip)
+ Anypoint Studio Project from External Location
+ Maven-based Mule Project from pom.xml
+ Mule ESB Configuration XML from External Location

You can find a detailed description on how to do so in this [Documentation Page](http://www.mulesoft.org/documentation/display/current/Importing+and+Exporting+in+Studio).


### Running on Studio <a name="runonstudio"/>
Once you have imported you Anypoint Template into Anypoint Studio you need to follow these steps to run it:

+ Locate the properties file `mule.dev.properties`, in src/main/resources
+ Complete all the properties required as per the examples in the section [Properties to be configured](#propertiestobeconfigured)
+ Once that is done, right click on you Anypoint Template project folder 
+ Hover you mouse over `"Run as"`
+ Click on  `"Mule Application"`
Once you have imported your Anypoint Template into Anypoint Studio you need to follow these steps to run it:

+ Locate the properties file `mule.dev.properties`, in src/main/resources
+ Complete all the properties required as per the examples in the section [Properties to be configured](#propertiestobeconfigured)
+ Once that is done, right click on you Anypoint Template project folder 
+ Hover you mouse over `"Run as"`
+ Click on  `"Mule Application"`

### Running on Mule ESB stand alone <a name="runonmuleesbstandalone"/>
Complete all properties in one of the property files, for example in [mule.prod.properties] (../master/src/main/resources/mule.prod.properties) and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`. 


## Running on CloudHub <a name="runoncloudhub"/>
While [creating your application on CloudHub](http://www.mulesoft.org/documentation/display/current/Hello+World+on+CloudHub) (Or you can do it later as a next step), you need to go to Deployment > Advanced to set all environment variables detailed in **Properties to be configured** as well as the **mule.env**.
While [creating your application on CloudHub](http://www.mulesoft.org/documentation/display/current/Hello+World+on+CloudHub) (Or you can do it later as a next step), you need to go to Deployment > Advanced to set all environment variables detailed in **Properties to be configured** as well as the **mule.env**. 
Follow other steps defined [here](#runonpremise) and once your app is all set and started, there is no need to do anything else. Every time a Contact is created or modified, it will be automatically synchronised to supplied database table.

### Deploying your Anypoint Template on CloudHub <a name="deployingyouranypointtemplateoncloudhub"/>
Mule Studio provides you with really easy way to deploy your Template directly to CloudHub, for the specific steps to do so please check this [link](http://www.mulesoft.org/documentation/display/current/Deploying+Mule+Applications#DeployingMuleApplications-DeploytoCloudHub)


## Properties to be configured (With examples) <a name="propertiestobeconfigured"/>
In order to use this Mule Anypoint Template you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. Detail list with examples:
### Application configuration
**Salesforce Connector configuration**

+ sfdc.username `joan.baez@orgb`
+ sfdc.password `JoanBaez456`
+ sfdc.securityToken `ces56arl7apQs56XTddf34X`
+ sfdc.url `https://login.salesforce.com/services/Soap/u/32.0`

**MS Dynamics Connector configuration**

+ crm.auth-type `CRMONLINE`
+ crm.username `username@company_name.onmicrosoft.com`
+ crm.password `password`
+ crm.service-url `https://company_name.api.crm4.dynamics.com/XRMServices/2011/Organization.svc`

**SMTP Services configuration**

+ smtp.host `smtp.gmail.com`
+ smtp.port `587`
+ smtp.user `johndoe%40gmail.com`
+ smtp.password `password`

**E-mail Details**

+ mail.from `batch.migratecontacts.migration%40mulesoft.com`
+ mail.to `user@example.com`
+ mail.subject `Batch Job Finished Report`

**Syncing policy for accounts**

+ account.sync.policy=syncAccount

**Note:** the property **account.sync.policy** can take any of the two following values:

+ **doNotCreateAccount**: The application will migrate the contacts over without assigning any account to them.
+ **syncAccount**: The application will migrate the contacts over and try to assign them their respective account in Salesforce, matching accounts by name. If no account is found for a specific contact, the application will create an account in Salesforce with the same name and assign it to the contact.

# API Calls <a name="apicalls"/>
Salesforce imposes limits on the number of API Calls that can be made. Therefore calculating this amount may be an important factor to consider. Contact Migration Template calls to the API can be calculated using the formula:

***1 + X + X / 100*** 

Being ***X*** the number of Contacts to be synchronized on each run. 

The division by ***100*** is because, by default, Contacts are gathered in groups of 100 for each Upsert API Call in the commit step.	

For instance if 10 records are fetched from origin instance, then 12 api calls will be made (1 + 10 + 1).

**Note:** if the property **account.sync.policy** is set as "syncAccount", the number of API calls will be increased because of the needed query for the specific account, before upserting the contact in the destination system.


# Customize It!<a name="customizeit"/>
This brief guide intends to give a high level idea of how this Anypoint Template is built and how you can change it according to your needs.
As mule applications are based on XML files, this page will be organized by describing all the XML that conform the Anypoint Template.
Of course more files will be found such as Test Classes and [Mule Application Files](http://www.mulesoft.org/documentation/display/current/Application+Format), but to keep it simple we will focus on the XMLs.

Here is a list of the main XML files you'll find in this application:

* [config.xml](#configxml)
* [endpoints.xml](#endpointsxml)
* [businessLogic.xml](#businesslogicxml)
* [errorHandling.xml](#errorhandlingxml)


## config.xml<a name="configxml"/>
Configuration for Connectors and [Properties Place Holders](http://www.mulesoft.org/documentation/display/current/Configuring+Properties) are set in this file. **Even you can change the configuration here, all parameters that can be modified here are in properties file, and this is the recommended place to do it so.** Of course if you want to do core changes to the logic you will probably need to modify this file.

In the visual editor they can be found on the *Global Element* tab.


## businessLogic.xml<a name="businesslogicxml"/>
Functional aspect of the Template is implemented on this XML, directed by one flow that will check for Salesforce creations/updates. The several message processors constitute three high level actions that fully implement the logic of this Template:

1. During the Input stage the Template will go to the MS Dynamics and query all existing Contacts that match the filter criteria.
2. During the Process stage, each MS Dynamics Contact will be matched by name against Salesforce, in order to decide whether to create or update the contact.
3. The following Batch step will match the Accounts for each contact in the destination system if the syncAccount policy is set. The final batch step will upsert the contacts in Salesforce by gathering them in batches.

Finally during the On Complete stage the Template will log output statistics data into the console.



## endpoints.xml<a name="endpointsxml"/>
This file is conformed by a Flow containing the HTTP endpoint that triggers the migration by executing the batch job process, and a Mule component that returns the batch job response to the endpoint.



## errorHandling.xml<a name="errorhandlingxml"/>
This is the right place to handle how your integration will react depending on the different exceptions. 
This file holds a [Choice Exception Strategy](http://www.mulesoft.org/documentation/display/current/Choice+Exception+Strategy) that is referenced by the main flow in the business logic.



