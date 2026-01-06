**What is an Error Boundary?**
While building applications, errors are inevitable. They might come from APIs, UI or from several other places.

It’s very important to handle these errors gracefully & maintain good UX despite these errors.

Error Boundary is one such way of error handling in React.

How does Error Boundary help?
To understand this, let’s understand the situation before the introduction of the Error Boundary.

Before Error Boundaries, the errors occurring inside components eventually propagated & broke the UI or rendered the white screen.

This caused a really bad UX.

Error Boundary helps us to handle such errors & display a fallback UI instead of breaking the UI or showing white screen.

How to use Error Boundary?
React v16 officially introduced the Error Boundary.

It’s a Class-Based Component which can be used to wrap your application.

It accepts a fallback UI to be displayed in case your application has errors or otherwise, it simply renders the children component to resume the normal flow of your application.

This is how the React Documentation recommends using it

class ErrorBoundary extends React.Component {
 constructor(props) {
 super(props);
 this.state = { hasError: false };
 }
static getDerivedStateFromError(error) {
 // Update state so the next render will show the fallback UI.
 return { hasError: true };
 }
componentDidCatch(error, info) {
 // Example "componentStack":
 // in ComponentThatThrows (created by App)
 // in ErrorBoundary (created by App)
 // in div (created by App)
 // in App
 logErrorToMyService(error, info.componentStack);
 }
render() {
 if (this.state.hasError) {
 // You can render any custom fallback UI
 return this.props.fallback;
 }
return this.props.children;
 }
}
What’s the problem with React’s Error Boundary?
It cannot catch errors occurring in,

Event Handlers (these errors need to be handled with try-catch blocks)
Asynchronous Code (APIs, setTimeout, requestAnimationFrame etc.)
Server-side rendering
The error that occurs in Error Boundary itself
It does not work with Functional Components. Although we can make it work with a few code changes.
Hooks cannot be used inside it.
What’s the solution?
There’s a npm package called react-error-boundary which is a wrapper on top of the traditional Error Boundary component.


Using this package, we’re able to overcome all the issues faced in the traditional Error Boundary component.

How to use it?
You can wrap your entire application with <ErrorBoundary> or you can wrap individual components with <ErrorBoundary>.

The granularity of implementation is up to you.

Let’s understand how to use it.

import React from 'react';
import { ErrorBoundary } from "react-error-boundary";

const App = () => {
return <ErrorBoundary fallback={<div>Something went wrong</div>}>
/* rest of your component */
</ErrorBoundary>
}
This is the simplest example of using ErrorBoundary. There’s more to this library.
