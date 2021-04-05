# Zoho CRM Widget JavaScript Assessment

Welcome! Here we will guide you to setup a Zoho CRM widget to enable you to design your very own *awe-inspiring* Zoho CRM widget. Widgets are essentially a small `<iframe>` containing a simple web app within Zoho CRM. End-users access widgets by clicking a button on single records or a list of records. Your job will be to develop and deploy your widget to Zoho CRM.

You'll need some background in the following areas to follow along:
- JavaScript (with Promises)
- HTML & CSS
- NPM and Node.js installed on local machine
- Zoho CRM Modules & Fields


## Project Overview
Alrighty, let's go over what exactly you're going to build. Adding Notes to records in CRMs is a very common task. Currently when you create a new Note on a record, it doesn't appear on associated modules. For example, let's say we work for the leading bobblehead manufacturer in the world and we have a new Account, the Dallas Mavericks. Since they're a needy client, we're going to be making tons of Notes to make sure we get everything right. Of course, we don't just want those Notes on the Maverick's Account record, but we want those notes to be seen on Mark Cuban and Luka Doncic's Contact records, which are associated to the Mavericks's Account.

Your job is to create a Zoho CRM Widget on an Account record that allows you to input text for a Note and select which related Contacts and Orders should get the Note as well. You must then create the Notes for the Account and the selected Contacts and Orders.

You are welcome to use any JS framework or library that you'd like to build your application. You have complete liberty to make UI and program structure decisions. At the end of this guide, we will highlight what will make your app stand out.

## Widget Development Setup
Here we will walk through step-by-step how to setup, build, and deploy a Zoho CRM Widget. Once you have this down, it's up to build the damn thing!

### Install the Zoho CLI
The Zoho CLI, or Zet, is required to build Zoho CRM Widgets. It will help you initialize projects, run a local webserver, and package your code for deployment. Make sure you have Node and npm installed on your machine, then run the following command in your terminal:
```
$ npm install -g zoho-extension-toolkit
```

Once installed, run the following commmand to ensure it installed correctly:
```
$ zet
```
You should have seen some basic help information about the Zet tool. If not, make sure your npm and path is setup correctly.

### Initialize the Project
Now that Zet is installed, we will be using it to initialize the project for our widget. When we initialize a project using Zet, it creates required the file structure and manages core dependencies. This is similar to the `npm init` command, but will pull in all the necessary dependencies that Zoho requires.

To initialize a new Widget, run the following command:
```
$ zet init
```

You will now be sent through a simple CLI for your project requirements. When prompted for a Zoho Service, select Zoho CRM, then name your project.

Let's take look into what the Zoho CLI has done for us. Navigate into your project and you should see a number of files and directories. We will be spending our time in the `app` directory.

You will be adding all your code within the `app` directory. Within it, there is a an html file called `widget.html` and a translations directory, which you can completely ignore. We can later specify which html page will be the entry point of the application, so you can add your code to whatever file you'd like.

### Building Your Widget
Let's quickly walk through running a local Zet server and viewing your web app within Zoho CRM.

To start a Zet local server, execute the following in your terminal:
```
$ zet run
```

You can now view your app online. Go to https://127.0.0.1:5000 in a browser. You'll likely have to bypass the browser's security complaint. If you are using Google Chrome, type anywhere "thisisunsafe" and you will be able to proceed.

Click into the `widget.html` and you should now see a screen that says "This is a sample Widget built using Zoho Extension toolkit."

You now need to be able to view your app within Zoho CRM. Let's start by creating the Widget:
1. Click **Setup**
2. Under *Developer Space*, select **Widgets**.
3. Click **New**
  - *Name*: YOUR PROJECT NAME
  - *Widget Type*: Button
  - *Hosting*: External
  - *Base URL*: https://127.0.0.1:5000/app/widget.html 
    - If you are using another entrypoint to your app, reference it here.
4. Click **Save**

Now that you've created the Widget, let's move onto creating the Button which will open the Widget.
1. Click **Setup**
2. Under *Customization*, select **Modules & Fields**
3. Go to **Accounts**, then navigate to the **Links and Buttons** tab.
4. Click **New Button** and name your button.
5. Under *Where would you like to place the button?* select, **View Page**.
6. Under *What action would you like the button to perform?*, select **Open a Widget**.
7. Find your widget, and click **Install**.

You should now be able to see the button and widget on an Account record. Navigate to an Account record and open the widget and make sure you're viewing the widget homepage.

### Deploying Your Widget
When deploying the widget, we will obviously not be referencing a local webserver. We will package our project via Zet, then upload the zip into Zoho CRM.

Let's package the Widget with Zet:
```
$ zet pack
```

You now need to create a new button and widget, like in the previous steps. With deployment we will now host the code externally. Now within your project directory, navigate to the `dist` directory and find the YOUR_PROJECT_NAME.zip. Here is what you need to do the for the widget:
1. Click **Setup**
2. Under *Developer Space*, select **Widgets**.
3. Click **New**
  - *Name*: YOUR PROJECT NAME
  - *Widget Type*: Button
  - *Hosting*: Zoho
  - *Index Page*: /widget.html (do not include the /app)
    - If you are using another entrypoint to your app, reference it here.
4. Click **Save**

Now, you will be able to access your project within Zoho CRM without having to run a local webserver.


## Getting Started
You will need some more information to get started. To access the Zoho CRM API from your widget, you will need to use the Zoho CRM JS SDK (so many acronyms, sheesh). The SDK will handle all API authorization for you. 

Here is the Zoho CRM JS SDK reference: https://help.zwidgets.com/help/latest/index.html

You can pull the SDK into your project with:
```html
<!-- Zoho Embedded App Framework -->
<script src="https://live.zwidgets.com/js-sdk/1.0.5/ZohoEmbededAppSDK.min.js"></script>
```

You will need to have the following code executed on page load to use the Zoho CRM JavaScript SDK:
```javascript
ZOHO.embeddedApp.on("PageLoad",function(entity)
{
	console.log(entity); // Entity is the current record
})

// Initialize the Zoho App
ZOHO.embeddedApp.init();
```

Now you can use the Zoho CRM API in the following way:
```javascript
ZOHO.CRM.API.getRecord({Entity:"Leads",RecordID:"1000000030132"})
.then(function(data){
	console.log(data)
})
```

## How We Will Evaluate Your App
We really want to see you shine. Show off your skills! We assume you can be understand the business use-case well enought that your web-dev creativity can shine.

Here are some specific things we are looking for:
- Intuitive to use
- Looks good within Zoho CRM
- Works as expected
- Adding additional details or functionality. Be creative!
