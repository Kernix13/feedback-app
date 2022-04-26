# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Props

You can destructure props:
``jsx

<Header test="Hello there" /> 
function Header(props) {
  return (
    <header>
      <div className="container">
        <h2>{props.text}</h2>
<!-- or -->
function Header({ text }) {
  return (
    <header>
      <div className="container">
        <h2>{text}</h2>
```

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)

---

# From Brads Folder

---

# React Feedback App

This is a project from my React Front To Back 2022 course. It allows users to add, update and delete feedback. It uses a mock REST api with json-server.

This project goes over all of the fundamentals of React including...

- Components
- JSX
- Props (proptypes, defaultprops, etc)
- State (Component & App Level)
- Styling
- Handling Events
- Lists & Keys
- Forms
- Context API
- HTTP Requests

---

### Bug Fixes, corrections and code FAQ

The repository code here on the main branch has been updated due to bugs and issues found by students since the course was released.
If you are looking for exact code from the course then please check out the [originalcoursecode branch](https://github.com/bradtraversy/feedback-app/tree/originalcoursecode) of this repository.

The updates here aim to be a reference and resource for common questions asked
by students in the Udemy Q&A and for those wishing to make corrections to the
project.

#### Q: Why are we spreading data and item?

Before implementing json-server, when we updated feedback we didn't have feedback
ID in the updItem so spreading both data and item merges the two objects so we
have all the properties. After changing the code to use json-server we can instead use the
data response from json-server which will have an ID. So spreading both data and
item are no longer necessary.

> Code changes can be seen in [FeedbackContext.js](src/context/FeedbackContext.js#L62)

#### BUG: After editing a feedback it is not possible to add a feedback

After we edit a feedback our `feedbackEdit.edit` state is still true meaning we
only ever edit the same feedback again even if it's a new feedback.
The simple solution is to reset feedbackEdit state after updating a feedback.

> Code changes can be seen in [FeedbackContext.js](src/context/FeedbackContext.js#L65)

#### BUG: Validation not working correctly on feedback input

`handleTextChange` should validate on the input value, not on state.
State will only have changed on the next render of the component, which
happens after we call `setText`. Our text state is not the current value of
the input so is not suitable for validating the users input. Additionally we don't need to check twice for an empty string.

Code changes can be seen in [FeedbackForm.jsx](src/components/FeedbackForm.jsx#L24)

#### Q: How do you reset state after submitting a feedback?

Reset sate back to default after adding a new feedback.

> Code changes can be seen in [FeedbackForm.jsx](src/components/FeedbackForm.jsx#L57)

#### Q: Why does the default rating of 10 not show?

Initially `feedbackEdit.item.rating` is initially undefined, so when RatingSelect first mounts we set local state in our useEffect to undefined, which is why the the default rating of 10 does not show.
However there is no need for local state, useEffect or consuming context in this component as it's
just a duplicate of parent state. Relies on `selected` being passed as prop in [FeedbackForm.jsx](src/components/FeedbackForm.jsx#L64)

Additionally here we can simplify our JSX with iteration.

> Code changes can be seen in [RatingSelect.jsx](src/components/RatingSelect.jsx#L2) and [FeedbackForm.jsx](src/components/FeedbackForm.jsx#L64)

#### Simplify average rating calculation

Simplify average rating calculation without needing regex.

> Code changes can be seen in [FeedbackStats.jsx](src/components/FeedbackStats.jsx#L7)

#### BUG: About link icon shows in the wrong place with many feedback items

The about link icon container was positioned
absolute to the container meaning when lots of feedback's were added the icon
would appear off to the right and not at the bottom of the page.

> Code changes can be see in [index.css](src/index.css#L188)

---

# Usage

### Install dependencies

```bash
npm install
```

### Run

```bash
npm run dev
```

This will run JSON-server on port :5000 and React on port :3000
