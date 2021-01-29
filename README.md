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

By clicking on the pencil icon on the right-hand side of the project title, the `EditProject` view is loaded with the current project data. When the button `Update Project` is clicked, the project data is updated.

### Deleting Project

The trash icon deletes the targeted project. The icon is located on the right-hand side of the project title. There is no confirmation before deleting.

### Changing Project Completion Status
<img src="./pics/CompletionStatus.png"  />

A project may be set as completed or ongoing. The left-hand border colour identifies the project completion status. The check icon is also coloured differently to identify the completion status. In addition, the check icon changes the project completion status.

### Adding a New Project
<img src="./pics/AddProject.png"  />

The main menu enables adding a new project by clicking on the corresponding option. It loads the `AddProject` view. Both fields are required although there is no other check. The `Add Project` button stores the data in the local database.

## Views & Components Overview

<img src="./pics/ComponentTree.png"  />

Using Vue 3, the project consists of a root (`App.vue`, as always) and three child views: `Home`, `AddProject` and `EditProject` (`.vue`). The root view also has a navbar (`Navbar.vue`) whereas the Home view has two child components: `FilterNav` and `SingleProject` (`.vue`).

## Views & Components Details

### Views
* `Home` is the main agregating page (after the App.vue, of course). It groups the filter component (`FilterNav`), which is located between the main menu and the project list in the main screen. It also groups the project list. Each project item is an instance of `SingleProject`. Both `FilterNav` and `SingleProject` receives parameters via `props`, and emit events to/from `Home`.  

* `AddProject` has the form for project data input. Once the data is populated and the button clicked, the `view` submits a `POST` request to insert the new data into the local database. The route to this is view is managed by the _Vue Router_, according to configuration set on the `Navbar.vue` and `router/index.js`.

* `EditProject` has the same form used in the `AddProject` view (which could have been a separated component for increasing reuse). Different from the `AddProject`, this view needs to populate the current data into the  form before enabling any editing. This is done by retrieving data from the database via a `GET` request. The updated data is sent to the local database via a `PATCH` request. After editing, the _Vue Router_ redirects to the main page as long as everything works fine.

### Components

* `NavBar` represents the main menu on the top of the screen. It just sets links that are processed by the _Vue Router_, according to the configuration on the `router/index.js`.

* `SingleProject` represents a project item. It consists of title and description. The description is hidden by default, but can be shown by clicking on the project title. This component receives project data as a `props`. It also emit two events to update the local data after changing the database. It also uses the _Vue Router_ to send the user to the `EditProject` view.

* `FilterNav` is responsible for filtering the project list. It is a very simple component that just show the filtering options and emit an event according to the user selection. The `Home` view is responsible for updating the project list by using a _computed property_.

## File Structure

<img src="./pics/FileStructure.png"  />

## Dependencies

## Data

## Running the Project Locally
