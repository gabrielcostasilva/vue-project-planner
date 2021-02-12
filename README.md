# Project Planner - Composition API
This project is based on one of the three projects developed by [The Net Ninja (Shaun Pelling)](https://www.youtube.com/channel/UCW5YeuERMmlnqo4oq8vwUpg) on his excelent [Udemy course](https://www.udemy.com/course/build-web-apps-with-vuejs-firebase).

Different from the project in the master branch, this project was modified to use the newly introduced composition API. All funcionalities, components, Views, and methods are the same, apart from one new method that needed to be introduced. Please, check the commits in this branch to see the differences in detail.

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

The directory tree was automatically built by the _Vue CLI_. The `data` folder has added to host the database file. In the Figure above, the files marked with a dark gray flag means that we created the file in for the project, whereas those marked with a green pencil means that we updated the existent file for the purpose of the project.

We updated the `public/index.html` file to link material icons we used in the project. We updated `router/index.js` to set the appropriate route configuration for _Vue Router_. We updated the `Home` file to represent the main page of the project, including both structure and formatting. The `App` file aggregates the `Navbar` and the router view. 

## Dependencies

The project has two main dependencies. First, the _View Router_ that is automatically added during the project creation using the _Vue CLI_. Second, the _json-server_ is used to simulate a local endpoint for the database. The database is just a file in the file structure as can be seen in the file structure descripption.

## Data

```json
{
  "projects": [
    {
      "id": 1,
      "title": "Create new homepage banner",
      "details": "Lorem ipsum",
      "complete": true
    }
  ]
}
```

The _json-server_ uses a single JSON file to represent the data in the database. As one can see, there are four attributes. The `id` is automatically created by the _json-server_ when inserting new data. During the project execution, the file is updated as operations (add, update, delete) are performed.

## Running the Project Locally

To run the project, ensure that you have NPM installed. You also need the _json-server_ installed globally before starting.

1. Clone the project locally

```
git clone https://github.com/gabrielcostasilva/project-planner.git
```

2. In the project folder, start the _json-server_

```
json-server --watch data/db.json
```

3. Open another terminal. In the project folder, start the project.

```
npm run serve
```

4. Access the app with your browser at `http://localhost:8080`