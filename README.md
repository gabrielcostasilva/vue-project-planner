# Project Planner
This project is based on one of the three projects developed by [The Net Ninja (Shaun Pelling)](https://www.youtube.com/channel/UCW5YeuERMmlnqo4oq8vwUpg) on his excelent [Udemy course](https://www.udemy.com/course/build-web-apps-with-vuejs-firebase).

## Project Overview

### Home Screen
<img src="./pics/Home.png"  />
The home screen shows existent projects as a list of items. Whereas completed projects are marked in green, ongoing projects are marked in pink. The menu on the top of the screen shows available options. The current option is underlined in green. Between the top menu and the project list is the filter. The current filter shows all projects, but one can choose to see only the completed or ongoing projects.

### Project Item
<img src="./pics/ProjectItem.png"  />
Each single project item can be expanded to show the details by clicking on the project title. A project can be edited, deleted or marked as completed by using the icons on the right-hand side.

### Editing Project
<img src="./pics/EditProject.png"  />
By clicking on the pencil icon on the right-hand side of the project title, the _EditProject_ view is loaded with the current project data. When the button _Update_ _Project_ is clicked, the project data is updated.

### Deleting Project
The trash icon deletes the targeted project. The icon is located on the right-hand side of the project title. There is no confirmation before deleting.

### Changing Project Completion Status
<img src="./pics/CompletionStatus.png"  />
A project may be set as completed or ongoing. The left-hand border colour identifies the project completion status. The check icon is also coloured differently to identify the completion status. In addition, the check icon changes the project completion status.

### Adding a New Project
<img src="./pics/AddProject.png"  />
The main menu enables adding a new project by clicking on the corresponding option. It loads the _AddProject_ view. Both fields are required although there is no other check. The _Add_ _Project_ button stores the data in the local database.

## Views & Components Overview

<img src="./pics/ComponentTree.png"  />

Using Vue 3, the project consists of a root (App.vue, as always) and three child views: Home, AddProject and EditProject (.vue). The root view also has a navbar (Navbar.vue) whereas the Home view has two child components: FilterNav and SingleProject (.vue).

## Views & Components Details

### Views
* _Home_ is the main agregating page (after the App.vue, of course). It groups the filter component (_FilterNav_), which is located between the main menu and the project list in the main screen. It also groups the project list. Each project item is an instance of _SingleProject_. Both _FilterNav_ and _SingleProject_ receives parameters via _props_, and emit events to/from _Home_.  

* _AddProject_ has the form for project data input. Once the data is populated and the button clicked, the _view_ submits a REST/POST request to insert the new data into the local database. The route to this is view is managed by the Vue Router, according to configuration set on the _Navbar.vue_ and _router/index.js_.

* _EditProject_ has the same form used in the _AddProject_ view (which could have been a separated component for increasing reuse). Different from the _AddProject_, this view needs to populate the current data into the  form before enabling any editing. This is done by retrieving data from the database via a GET request. The updated data is sent to the local database via a PATCH request. After editing, the Vue Router redirects to the main page as long as everything works fine.

### Components
* _NavBar_

* _SingleProject_

* _FilterNav_

## File Structure

<img src="./pics/FileStructure.png"  />

## Dependencies

## Data

## Running the Project Locally
