---
layout: post
title:      "React/Redux FINAL Project!! "
date:       2021-04-05 03:19:28 +0000
permalink:  react_redux_final_project
---


**Planning** 

Approaching this final project of the Flatiron curriculum I had a heightened sense of confidence that I had not yet possessed when embarking upon the previous portfolio projects. I finally felt like I had shed the imposter syndrome that had plagued me throughout a majority of the course. Although I have no doubt there is much more to learn on my software engineering journey (this being one of the numerous reasons I chose to pursue the field), the confidence felt like a rewarding culmination of my many hours of studying, stressing, and practice. Phewf! 

As I began the planning process for my project I ran through a number of potential ideas. I knew, like the rest of my projects, that I wanted the theme to be something I was passionate about- as this would make the build more enjoyable. I narrowed my list down and decided to pursue one of my first ideas- an endangered species tracker. The idea being that a user could signup or login to access the web app’s core functionality- fetching data from the Environmental Conservation Online System’s (ECOS) API of global endangered species. 


**App Functionality **

Once logged-in, users are able to search for endangered species by name, view the search-matching species with some associated information- including a link to the species’ ECOS profile page for further information- and save the species to the user’s dashboard so a user can keep track of endangered species they are interested in. 

When a user clicks on the ‘Save Species to Dashboard’ button a POST request is sent to my Rails API backend via a fetch request. The species’ data that was pulled from the ECOS API is then saved to my backend API’s database and then fetched from there through a GET request to be rendered on the associated user’s dashboard page. User’s are also able to remove a species from their dashboard via a button rendered on the species’ card, which triggers a DELETE request to the backend. 


**Backend Design **

Now that I have provided a brief synopsis of the app’s functionality, let’s further discuss what’s going on under the hood. 

To create my backend I used the ‘rails new’ command. I then used the resource generator to create models, controllers, routes, and migrations for User and AnimalCard. I created User has_many AnimalsCards and AnimalCard belongs_to User relationships. Additionally, I created serializers for User and AnimalCard so that I would be able to view and access the associations (via JSON) more easily from the frontend. 

For user authentication I decided to utilize HTTPOnly Cookies- so that a user was able to stay logged-in upon page refresh and the client-side scripts were unable to access the user data. 

I created namespaced (Api::V1::) controllers for Users, AnimalCards, and Sessions. Within my Application Controller, I created two helper methods- ‘logged_in?’ and ‘current_user’- which I incorporated into my Sessions Controller for the authentication process. Additionally, within the Sessions Controller create action I used the authenticate method provided by has_secure_password (included in User model) to ensure that the user that was found in the database by username is providing the correct password. I used the BCrypt gem and password_digest to hash user passwords. 

Within the Sessions Controller I also defined two additional actions- ‘logged_in’ and ‘logout’. The ‘logged_in’ action utilizes the ‘logged_in?’ helper method, defined in Application Controller, to render JSON to the frontend that includes the information of the ‘current_user’ and a status of ‘logged_in: true’- if a user is in fact logged in. Otherwise, the action renders JSON that includes an empty object for user and a status of false for logged_in. The ‘logout’ action simply calls reset_session and renders JSON that includes an empty user object and status of ‘logged_in: false’. 

The User Controller actions come into play for the signup process. This controller contains two actions, ‘create’ and ‘show’- as these are the only two actions I required for my app’s frontend functionality.  The ‘create’ action (surprise, surprise) creates a new user and saves it to the database given that the object sent from the frontend contains the required parameters. The method then renders some JSON back to the frontend upon successful user creation that includes the newly created user object and a status of ‘logged_in: true’. Additionally, upon successful saving of a user to the database- the session id is set to the new user’s id. The show action is used to render the user’s information via JSON to the frontend. 

For the Animal_Cards Controller I defined create, index, and destroy actions. The create action creates a new AnimalCard and saves it to the database if the object sent from the frontend contains the required parameters. The action then renders a JSON object including the newly saved animal_card. The index action renders all of the animal_cards as JSON. Finally, the destroy action finds the animal card by id (sent from the frontend) and then deletes that animal card from the database. 

**Frontend Design **

On the frontend side, as per the project instructions, I created my ReactJS frontend with the ‘create-react-app’ generator. I began with setting up the store in redux/index.js, importing createStore, combineReducers, compose, and applyMiddleware from the redux library. I also imported thunk middleware from redux-thunk, enabling me to return functions from my action creators. I created my authReducer.js and authActions.js files, importing authReducer into my redux/index.js file, using it to create the store. In my src/index.js file I rendered my App component- which I connected to the store and used the store’s auth state to determine whether a user was logged in. Within the App component I used react-router to dynamically render the links that were to be displayed in the navbar depending upon whether a user was logged in or not. 

In my newly created authAction file I created an action assigned to the variable name ‘signup.’ This action took ‘user’ and ‘history’ as arguments and called a POST fetch request to the backend users path, including the user as stringified JSON within the body of the request. Once the returned Promise was resolved the returned JSON was dispatched to the reducer with a matching ‘AUTH_SUCCESS’ case. Upon reaching the reducer, the auth state was updated to include the returned user object and logged-in status. Also within this authAction file were actions for ‘login’, ‘checkLoggedIn’ and ‘logout’ - all of which contained fetch requests to the backend and returned Promises that were resolved and converted the response to JSON, then calling dispatch with types that matched the cases within the authReducer. 

I created stateful Login and Signup components- the default key values of said state being empty strings. Within both components I rendered forms- with an onSubmit event listener attached to each form and onChange listeners attached to each input field. The onChange event listeners update the value of the component state that corresponds to the changed input value. 

To incorporate the endangered species I began by creating animalActions.js and animalReducer.js files, importing the animalReducer to redux/index.js and adding it to the store. I added a fetchAllAnimals action creator to animalActions.js, which dispatches an action with type ‘LOADING_ANIMALS’ before calling a fetch request to the ECOS API. Once the returned Promise is resolved, the response is dispatched as the payload with a type of ‘FETCH_ALL_ANIMALS.’ This matches a case in the animalReducer and updates the state to include all of the animals that were returned from the fetch request. I mapped this dispatch action to props in the SearchPage component, which called the action within the componentDidMount hook and also renders the SearchBar component with the species from the store’s state passed to it as props. 

The SearchBar has component state with query (defaulted to empty string), data (defaulted to empty array), and filteredData keys (defaulted to empty array). The SearchBar component uses a ComponentDidMount hook to set the component’s state data key to the species that were passed as props from SearchPage. The component renders an input element which represents the search-bar and the SpeciesSearchResults component, which is passed the SearchBar component state’s filteredData as a prop. The input element has an onChange event listener attached that calls a method, which uses setState to update the query and filteredData keys. In order to filter the data the filter method is called on the previously set state’s data value, returning the data elements that have a name attribute which matches the query value. The filteredData is then iterated through and each individual object is rendered as an Animal component. 

The Animal components that are rendered each include a button that a user can click to save the species to their dashboard. This button has an onClick event listener that calls the saveAnimal dispatch action. This action sends a POST request to the backend API in order to save the species to the database and associate it with the current user. When a user navigates to their dashboard, the Dashboard component calls the fetchSavedAnimals dispatch action in ComponentDidMount in order to gain access to the saved species from the backend. The component renders an AnimalCard component for each of the user’s saved species with each having a button to remove the species from the dashboard- which calls a dispatch action that sends a DELETE fetch request to the backend to remove the species from the database. 


**Style**

For the styling of my app I incorporated TailwindCSS into my frontend, which after reading the documentation was very easy and enjoyable to implement! With the help of this framework I was able to give my application some great style! 

